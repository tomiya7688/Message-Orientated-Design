# 02. オブジェクトとメッセージ

## メッセージは関数呼び出しではない

本設計でいう Message は、関数呼び出しを別の記法で書いたものではありません。

例えば次のような情報そのものがメッセージです。

    owner, dog, move, 100, 0

現時点での基本構造は次のように表します。

    Message
    ├─ from
    ├─ to
    ├─ type
    └─ content

例えば、

    from: owner
    to: dog
    type: move
    content:
        x: 100
        y: 0

です。

送信側が知るべきなのは「dog の move 関数を呼ぶ方法」ではなく、「dog に move というメッセージを送りたい」ということです。

## 送信元と送信先

メッセージは、論理的な送信元と送信先を識別できる必要があります。

これにより受信側は、要求の意味だけでなく「誰からの要求か」を判断材料にできます。また応答先も明確になります。

ここでいう from / to は論理的な送信元・送信先の識別情報です。暗号学的な電子署名や認証方式については、現時点では仕様を定めません。

## type と content

type は、受信主体が理解するメッセージそのものの意味を表します。

例えば、

    type: move
    type: can_pass
    type: material_at
    type: movement_blocked

などです。

content は、その type のメッセージを成立させるために必要な内容です。

    type: move
    content:
        x: 100
        y: 0

query、decision、request、event、result のような共通分類を Message の必須フィールドにはしません。

「情報が欲しい」「判断してほしい」「行動してほしい」「起きたことを通知したい」といった性質は、それぞれの type と content が表現します。

例えば、

    from: physical
    to: material
    type: material_at
    content:
        position: [100, 200]

は情報を求めるメッセージです。

一方、

    from: physical
    to: material
    type: can_pass
    content:
        body: dog
        path: ...

は Material 領域に判断を依頼するメッセージです。

Message Manager はこの意味分類を利用してドメイン判断を行いません。type を解釈して処理を決める責任は最終的に受信主体側にあります。

## Message は不変である

一度生成された Message は変更しません。

Manager が配送途中で from、to、type、content を書き換えてはいけません。

別の意味、別の宛先、別の処理段階を表現する必要がある場合は、元の Message を変更するのではなく、新しい Message を生成します。

例えば、

    Dog Brain
        |
        | type: move
        v
    Dog Moving
        |
        | type: animal_move_request
        v
    Animal Manager
        |
        | type: physical_move_request
        v
    Physical Manager

という流れでは、一つの Message が書き換えられていくのではありません。

各段階の主体が判断した結果として、新しい Message が生成されます。

このため、送信主体が送った Message と、受信主体が受け取る Message の内容は一致します。

## Message にグローバル ID を持たせない

Message 自体には、システム全体で共通の Message ID を要求しません。

「何番目に発行されたか」「ある Manager を何番目に通過したか」といった情報は、送信主体や受信主体にとって通常は意味を持たないためです。

Manager は実装上必要であれば、自分の管理範囲の内部で Message に管理用の ID、キュー番号、時刻、再送回数などを関連付けても構いません。

ただし、それらは Message の意味論には含めません。

    Message
        from
        to
        type
        content

    Manager Internal Metadata
        internal_id
        queue_position
        received_at
        retry_count
        ...

Manager Internal Metadata は配送システムの内部情報であり、通常は送信主体や受信主体へ露出させません。

各 Manager が同じ Message に異なる内部 ID を付与しても問題ありません。それらは Message の同一性を定義するものではありません。

## 応答もメッセージ

オブジェクト境界を越える応答を、関数の return 値として返すことは基本モデルにしません。

要求が正しくても正しくなくても、必要な応答は Message Sender から新しい Message として送ります。

例:

    owner -> dog
    type: move
    content:
        x: 100
        y: 0

成功時:

    dog -> owner
    type: move_accepted
    content: ...

拒否時:

    dog -> owner
    type: move_rejected
    content: ...

応答を元の Message の ID に依存させることも、基本仕様にはしません。

必要な対応関係は、Message の意味と内容によって表現することを基本とします。実装上の追跡情報が必要な場合は Manager 内部の管理情報として扱えます。

## 他領域の状態

他のオブジェクトや他の領域が所有する状態を直接読みに行きません。

必要な情報がある場合は、その情報を所有する主体へメッセージを送り、メッセージとして結果を受け取ります。

また、可能であれば生の状態を取得して外部で判断するのではなく、その状態を所有する主体へ判断自体を依頼することも検討します。

例えば、

    「壁の一覧をください」

と問い合わせて Physical 側で判断するより、

    「この経路を通過できますか」

という判断を適切な領域へ依頼する方が、領域内部の状態を外へ漏らさずに済む場合があります。
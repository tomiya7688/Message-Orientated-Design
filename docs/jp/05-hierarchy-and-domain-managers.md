# 05. 階層と Domain Manager

## Message Manager と Domain Manager

本書では、二種類の Manager の役割を区別します。

### Message Manager

メッセージの配送を担当します。内容のドメイン意味を判断しません。

### Domain Manager

その領域に固有の判断、調停、状態管理を担当するオブジェクトです。Domain Manager も他のオブジェクトと同様に、メッセージで通信します。

## 複雑なオブジェクトを分割する

Dog の内部挙動が複雑になった場合、すべてを一つの巨大な Dog に押し込む必要はありません。

例えば次のように分割できます。

    Dog
      - Dog Brain
      - Dog Moving
      - ...

Dog Brain と Dog Moving は互いの内部関数を直接呼びません。Dog Manager を通じてメッセージを交換します。

## 上位領域へ渡す

Dog Moving が移動候補を計算しても、それだけで世界の中で実際に移動できるとは限りません。

Dog 固有の処理から、より上位の領域へ順に判断を委ねられます。

    Dog domain
        |
        v
    Animal domain
        |
        v
    Physical domain

Animal Manager は animal 固有の条件を判断します。Physical Manager は物理挙動を判断します。

上位へ行くほど、Dog 固有の事情ではなく、より一般的な領域の規則を扱います。

## 他領域への問い合わせ

Physical Manager が壁や電柱などの情報を必要とした場合、Material 側の内部状態を直接読みません。

Material Manager へ「この情報が必要」というリクエストメッセージを送り、Material Manager が自分の領域の状態をもとに応答メッセージを返します。

    Physical Manager
        | request
        v
    Material Manager
        | response
        v
    Physical Manager

この原則により、状態の所有者と、その状態を使いたい側の境界を保てます。

## 重要な原則

    他領域の状態を直接参照しない。
    必要な情報や判断は、その領域を所有する主体へメッセージで依頼する。
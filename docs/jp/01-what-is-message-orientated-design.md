# 01. Message Orientated Design とは

## 定義

Message Orientated Design は、**状態を持つ独立した主体を状態機械として扱い、主体どうしの相互作用を実際のメッセージ交換によって構成する設計モデル**です。

最も基本的な境界は次です。

    オブジェクト間 = Message
    オブジェクト内部 = Function Call

ある主体が別の主体へ処理を依頼するとき、相手の内部関数を直接呼びません。

送信側は Message Sender から Message を送り、受信側では Message Receptor が Message を受け取り、対応する内部関数を呼び出します。

## オブジェクトは状態機械である

各オブジェクトは自分の状態を所有します。

受信した Message と現在の状態をもとに、自分自身で処理と状態遷移を決めます。

概念的には次のように表せます。

    (Current State, Incoming Message)
        ->
    (Next State, Outgoing Messages)

これは概念モデルであり、実装を純粋関数に限定するものではありません。

重要なのは、状態に関する判断を、その状態を所有する主体が行うことです。

## Message は通信そのものである

Message は、関数呼び出しを別の構文で表したものではありません。

例えば、

    from: owner
    to: dog
    type: move
    content:
        x: 100
        y: 0

という情報そのものが Message です。

送信側が dog の内部にある move 関数を知る必要はありません。dog に対して move という意味の Message を送るだけです。

## 境界を越えて内部を触らない

他オブジェクトの内部状態を直接読み書きしません。

別領域が所有する情報や判断が必要なら、その領域へ Message を送ります。

可能であれば、生のデータを取り出して外部で判断するよりも、その状態を所有する主体へ判断そのものを依頼します。

## Sender と Receptor

各オブジェクトは外部との通信境界として Message Sender と Message Receptor を持ちます。

Message Receptor の責務は限定されます。

1. Message を受け取る。
2. type を識別する。
3. 対応する内部関数を呼ぶ。

Message の内容が妥当か、現在の状態で要求を受理できるか、といった意味上の判断は Receptor ではなく、その次に呼ばれた内部処理が行います。

## Message Manager

Message Manager は Message の宛先を見て配送します。

同じ管理領域内で完結する通信は、その領域の Manager だけで処理します。Global Manager を必ず経由させるものではありません。

境界を越える Message だけを上位 Manager へ渡すことで、システムを階層化できます。

## Domain Manager

Message Manager が配送を担当するのに対し、Domain Manager はその領域固有の判断を担当します。

例えば Dog、Animal、Physical、Material という領域がある場合、それぞれの領域が自分の責務だけを判断し、他領域が必要になれば Message を送ります。

## Message は不変である

一度生成された Message は書き換えません。

処理の結果として別の意味や宛先を持つ通信が必要になった場合は、新しい Message を生成します。

配送上必要な ID、キュー番号、再送回数などは Manager の内部情報であり、Message 自体の意味には含めません。

## 継承は中心ではない

継承を禁止するものではありませんが、継承は Message Orientated Design の成立条件ではありません。

この設計で重要なのは、共通の親クラスを持つことではなく、各主体が受け取った Message を自分自身で解釈できることです。

## 目標

Message Orientated Design が目指すのは、システムが巨大化しても、

- 状態の所有者が明確であること
- 判断責任が局所化されていること
- 領域を越える依存が Message として明示されること
- 他主体の内部実装への直接依存を避けること
- 通信構造を階層化して拡張できること

を維持できる設計です。

以降の章では、Message、Sender / Receptor、Manager、階層化について具体的に定義します。

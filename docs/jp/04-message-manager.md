# 04. Message Manager

## 配送を担当するオブジェクト

Message Manager はメッセージの宛先を見て、対象オブジェクトの Message Receptor へ配送します。

    Sender
      |
      v
    Message Manager
      |
      v
    Target Receptor

Message Manager 自身もオブジェクトであり、Message Sender と Message Receptor を持ちます。

## Message Manager の責務

Message Manager の中心的な責務は配送です。

- メッセージを受け取る。
- 宛先を確認する。
- 自分の管理範囲にいる対象なら、その対象の Receptor へ配送する。
- 自分の管理範囲外なら、必要な上位 Manager へ渡す。

Message Manager は、dog の move が意味的に正しいか、animal として移動可能か、物理的に衝突するか、といったドメイン固有の判断を行いません。

## ローカル通信

内側の通信で Global Manager を経由する必要はありません。

例えば同じ Dog 内に Dog Brain と Dog Moving があるなら、両者の通信は Dog Manager の管理範囲だけで完結できます。

    Dog Brain
        |
        v
    Dog Manager
        |
        v
    Dog Moving

上位の Animal Manager や Global Manager を通す必要はありません。

## 境界を越える通信

管理範囲を越える場合だけ上位へ渡します。

    Local A
       |
       v
    Upper Manager
       |
       v
    Local B

原則は次です。

    メッセージは、配送に必要な最小の管理領域だけを通る。

これにより Global Manager に全通信を集中させず、境界を越える通信だけを上位で扱えます。

## 階層化

Manager は必要に応じて階層化できます。

送信元のローカル Manager から、宛先との共通の管理領域まで上がり、そこから宛先側へ降りる構造を取れます。

各オブジェクトは配送経路を知る必要がありません。宛先を指定して Sender からメッセージを出せば、経路は Manager 側が決めます。
# 03. Message Sender と Message Receptor

## 各オブジェクトが持つ境界

各オブジェクトは、外部との通信境界として Message Sender と Message Receptor を持ちます。

    Incoming Message
          |
          v
    Message Receptor
          |
          v
    Object internal functions / state machine
          |
          v
    Message Sender
          |
          v
    Outgoing Message

## Message Receptor の責務

Message Receptor の仕事は限定します。

1. 自分宛てのメッセージを受け取る。
2. メッセージの種類を識別する。
3. 対応する内部関数を呼び出す。

例えば dog の Receptor が次のメッセージを受け取ったとします。

    owner, dog, move, 100, 0

Receptor は move メッセージに対応する内部関数を呼び出します。

    move_request(owner, 100, 0)

ここで初めて通常の関数呼び出しになります。

## Receptor がしないこと

Receptor は次のような意味判断を担当しません。

- 100, 0 という値が妥当か。
- 現在の状態で move できるか。
- owner に move を要求する権限があるか。
- 成功時や失敗時に何を返すべきか。

これらは move_request など、呼び出された側の処理が判断します。

Receptor は「メッセージから内部関数への変換境界」であり、ドメインロジックを置く場所ではありません。

## Message Sender の責務

Message Sender は、オブジェクトが外部へ送るメッセージの出口です。

他オブジェクトの関数を直接呼び出す代わりに、送信元、送信先、メッセージ種別、引数などを持つメッセージを外へ出します。

不正な要求への拒否も、必要であれば Sender を使ってメッセージとして返します。
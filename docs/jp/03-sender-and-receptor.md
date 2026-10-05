# 03. Message Sender / Receptor

各オブジェクトは外部との境界に Sender と Receptor を持ちます。

    Message -> Receptor -> internal function
    internal processing -> Sender -> Message

## Receptor

Receptor の仕事は3つだけです。

1. Message を受け取る。
2. type を識別する。
3. 対応する内部関数を呼ぶ。

例:

    type: move
        ↓
    move_request(...)

値が妥当か、現在の状態で実行できるか、送信者に権限があるか、といった判断は Receptor ではなく呼び出された内部処理が行います。

## Sender

Sender は外部へ Message を出す唯一の出口です。他オブジェクトの内部関数を直接呼びません。

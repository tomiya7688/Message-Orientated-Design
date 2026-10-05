# 02. オブジェクトと Message

Message の最小構造は次です。

    Message
    ├─ from
    ├─ to
    ├─ type
    └─ content

例:

    from: owner
    to: dog
    type: move
    content:
        x: 100
        y: 0

type は Message の意味です。query や request のような共通 kind は必須にしません。「情報が欲しい」「判断してほしい」などは type と content で表現します。

Message は **immutable** です。配送途中で from / to / type / content を書き換えません。別の意味や宛先が必要なら、新しい Message を作ります。

Message 自体にグローバル ID は要求しません。Manager が配送管理のため内部 ID を持つのは構いませんが、それは送信側・受信側の意味情報ではありません。

応答も return 値ではなく、新しい Message として返します。

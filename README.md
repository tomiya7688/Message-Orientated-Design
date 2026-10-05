# Message Orientated Design

状態を持つ独立した主体が、互いの内部関数を直接呼ばず、**Message** を交換して協調するための設計モデルです。

## まず読む

日本語が正本です。

- **日本語:** [docs/jp/README.md](docs/jp/README.md)
- English: [docs/en/README.md](docs/en/README.md)

Checker は別です。

- [Message Orientated Design Checker](message-orientated-design-checker/README.md)

## 核心

    オブジェクト間 = Message
    オブジェクト内部 = Function Call

各オブジェクトは状態機械として振る舞い、外部との境界に Message Sender / Message Receptor を持ちます。

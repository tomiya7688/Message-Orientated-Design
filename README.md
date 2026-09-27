# Message Orientated Design

Message Orientated Design は、**状態を持つ独立した主体が、相手の内部関数を直接呼び出すのではなく、実際のメッセージを交換して協調する**ための設計モデルです。

このリポジトリでは、現代一般に使われる「オブジェクト指向」という語との混同を避けるため、この考え方を **Message Orientated Design / メッセージ指向設計** と呼びます。

## Core idea

```text
Object間      = Message
Object内部    = Function Call
```

各オブジェクトは状態機械であり、Message Sender と Message Receptor を持ちます。

```text
Object A
  │
  ▼
Sender
  │
  │ Message
  ▼
Message Manager
  │
  ▼
Receptor
  │
  ▼
Object B internal function
```

Message Receptor はメッセージを受け取り、その種類に対応する内部関数を呼び出すところまでを担当します。メッセージの意味的な妥当性や、現在の状態で要求を受理できるかどうかは、呼び出された側の処理が判断します。

Message Manager は宛先を見て配送します。大規模なシステムでは Manager を階層化し、ローカル通信はローカルで完結させ、境界を越える通信だけを上位へ渡します。

## Documentation

日本語版を正本とします。英語版は日本語版に対応する翻訳です。

- [日本語 / Japanese — canonical](docs/jp/README.md)
- [English](docs/en/README.md)

## Repository scope

このリポジトリの本体は設計思想と仕様を記述する文書です。

将来的に、この設計に沿っているかを確認する checker を付属させますが、checker 自体がこのプロジェクトの中心ではありません。

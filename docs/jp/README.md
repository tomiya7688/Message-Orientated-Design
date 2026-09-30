# 日本語ドキュメント

このディレクトリを Message Orientated Design の正本とします。

英語版は docs/en に置き、日本語版の内容に対応する翻訳として管理します。日本語版と英語版に差異がある場合は、日本語版を基準とします。

## まず読む文書

- [00. オブジェクト指向の原型](00-object-orientation-origins.md)
- [01. Message Orientated Design とは](01-what-is-message-orientated-design.md)

最初の章では、この設計がどのような歴史的発想を出発点としているかを説明します。

次の章では、このプロジェクト独自の Message Orientated Design を定義します。歴史的な Smalltalk の説明と、このプロジェクトの仕様は区別します。

## 設計仕様

- [02. オブジェクトとメッセージ](02-object-and-message.md)
- [03. Message Sender と Message Receptor](03-sender-and-receptor.md)
- [04. Message Manager](04-message-manager.md)
- [05. 階層と Domain Manager](05-hierarchy-and-domain-managers.md)
- [06. Dog / Animal / Physical / Material の例](06-dog-world-example.md)

## Checker

Checker の検査内容や実装仕様は、本体の設計仕様とは分離します。

- [Message Orientated Design Checker](../../message-orientated-design-checker/docs/jp/README.md)

Checker はこの文書を基準に検査する付属ツールであり、Checker の都合で Message Orientated Design 本体の原則を決めません。

## 現時点での位置づけ

この文書は、ここまでに合意した設計原則を固定するためのものです。未決定の実装方式、通信プロトコル、永続化方式、並行実行方式、暗号方式などは、この時点では仕様化しません。

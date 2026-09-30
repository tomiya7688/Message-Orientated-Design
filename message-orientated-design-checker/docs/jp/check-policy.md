# 検査方針

## Checker の位置づけ

Checker は Message Orientated Design の設計原則に沿っているかを確認するための付属ツールです。

Checker の実装都合によって設計原則を決めるのではなく、リポジトリ直下の `docs/jp` で定義された原則を Checker が追いかけます。

## 現時点で検討する検査項目

- オブジェクト境界を越えて他オブジェクトの内部関数を直接呼んでいないか。
- 他オブジェクトや他領域の内部状態を直接読み書きしていないか。
- 外部との通信が Message Sender / Message Receptor を経由しているか。
- Receptor にドメイン判断や妥当性判定を入れていないか。
- Receptor が受信した Message の type に対応する内部関数を呼んでいるか。
- オブジェクト境界を越える結果を return 値だけで返していないか。
- 必要な応答を Sender から Message として返しているか。
- Message Manager に配送以外のドメインロジックを集中させていないか。
- 他領域の情報が必要なとき、その領域へ Message で問い合わせているか。
- ローカルで完結できる通信を不必要に Global Manager へ集約していないか。
- 配送途中で Message の from / to / type / content を書き換えていないか。
- Manager 内部の配送管理 ID を、Message 自体の意味として外部へ露出させていないか。

## 継承の扱い

継承の有無だけで合否を決めません。

継承は Message Orientated Design の中心ではありません。継承による実装依存が、主体の独立性や Message 境界を壊していないかを検査対象として考えます。

## 未決定事項

以下はまだ決定していません。

- 対象言語
- 静的解析方式
- 各ルールの重大度
- 設定ファイル形式
- CI 連携
- 自動修正の有無
- Manager / Sender / Receptor をコード上で識別する方法

これらは Message Orientated Design 本体の仕様ではなく、Checker の仕様としてこのディレクトリで決定します。

# 05. 階層と Domain Manager

Message Manager と Domain Manager は役割が違います。

- **Message Manager:** 配送する。
- **Domain Manager:** その領域の意味を判断する。

複雑な主体は分割できます。

    Dog
    ├─ Dog Brain
    └─ Dog Moving

Dog Brain と Dog Moving は直接関数を呼び合わず、Dog Manager 経由で Message を交換します。

別領域の情報が必要なら、その領域へ Message で問い合わせます。

    Physical Manager
        ↓ request
    Material Manager
        ↓ response
    Physical Manager

他領域の状態を直接読むのではなく、**その状態を所有する主体に情報または判断を依頼する**のが基本です。

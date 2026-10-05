# 04. Message Manager

Message Manager は **配送だけ**を担当します。

    Sender -> Message Manager -> Target Receptor

役割は次の通りです。

- 宛先を見る。
- 管理範囲内なら対象 Receptor へ渡す。
- 管理範囲外なら上位 Manager へ渡す。

ドメイン判断はしません。

同じ管理領域内の通信はローカルで完結させます。Global Manager を必ず通す必要はありません。

    Dog Brain
        ↓
    Dog Manager
        ↓
    Dog Moving

原則は **必要な最小の管理領域だけを通る** ことです。

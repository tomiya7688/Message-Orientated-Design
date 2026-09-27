# 06. Dog / Animal / Physical / Material の例

この章は、ここまでの原則を一つの流れとして示します。

## 1. Dog 内部の要求

Dog Brain が「移動したい」と判断したとします。

Dog Brain は Dog Moving の関数を直接呼びません。

    Dog Brain
        | move request
        v
    Dog Manager
        |
        v
    Dog Moving Receptor
        |
        v
    move_request(...)

Dog Moving の Receptor はメッセージ種別を見て、対応する内部関数を呼ぶだけです。

## 2. Dog Moving の結果

Dog Moving は Dog 内部の状態を使って移動候補を計算します。

計算結果が世界の中で成立するかを自分だけで決めるのではなく、必要な上位領域へメッセージを出します。

    Dog Moving
        | movement candidate
        v
    Dog Manager
        |
        v
    Animal Manager

## 3. Animal 固有の判断

Animal Manager は animal 固有の条件を判断します。

例えば、身体状態や animal としての制約が関係するなら、それは Animal 領域の責務です。

そこで成立した要求を、物理的な判定が必要な形にして Physical Manager へ渡します。

    Animal Manager
        | physical movement request
        v
    Physical Manager

## 4. Physical から Material への問い合わせ

Physical Manager が衝突判定などのために壁や電柱の情報を必要とするとします。

Physical Manager は Material の内部データを直接参照しません。

    Physical Manager
        | material information request
        v
    Material Manager
        | material information response
        v
    Physical Manager

Material Manager は、自分が所有する Material 領域の状態をもとに応答します。

## 5. 物理結果

Physical Manager は得られた情報を使って物理挙動を判定し、その結果をメッセージとして返します。

結果は必要に応じて、Physical -> Animal -> Dog という領域境界をメッセージとして戻ります。

## 全体像

    Dog Brain
        |
        v
    Dog Manager
        |
        v
    Dog Moving
        |
        v
    Animal Manager
        |
        v
    Physical Manager
        | request
        v
    Material Manager
        | response
        v
    Physical Manager
        |
        v
    Animal Manager
        |
        v
    Dog Manager

重要なのは、各境界で相手の内部関数や内部状態へ直接アクセスせず、メッセージによって協調していることです。
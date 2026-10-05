# 06. Dog / Animal / Physical / Material の例

Dog Brain が移動を要求する例です。

    Dog Brain
        ↓ move
    Dog Manager
        ↓
    Dog Moving
        ↓ animal_move_request
    Animal Manager
        ↓ physical_move_request
    Physical Manager
        ↓ material query
    Material Manager
        ↓ material result
    Physical Manager
        ↓ result
    Animal Manager
        ↓
    Dog Manager

役割は分かれています。

- **Dog Moving:** Dog 内部の移動処理。
- **Animal Manager:** Animal 固有の条件を判断。
- **Physical Manager:** 物理挙動を判断。
- **Material Manager:** 壁や電柱など Material 領域の情報・判断を提供。

各境界では内部状態や内部関数へ直接アクセスせず、Message を交換します。

# 00. オブジェクト指向の原型

## この章の目的

Message Orientated Design は、現代一般に「オブジェクト指向」と呼ばれている設計技法を言い換えたものではありません。

このプロジェクトが出発点としているのは、Alan Kay と初期 Smalltalk の系譜で強く語られていた、**独立した主体が内部を保護し、メッセージによってのみ相互作用する**という考え方です。

ただし、本プロジェクトは初期 Smalltalk の歴史的再現でも、Alan Kay の設計をそのまま仕様化するものでもありません。歴史的な発想を出発点とし、現在の大規模なソフトウェア設計へ適用できるよう、独自に規則化するものです。

## 初期の発想

Alan Kay は *The Early History of Smalltalk* で、複雑さを抑えながら大規模なシステムを作るための発想を、生物学的なモデルになぞらえて説明しています。

そこでは、保護された普遍的な「細胞」が、互いにメッセージだけを使って相互作用するという方向が述べられています。

重要なのは、中心に置かれていたものが単なる「データと手続きのひとまとめ」ではなく、**境界を持つ主体どうしの通信**だったことです。

Kay は後年の 1998 年にも、Smalltalk は構文やクラスライブラリのことではなく、さらにはクラスそのものが中心なのでもないと説明し、中心的な考えを messaging だと述べています。

このため、本プロジェクトでは次の点を歴史的な出発点として扱います。

- 主体は自分の内部状態を持つ。
- 他の主体は、その内部状態を直接操作しない。
- 主体間の相互作用はメッセージで行う。
- メッセージを受け取った側が、それをどう解釈し、どう振る舞うかを決める。
- 大規模なシステムでは、内部構造そのものよりも、主体間の通信境界が重要になる。

## 現代一般の「オブジェクト指向」との区別

現在「オブジェクト指向」という言葉は、クラス、継承、インターフェース、カプセル化、ポリモーフィズムなどを中心に説明されることが多くあります。

それらは有用な技法ですが、このプロジェクトが扱う中心概念とは一致しません。

特に、継承は Message Orientated Design の成立条件ではありません。同じメッセージを異なる主体がそれぞれ解釈できれば、共通の親クラスを持たなくても多態的な振る舞いは成立します。

そのため、このリポジトリでは「本来のオブジェクト指向」という名称をそのまま使わず、現代の一般的な用法との混同を避けるため **Message Orientated Design / メッセージ指向設計** という別名を使います。

## 歴史と本仕様を混同しない

歴史的資料は、この設計の着想を説明するためのものです。

このリポジトリで定義する Message Sender、Message Receptor、階層化された Message Manager、Domain Manager、immutable な Message などの具体的な規則を、Alan Kay や Smalltalk がそのまま定義していたと主張するものではありません。

それらは、本プロジェクトがメッセージ中心の考え方を大規模システムへ適用するために導入する設計です。

## 参考資料

- Alan C. Kay, *The Early History of Smalltalk*: https://archive.computerhistory.org/resources/access/text/2024/06/102739394-05-0001-acc.pdf
- Alan Kay, “prototypes vs classes was: Re: Sun's HotSpot”, Squeak mailing list, 1998: https://lists.squeakfoundation.org/pipermail/squeak-dev/1998-October/017019.html
- Computer History Museum, *Introducing the Smalltalk Zoo*: https://computerhistory.org/blog/introducing-the-smalltalk-zoo-48-years-of-smalltalk-history-at-chm/

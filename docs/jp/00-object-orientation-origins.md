# 00. オブジェクト指向の原型

Alan Kay と初期 Smalltalk では、中心にあったのはクラス階層そのものではなく、**内部を保護した主体どうしが Message で相互作用する**という考え方でした。

Kay は後年にも、Smalltalk の中心はクラスではなく messaging だと説明しています。

このプロジェクトはその方向を出発点にします。ただし、Sender / Receptor / 階層 Manager / immutable Message などは、このプロジェクト独自の設計です。歴史的 Smalltalk の再現ではありません。

現代の「オブジェクト指向」と区別するため、ここではこの設計を **Message Orientated Design** と呼びます。

## 参考

- Alan C. Kay, The Early History of Smalltalk: https://archive.computerhistory.org/resources/access/text/2024/06/102739394-05-0001-acc.pdf
- Alan Kay, Squeak mailing list, 1998: https://lists.squeakfoundation.org/pipermail/squeak-dev/1998-October/017019.html

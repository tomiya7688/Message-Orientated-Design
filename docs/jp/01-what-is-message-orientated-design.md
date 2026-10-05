# 01. Message Orientated Design とは

Message Orientated Design は、**状態を持つ独立した主体を状態機械として扱い、主体間の通信を Message に限定する設計**です。

    オブジェクト間 = Message
    オブジェクト内部 = Function Call

基本原則は5つです。

1. 各オブジェクトは自分の状態を所有する。
2. 他オブジェクトの内部関数を直接呼ばない。
3. 他オブジェクトの内部状態を直接読み書きしない。
4. 外部とのやり取りは Message Sender / Receptor を通す。
5. 受信した Message をどう解釈するかは受信側が決める。

継承は必須ではありません。重要なのは共通の親クラスではなく、同じ Message を各主体が自分で解釈できることです。

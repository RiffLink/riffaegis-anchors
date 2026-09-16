# RiffAegis Public Audit Anchor Ledger (公開マークルルート監査台帳)

This repository serves as the **public, tamper-evident audit anchor ledger** for [RiffAegis](https://github.com/RiffLink/RIFFAEGIS) — the Post-Quantum Secure E-Signature Platform.

---

## 🛡️ 役割と位置づけ (Purpose & Architecture)

RiffAegis では、電子契約の締結が完了した瞬間に、すべての当事者の署名・原本ハッシュ・NICT日本標準時原子時計時刻を結合した **Final Merkle Root（最終マークルルート）** を算出します。

本リポジトリは、その Merkle Root と契約IDを外部の公開環境へ即座に刻み込むための**「迅速な状況証拠アンカー」**です。

1. **Web即時可視性 (Instant Public Visibility):**
   * 契約当事者や第三者が、GitHubのWeb画面上でコミットハッシュ、コミット日時、コミットメッセージ（Document ID & Merkle Root）を即座に視認・照合できます。
2. **多層タイムスタンプ (Multi-Layered Verification):**
   * **一次アンカー（即時確認用）：** 本 GitHub コミット（秒単位の即時記録）
   * **絶対的永続アンカー（改ざん不能）：** OpenTimestamps（ビットコイン・ブロックチェーン上に確定カレンダーを埋め込み、永久不変性を保証）

---

## 📜 コミット記録フォーマット (Commit Format)

RiffAegis サーバーによって、合意完了時に以下のフォーマットで自動的にコミットが追加されます：

```text
anchor: <DOCUMENT_UUID>

Final Merkle Root: <64-HEX SHA-256 HASH>
Timestamp: <ISO-8601 UTC>
Source: RiffAegis Finalization Engine

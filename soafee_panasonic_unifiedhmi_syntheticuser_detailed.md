
# SOAFEE × Panasonic – Unified HMI：クラウド上で Synthetic User によるHMI評価 詳細整理
（SOAFEE公式Blueprint・Unified HMI技術資料・Varjo事例の関連性に基づく）

## 1. 概要
**Panasonic Automotive Systems** は、SOAFEE（Scalable Open Architecture for Embedded Edge）のエコシステムに参加し、
**Unified HMI（仮想ディスプレイ基盤）** を開発・公開した。これは、車載HMIを“ハードウェア依存から解放”し、**クラウド上でHMI開発・評価が完結する次世代アーキテクチャ**である。citeturn29search212

Unified HMI の最大の特徴は：
- **VirtIO‑GPUを拡張した仮想ディスプレイ技術**
- **マルチOS・マルチECUを統合するディスプレイ仮想化レイヤ**
- **クラウド環境でマルチディスプレイHMIを構築・評価可能**
- **Synthetic User（AIエージェント）によるHMIレビューに極めて相性が良い**

SOAFEEと組み合わせることで、車載HMIが **“ソフトウェア定義（SDV）”として進化できる基盤**となる。citeturn29search212

---

## 2. Unified HMI とは何か？（Panasonic Automotive 提案）
Unified HMI は、Panasonic Automotive が SOAFEE Blueprint として公開した、
**車載HMI向けの標準化された仮想ディスプレイ・フレームワーク**である。citeturn29search212

### ● 核心技術：Remote VirtIO GPU（RVGPU）
- VirtIO‑GPU を拡張し、**クラウド側でレンダリングした画面を車載側にストリーミング**
- マルチディスプレイ（CID／HUD／メータ）が“仮想的に統合される”
- HMIアプリは「どのGPU／どの表示器で動くか」を意識せず開発可能

### ● Distributed Display Framework
- ウィンドウ管理・レイアウト管理を仮想化
- 車載SoCが分散しても**HMIを一体化制御**

### ● 対応OS
- Linux
- AGL（Automotive Grade Linux）
- Android（開発中）

→ **クラウド上で動くHMIをそのまま車両に反映できる“SDV時代の標準基盤”** となる。citeturn29search212

---

## 3. なぜ “Synthetic User × Unified HMI” が強力なのか？
Unified HMI は仮想ディスプレイをクラウド上に完全再現できるため、
**AI Synthetic User（LLMエージェント）によるHMI評価が非常に容易**になる。

その理由：
- HMIがクラウド上の仮想ディスプレイとしてレンダリング → AIが直接操作可能
- マルチディスプレイの配置・遷移・亮度・視覚ノイズを“画面構造として解析”できる
- 画面遷移ログ・入力デバイスイベントを AI エージェントに直接供給可能
- 複数エージェント（複数ユーザー役）を同時に走らせる“マルチエージェントHMI評価”が可能

これは、従来のHMI評価が**実車・試作・固定的シミュレータ**に依存していた構造を根本的に変える。

---

## 4. Synthetic User が Unified HMI 上で評価できる項目
### ● 1. UI操作性（Button / Menu / Touch / Rotary）
- 階層の深さ
- 戻る動線の複雑度
- 誤タップ・不明瞭アイコン

### ● 2. マルチディスプレイの連携UX
- メータ→CID→HUD の注意遷移
- 二重表示・過剰表示の検出

### ● 3. 認知負荷（Cognitive Load）評価
- 表示情報量が多すぎる箇所をAIが指摘
- 対応時間（Reaction Time）をシミュレーション

### ● 4. 通知UX（Interruptibility）
DriverDoubles（Aalto大）の Synthetic User と同様の手法で：
- 運転中の通知の煩わしさ
- 無視されやすい通知
を仮想的に評価可能。

### ● 5. HMIの文化差 / ユーザー属性差
Synthetic Persona（性格・年齢・経験値）を付与し：
- 高齢者モデル
- 新人ドライバー
- 反応の遅いユーザー
など仮想ユーザーを大量生成できる。

---

## 5. アーキテクチャ：SOAFEE × Unified HMI × Synthetic Users
以下の3層で構成される評価体系が実現する。

### **① Cloud Layer（HMI開発・仮想ディスプレイ環境）**
- HMIアプリをクラウドでビルド
- VirtIO‑GPU拡張で仮想ディスプレイ生成
- Synthetic Userエンジンをクラウド側に配置

### **② Simulation Layer（UX評価）**
- Synthetic User が仮想ディスプレイ操作
- マルチエージェントで同時に評価
- A/B HMI比較
- UXパターン自動抽出

### **③ Vehicle Layer（SDV実機）**
- 統合HMI（Unified HMI）が車載にデプロイ
- クラウドと OTA（SOAFEE標準）で同期

→ **開発→評価→車載デプロイが1つのラインで統合**される。

---

## 6. SOAFEE公式資料に記載されている Unified HMI の機能（要点）
以下は SOAFEE Blueprint で説明されている Unified HMI の明確な特徴：
- “**hardware‑independent cockpit UI/UX**”（ハード非依存のHMI）citeturn29search212
- Multi‑display UI を cloud で構築し、車載に deployment 可能citeturn29search212
- VirtIO‑GPU ベースの **remote rendering**（クラウド描画）citeturn29search212
- Linux / AGL / Android（開発中）対応のオープンフレームワークciteturn29search212
- SOAFEE と強く統合され、SDV開発の標準候補になりつつある

---

## 7. Panasonic Automotive が Unified HMI によって得るメリット
### ✔ 1. 仮想HMI環境での高速プロトタイピング
### ✔ 2. 実車プロトタイプなしでの UX 初期検証
### ✔ 3. 複数OEM向けHMIを同時展開（差分を仮想空間で管理）
### ✔ 4. Synthetic User と Varjo XR‑3 を組み合わせた“実視界評価”も可能
### ✔ 5. OTAアップデート可能な SDVアーキテクチャとの完全整合

特に Synthetic User との相性が良く：
- Multi-agent による **大量UXレビュー**
- 高齢者／初心者／注意散漫状態などの **仮想ドライバー再現**
- HMI異常系（誤操作・迷い）の自動検出
が可能になる。

---

## 8. 製品・研究の方向性：今後の展望
SOAFEE × Panasonic Unified HMI は今後次の方向に強化されるとみられる：

### ● **1. SDV向けクラウドHMIの完全仮想化開発環境**
- 仮想ECU × 仮想HMI × Synthetic User を完全クラウド化

### ● **2. XR（Varjo XR‑3）との融合**
- AR‑HUD／HUD／メータクラスタを仮想空間で完全再現

### ● **3. “Continuous UX Testing” の常態化**
- HMI更新ごとに Synthetic User が自動レビュー
- デプロイ前に UX リスクを自動検知

### ● **4. Automotive HMI の標準プロセス化**
- OEM／Tier1 間で共通仮想環境を使用
- ユーザー安全性の第三者検証が自動化

---

## 9. まとめ
Panasonic × SOAFEE Unified HMI は、
> **クラウド上に仮想コックピットを構築し、AI Synthetic User によるHMI評価を可能にした“SDV時代の中核技術”**
として位置づけられる。

特に：
- 仮想ディスプレイ（Remote VirtIO‑GPU）
- マルチOS対応のオープンHMIフレームワーク
- Synthetic User × Multi-agent UX 評価との強い親和性
- SDV（Software Defined Vehicle）における OTA開発プロセスとの整合

などにより、自動車UX開発は **“実車検証中心 → 仮想UX検証中心”** へ大きくシフトしつつある。

今後の自動車UX/HMI開発における最重要技術の1つといえる。

---

（※ 情報元：SOAFEE 2025 Blueprint “Unified HMI”, Panasonic Automotive 発表、Varjo ケーススタディ）

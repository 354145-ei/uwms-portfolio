# UWMS — Enterprise Workforce Management & Scheduling System

> 複雑な勤務条件・必要人数・休暇・勤務希望を考慮し、**勤務表の計画 → 候補生成 → 確認・修正 → 公開 → スタッフ本人の閲覧**までを一つの業務フローとして扱うワークフォース管理システムです。

UWMS（Unified Workforce Management System）は、シフト勤務を行う組織向けに個人開発しているWebアプリケーションです。

介護現場での実務経験を出発点にしていますが、介護専用の仕組みに固定せず、医療・小売・宿泊・製造など、さまざまなシフト型業務へ展開できるようにドメインを設計しています。

**応募向けポートフォリオとして、画面だけでなく、業務要件・設計判断・バックエンド検証・履歴管理まで説明できることを重視しています。**

▶ **[UWMS デモ動画を見る（YouTube）](https://youtu.be/cms7WxH145w)**

[ポートフォリオ画面](docs/index.html) · [設計上の判断](docs/engineering-decisions.md) · [システム構成](docs/architecture.md) · [デモシナリオ](demo/demo-scenario.md) · [English](README_EN.md)

---

## 採用担当者の方へ — 3分でわかる概要

| 項目 | 内容 |
| --- | --- |
| 開発形態 | 個人開発 / フルスタック |
| 対象 | シフト勤務を行う組織の勤務表作成・公開・閲覧 |
| 主な業務フロー | Setup → Planning → Candidate生成 → Review / Correction → Publication → My Schedule |
| バックエンド | Java 21 / Spring Boot 3 / REST API |
| フロントエンド | React / TypeScript / Vite |
| DB | PostgreSQL / Flyway |
| 最適化 | Timefold Solver |
| 認証・認可 | Keycloak / OIDC、テナント・施設スコープを考慮 |
| テスト | JUnit 5 / Mockito / Testcontainers / 結合テスト / ブラウザ受入確認 |
| 担当範囲 | 要件整理、ドメイン設計、DB設計、API、UI、テスト、受入確認、ドキュメント |

### このリポジトリについて

この `uwms-portfolio` は、応募時に安全に共有するための**ポートフォリオ専用リポジトリ**です。

開発用リポジトリをそのまま公開するのではなく、機密情報・ローカル設定・実データを含めない形で、以下を説明します。

- プロダクトの目的と業務フロー
- 実際に実装・確認した主要画面
- アーキテクチャ
- 重要な設計判断
- デモシナリオ
- スクリーンショット / デモ動画（公開前に匿名化・安全確認）

---

## なぜ作ったのか

勤務表作成は、単に「空いている職員」をシフトへ配置する作業ではありません。

実際には、次のような条件が同時に影響します。

- 必要人数
- 職種・資格
- 職員ごとの勤務条件
- 勤務可能曜日・祝日勤務可否
- 希望休・希望シフト
- 有給・欠勤
- 夜勤と翌日の「明」
- 連続勤務
- 週・期間単位の勤務日数や勤務時間
- 人員不足

UWMSでは、必要人数を満たせない場合でも、重要な制約を無理に緩和して不足を隠すことはしません。

**制約を守ったうえで不足を可視化し、最終判断を管理者に残す**ことを基本方針にしています。

---

## プロダクトの流れ

```text
組織・施設設定
      ↓
職員 / 職種 / 資格 / シフト設定
      ↓
必要人数設定
      ↓
勤務条件設定
      ↓
勤務希望・休暇
      ↓
作成前チェック
      ↓
勤務表候補の生成
      ↓
候補の確認・修正
      ↓
勤務表の公開
      ↓
スタッフ本人の My Schedule
```

生成結果をそのまま正式な勤務表にするのではなく、**Candidate（候補）と Publication（正式公開）を分離**し、人が確認・修正してから公開するライフサイクルを採用しています。

---

## 実装・紹介している主な領域

### 1. Workforce / 基本設定

- 組織・施設を前提とした管理
- Workforce Member（職員情報）の管理
- 職種・資格の管理
- 職員情報とログインIDを分離した設計
- Facility単位の運用・認可スコープ

### 2. Staffing Demand / 必要人数

必要人数は「必ずその人数にする値」ではなく、**最低限必要な人数**として扱います。

```text
必要人数 = 3

2名 → 1名不足
3名 → 充足
4名 → 有効な余剰
```

### 3. Scheduling Terms / 勤務条件

長期的な勤務条件と、特定の日付に対する勤務希望・休暇を分離して扱います。

例:

- 勤務可能曜日
- 祝日勤務可否
- 夜勤勤務可否
- 週単位の勤務日数・勤務時間
- 勤務時間上限

### 4. 勤務希望・休暇

- 希望休
- 希望シフト
- 有給
- 時間有給
- 欠勤

承認された内容は、その意味に応じて勤務表作成時の制約へ反映されます。

### 5. 夜勤・明け

夜勤は日付をまたぐ**1つの勤務**として扱います。

```text
10/01  夜勤
10/02  明
```

翌日の「明」は独立したShift Templateではなく、前日の夜勤から続く状態として扱います。

### 6. Candidate Generation / 勤務表候補の生成

必要人数、勤務条件、勤務希望、休暇などを基にTimefold Solverで勤務表候補を生成します。

重要な制約を壊して必要人数を埋めるのではなく、**HARD制約を守れる範囲で最善の候補を作り、残った不足を明示する**方針です。

### 7. Candidate Review / Correction

生成結果を確認し、人員不足や診断情報を見ながら管理者が最終調整を行います。

自動生成結果をブラックボックスのまま採用するのではなく、人が確認して決定できることを重視しています。

### 8. Publication / 公開

確認済みのCandidateを正式な勤務表として公開します。

公開後も単純に上書きするのではなく、履歴・改訂という考え方を持たせ、過去の正式状態を壊さない設計を重視しています。

### 9. My Schedule / スタッフ向け勤務表

スタッフ本人が、現在有効な公開済み勤務表を確認する画面です。

ポートフォリオでは、実際に受入確認した機能だけを紹介し、未確認の機能を「完成済み」として見せない方針です。

---

## 技術的に工夫した点

UWMSでは、単純なCRUDだけではなく、業務システムとして次の課題に取り組んでいます。

- Workforce MemberとログインIdentityを分離する
- UUIDの内部IDと人が扱う業務コードを分離する
- Staffing Demandを「最低必要人数」として扱う
- HARD制約を不足解消のために勝手に緩和しない
- 夜勤と翌日の「明」を1つの勤務として扱う
- CandidateとPublicationを別ライフサイクルとして扱う
- 公開済み勤務表や過去Candidateの履歴を保持する
- 重要な認可・勤務制約をバックエンドでも検証する
- 期間境界をまたぐ勤務条件を考慮する
- 現在の設定だけで過去の判断を無条件に再構築しない

詳細: [docs/engineering-decisions.md](docs/engineering-decisions.md)

---

## システム構成

```text
React / TypeScript / Vite
          │
          │ REST API
          ▼
Java 21 / Spring Boot 3
          │
          ├── Workforce
          ├── Planning
          ├── Scheduling Terms
          ├── Staffing Demand
          ├── Candidate
          ├── Publication
          ├── Authorization
          └── Timefold-based Optimization
          │
          ▼
PostgreSQL
          │
          └── Flyway

Authentication / Identity: Keycloak + OIDC
```

詳細: [docs/architecture.md](docs/architecture.md)

---

## 使用技術

### バックエンド
- Java 21
- Spring Boot 3
- Maven
- REST API / OpenAPI
- JPA / JDBC
- Timefold Solver

### データベース
- PostgreSQL
- Flyway
- Testcontainersを利用したDBテスト

### フロントエンド
- React
- TypeScript
- Vite
- レスポンシブWeb UI

### 認証・認可
- Keycloak
- OpenID Connect (OIDC)
- テナント / Facilityスコープを考慮した認可

### テスト・検証
- JUnit 5
- Mockito
- Testcontainers
- フロントエンド自動テスト
- 結合テスト
- ブラウザによる手動受入確認

---

## 開発担当範囲

個人開発として、次の工程を一貫して担当しています。

- 現場課題の整理
- 要件定義
- ドメイン設計
- データベース設計
- バックエンド実装
- REST API設計
- フロントエンド実装
- 勤務表作成ルール / 最適化条件の設計
- 認証・認可設計
- DBマイグレーション設計
- 自動テスト
- 手動受入確認
- UI / UX改善
- 技術ドキュメント作成

AI支援ツールも開発補助として利用していますが、業務要件、設計判断、受入条件、レビュー、最終確認は開発者自身が管理しています。

---

## ポートフォリオ公開準備状況

- [x] ポートフォリオ専用GitHubリポジトリ
- [x] 日本語README
- [x] 英語README
- [x] アーキテクチャ・設計判断の説明
- [x] ポートフォリオWebページの基礎
- [x] 管理者向け主要フローの動作確認
- [x] My Scheduleの動作確認
- [x] 架空データによる画面確認
- [ ] 掲載用スクリーンショットの最終選定
- [x] デモ動画の収録・YouTube掲載
- [ ] 公開前セキュリティ確認
- [ ] リポジトリ公開

公開前チェック: [SECURITY_REVIEW_CHECKLIST.md](SECURITY_REVIEW_CHECKLIST.md)

> 給与計算は現在の初期プロダクトスコープには含めていません。

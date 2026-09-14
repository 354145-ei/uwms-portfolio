# システム構成

このページでは、UWMSの構成を応募向けに簡潔に説明します。

詳細な開発環境、認証情報、ローカル設定などはポートフォリオには掲載しません。

---

## 全体構成

```text
┌────────────────────────────────────┐
│ React / TypeScript / Vite          │
│ 管理者・スタッフ向けWeb UI         │
└─────────────────┬──────────────────┘
                  │ REST API
                  ▼
┌────────────────────────────────────┐
│ Java 21 / Spring Boot 3            │
│                                    │
│ Workforce                          │
│ Planning                           │
│ Scheduling Terms                   │
│ Staffing Demand                    │
│ Candidate                          │
│ Publication                        │
│ Authorization                      │
│ Timefold-based Optimization        │
└─────────────────┬──────────────────┘
                  │
                  ▼
┌────────────────────────────────────┐
│ PostgreSQL                         │
│ Flywayによるスキーマ履歴管理       │
└────────────────────────────────────┘

Authentication / Identity
        └── Keycloak + OpenID Connect
```

---

## 勤務表作成フロー

```text
Facility
   ↓
Planning Workspace
   ↓
Staffing Demand + Workforce Scope
   ↓
Scheduling Terms
   ↓
Approved Requests / Leave
   ↓
Constraint Projection / Readiness
   ↓
Candidate Generation
   ↓
Candidate Review
   ↓
Human Correction
   ↓
Publication
   ↓
My Schedule
```

UWMSでは、自動生成結果をそのまま正式な勤務表にしません。

**Candidate（候補） → 管理者確認・修正 → Publication（正式公開）**というライフサイクルを分けることで、自動化と人の最終判断を両立させています。

---

## 主なアーキテクチャ上の考え方

### 1. テナントとFacilityを意識した境界

業務データはテナントを前提に扱い、Facilityは勤務表作成や運用上の重要な境界として扱います。

画面上で見えないようにするだけではなく、バックエンド側でも認可スコープを確認する設計を重視しています。

### 2. バックエンドを最終的な判定主体にする

重要な認可や勤務制約をフロントエンドだけに依存させません。

UIは操作性のために事前チェックを行えますが、正式な変更や公開時にはバックエンド側でも検証します。

### 3. 長期条件と一時的な希望を分離

職員の勤務可能曜日や夜勤可否などの長期的な条件と、特定日だけの希望休・希望シフト・休暇を分けて管理します。

これにより、恒常的な雇用・勤務条件と、一時的な申請を同じデータとして混在させないようにしています。

### 4. Staffing Demandを計画の出発点にする

先に「誰を入れるか」を決めるのではなく、どの日時・シフト・職種で最低何人必要かを定義し、その需要に対してCandidateを作成します。

### 5. 最適化と最終検証を分離

Timefold Solverは実現可能な勤務表候補の探索に利用します。

一方、Candidateの保存・修正・公開など重要なライフサイクル境界では、最適化処理だけに依存せず、業務上のHARD制約をバックエンドで再確認する考え方を採用しています。

### 6. 過去の勤務表を「現在の設定」だけで再構築しない

職員の設定は将来変更される可能性があります。

そのため、過去のCandidateやPublicationを現在の設定だけから無条件に再評価・再構築すると、当時の正式な状態と意味が変わる危険があります。

UWMSでは、勤務表作成時点の判断材料や公開履歴を保持することを重視しています。

### 7. 日付をまたぐ勤務を1つの業務単位として扱う

夜勤は翌日まで続く勤務です。

翌日の「明」を独立した別シフトとして扱うのではなく、前日の夜勤から続く状態として扱います。

これにより、夜勤回数・勤務日数・連続勤務などの意味が崩れないようにします。

---

## 技術スタックと役割

| 層 | 技術 | 主な役割 |
| --- | --- | --- |
| Web UI | React / TypeScript / Vite | 管理者・スタッフ向け画面 |
| API / Domain | Java 21 / Spring Boot 3 | 業務ロジック、認可、検証、REST API |
| Optimization | Timefold Solver | 勤務表候補の探索 |
| Database | PostgreSQL | 業務データ・履歴の保持 |
| Migration | Flyway | スキーマ変更履歴の管理 |
| Identity | Keycloak / OIDC | ログイン・認証基盤 |
| Test | JUnit 5 / Mockito / Testcontainers | 単体・結合・DBテスト |

---

## ポートフォリオ上の注意

この図は、採用担当者が短時間で理解できるように概念レベルへ簡略化しています。

以下は公開対象にしません。

- 認証情報・パスワード・トークン
- 実際の勤務先や個人情報
- ローカルDBダンプ
- 開発用の内部ハンドオフ資料
- ChatGPT / Codexの生ログ
- 公開に不要なローカルファイルパスや設定

英語版: [architecture_EN.md](architecture_EN.md)

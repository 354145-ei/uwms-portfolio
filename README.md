# UWMS — Enterprise Workforce Management & Scheduling System

> 複雑な勤務条件・必要人数・休暇・勤務希望を考慮し、勤務表の作成から確認・修正・公開までを支援するワークフォース管理システム。

UWMS（Unified Workforce Management System）は、シフト勤務を行う組織向けに個人開発しているWebベースのワークフォース管理・勤務表作成システムです。

介護現場での実務経験を主な出発点としていますが、介護専用にハードコードせず、医療・小売・宿泊・製造など複数のシフト型業務にも適用できる汎用的な設計を目指しています。

> **Portfolio status:** 継続開発中です。現在のPublic Portfolio Release 1.0は準備中で、実装済み・検証済みの機能と今後の開発項目を明確に分けて掲載します。

---

## なぜ作ったのか

勤務表の作成では、単に「空いている職員」をシフトへ配置するだけでは不十分です。

同時に考える必要がある例:

- 必要人数
- 職種 / Qualification
- 職員ごとの勤務条件
- 勤務可能曜日・祝日勤務可否
- 希望休・希望シフト
- 有給・欠勤
- 夜勤 / 明け
- 連続勤務
- 労働時間
- 人員不足

UWMSでは、必要人数を満たせないときにHARD制約を破って不足を隠すのではなく、制約を守ったうえで不足を可視化し、管理者を最終判断者として残すことを重視しています。

---

## 設計原則

- **Coverage before Schedule**
- **Policy before Decision**
- **Workspace before Publish**
- **Revision, Never Replace**
- **Explain Every Decision**
- **Best Feasible Planning**
- **Honest Scheduling**
- **Human Final Decision Maker**

---

## Manager Workflow

```text
Organization / Facility
        ↓
Workforce
        ↓
Profession / Qualification
        ↓
Shift Templates
        ↓
必要人数
        ↓
勤務条件
        ↓
勤務希望・休暇
        ↓
作成前チェック
        ↓
Candidate Generation
        ↓
Candidate Review / Correction
        ↓
Publish
```

---

## 主な実装領域

### Workforce / Setup
- Tenant / Organization / Facilityを前提とした管理
- Workforce Member管理
- Profession / Qualification
- Workforce MemberとLogin Identityの分離
- Facility単位の運用スコープ

### Staffing Demand
Coverageは「ぴったりの人数」ではなく**最低必要人数**として扱います。

```text
必要人数 = 3

2名 → 1名不足
3名 → 充足
4名 → 有効な余剰
```

### Scheduling Terms
長期的な勤務条件と、期間・日付ごとの勤務希望を分離します。

例:
- 勤務可能曜日
- 祝日勤務可否
- 夜勤勤務可否
- 勤務時間に関する条件

### 勤務希望・休暇
- 希望休
- 希望シフト
- 有給
- 時間有給
- 欠勤

承認済みの希望は、適用される意味に応じてScheduler Constraintへ反映します。

### Night / 明け
夜勤は日付をまたぐ1つの勤務として扱います。

```text
10/01  夜
10/02  明
```

`明`は独立したShift Templateではなく、前日の夜勤の継続 / reserved stateです。

### Candidate Generation
勤務条件・必要人数・休暇・勤務希望などを基にCandidateを生成します。

不足を隠すためにHARD制約を緩和するのではなく、Best Feasibleな結果と不足を可視化する方針です。

### Candidate Review
Candidateを勤務表として確認し、人員不足・診断情報を確認したうえで、管理者が修正・判断できる運用UIを構築しています。

### Publication
Candidateを正式な勤務表として公開します。公開履歴は単純上書きではなく、Revision / Publication lifecycleとして保持する設計です。

---

## Staff Experience — My Schedule

My Scheduleは現在、Portfolio Release 1.0に向けて仕上げ中です。

目標は、Staffが自分の**現在有効な公開済み勤務表**を分かりやすく確認できるstaff-first UIです。

完成後、このPortfolioでは次を実画面で紹介します。

- 月表示を中心としたMy Schedule
- 週表示
- 選択日の勤務詳細
- 夜 → 明のcontinuation表示
- 公休 / 有給 / 欠勤の区別
- 勤務希望・休暇へのentry point
- Staff向けutility / self-service導線

未完成の機能は、完成するまで実装済みとしては表示しません。

---

## Architecture

```text
React / TypeScript / Vite
          │
          │ REST
          ▼
Java 21 / Spring Boot 3
          │
          ├── Workforce
          ├── Planning
          ├── Scheduling Terms
          ├── Staffing Demand
          ├── Candidate
          ├── Publication
          └── Authorization
          │
          ▼
PostgreSQL
          │
          └── Flyway
```

詳細: [docs/architecture.md](docs/architecture.md)

---

## Tech Stack

### Backend
- Java 21
- Spring Boot 3
- Maven
- PostgreSQL
- JPA / JDBC
- Flyway
- REST
- OpenAPI / Swagger

### Frontend
- React
- TypeScript
- Vite
- Responsive Web / PWA-oriented UI

### Testing
- JUnit 5
- Mockito
- Testcontainers
- Frontend automated tests
- Integration tests
- Manual browser acceptance

---

## Engineering Decisions

CRUDだけでなく、次の設計課題にも取り組んでいます。

- Workforce MemberとLogin Identityを分離する理由
- UUIDとBusiness Codeを分離する理由
- Coverageをminimumとして扱う理由
- Published Scheduleを単純上書きしない理由
- Night D → 明 D+1をcross-date semanticsとして扱う理由
- HARD constraint違反で人員不足を隠さない理由

詳細: [docs/engineering-decisions.md](docs/engineering-decisions.md)

---

## Demo / Visual Showcase

Portfolio Release 1.0では、READMEだけではなく**実際のUIとutilityを短時間で理解できるデモ**を用意します。

予定:

1. Manager-side planning demo
2. Candidate Review / shortage visualization
3. Correction → Publication
4. Staff-side My Schedule demo（完成後）
5. Utility showcase
6. Architecture / engineering decisions

詳細: [demo/demo-scenario.md](demo/demo-scenario.md) / [docs/showcase-plan.md](docs/showcase-plan.md)

---

## 開発担当範囲

個人開発として、以下を一貫して担当しています。

- 業務課題整理
- 要件定義
- Domain設計
- Database設計
- Backend実装
- REST API設計
- Frontend実装
- Scheduling rule設計
- Authorization設計
- Migration設計
- Automated Test
- Manual Acceptance
- UI / UX設計
- Documentation

AI支援ツールも開発補助として利用していますが、業務要件、設計判断、Acceptance Criteria、レビューおよび最終検証は開発者が管理しています。

---

## Current Status / Roadmap

### 現在の主なFocus
- Manager向け setup → planning → candidate → correction → publish
- Candidate Review
- Workforce / Scheduling Terms
- 勤務希望・休暇
- Publication lifecycle
- **My Scheduleの仕上げ**

### Portfolio Release 1.0 Gate
- [x] GitHub staging repository
- [x] Japanese README foundation
- [ ] 5–7 anonymized screenshots
- [ ] Manager demo recording
- [ ] My Schedule completion
- [ ] Staff-side demo recording
- [ ] Utility showcase
- [ ] security review
- [ ] public release

Payrollは初期製品スコープには含めていません。

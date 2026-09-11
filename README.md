# UWMS — Enterprise Workforce Management & Scheduling System

> 複雑な勤務条件・必要人数・休暇・勤務希望を考慮し、勤務表の作成から確認・修正・公開、Staff自身の勤務表確認までを支援するワークフォース管理システム。

UWMS（Unified Workforce Management System）は、シフト勤務を行う組織向けに個人開発しているWebベースのワークフォース管理・勤務表作成システムです。

介護現場での実務経験を主な出発点としていますが、介護専用にハードコードせず、医療・小売・宿泊・製造など複数のシフト型業務にも適用できる汎用的な設計を目指しています。

> **Portfolio status:** Portfolio Release 1.0のshowcase対象が揃いました。現在は実画面Screenshot・demo capture・security reviewを準備しています。

[Portfolio Web Preview](docs/index.html) · [English](README_EN.md) · [Architecture](docs/architecture.md) · [Engineering Decisions](docs/engineering-decisions.md)

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

## End-to-End Workflow

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
        ↓
My Schedule
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

### Candidate Review / Correction
Candidateを勤務表として確認し、人員不足・診断情報を確認したうえで、管理者が修正・判断できる運用UIを構築しています。

### Publication
Candidateを正式な勤務表として公開します。公開履歴は単純上書きではなく、Revision / Publication lifecycleとして保持する設計です。

### Staff Experience — My Schedule
My ScheduleはPortfolio Release 1.0の正式なshowcase対象です。

Portfolioでは、現在の実装そのものをcaptureし、Staffが公開済み勤務表を確認する体験と、その画面から利用できるutilityを紹介します。README上で未検証のsub-featureを追加して見せることはせず、実画面を証拠として掲載します。

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

Showcase target:

1. Planning Workspace
2. 必要人数 / Scheduling Terms / 勤務希望・休暇
3. Generation Readiness
4. Candidate Generation
5. Candidate Review
6. 人員不足 / diagnostics
7. Correction → Publication
8. My Schedule
9. My Scheduleから利用できるcurrent utility

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

## Portfolio Release 1.0 Gate

- [x] GitHub staging repository
- [x] Japanese README
- [x] English README
- [x] Architecture / engineering story
- [x] Portfolio web page foundation
- [x] Manager-side showcase scope
- [x] My Schedule showcase scope
- [ ] 6–8 anonymized actual screenshots
- [ ] Automated / repeatable demo capture
- [ ] Short demo recording
- [ ] Utility showcase based on current build
- [ ] Security review
- [ ] Public release

Payrollは初期製品スコープには含めていません。

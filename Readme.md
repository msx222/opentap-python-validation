# README.md

[日本語READMEはこちら](README_ja.md)

# opentap-python-validation

OpenTAP and Python based validation toolkit for physical-input-driven embedded systems testing.

This repository explores how real-world hardware validation workflows can be represented as reusable OpenTAP test steps, Python instrument drivers, and AI-friendly test plans.

## Concept

Many hardware and embedded software tests are still performed manually:

- Set sensor inputs by hand
- Operate power supplies and instruments manually
- Check monitor tools visually
- Compare measured values with expected results
- Record results in spreadsheets

The goal of this project is to turn those manual operations into reusable test assets.

```text
Manual operation
↓
OpenTAP TestStep
↓
Reusable TestPlan
↓
Structured result
↓
Analysis / reporting
```

## Focus Areas

- OpenTAP plugin development with Python
- Instrument abstraction
- Physical input automation
- Virtual instruments
- Hardware/software validation
- Test result logging
- AI-friendly test plan generation

## Example Use Cases

### Physical Input Automation

Instead of exposing low-level commands such as resistance values or SCPI commands, test steps should use domain language.

```text
Bad:
SetResistance(10000)

Better:
SetOutdoorTemperatureSensor(25°C)
```

### Virtual Instrument

A monitor application, log file, or communication interface can be treated as a virtual measuring instrument.

```text
ReadCompressorFrequency()
ReadOperationMode()
ReadErrorCode()
```

### Judgment Step

Measurement and judgment should be separated into reusable steps.

```text
ReadFrequency
↓
AssertRange
↓
Pass / Fail
```

## Architecture

```text
OpenTAP TestPlan
  ↓
Validation TestSteps
  ↓
Python Instrument Abstraction
  ↓
Real / Virtual Instruments
  ↓
Hardware, Sensors, Fixtures, Monitor Tools
```

## Planned Components

- `drivers/`
  - Oscilloscope drivers
  - Power supply drivers
  - Sensor simulator drivers
  - Virtual board monitor drivers

- `steps/`
  - Measurement steps
  - Physical input steps
  - Judgment steps
  - Logging steps

- `examples/`
  - Sample OpenTAP test plans
  - YAML-based test definitions
  - Simulated validation workflows

- `docs/`
  - Architecture notes
  - Step design guidelines
  - Instrument abstraction policy

## Design Policy

This project does not aim to expose instrument commands directly to operators.

Instead, it aims to convert low-level operations into validation-oriented test steps.

```text
SCPI / device command
↓
Python driver
↓
Instrument capability
↓
Validation step
↓
Operator-friendly test plan
```

## Safety and Confidentiality

This repository is intended for general validation automation research.

It does not include:

- Confidential product information
- Internal test specifications
- Proprietary communication maps
- Company-specific evaluation conditions
- Non-public instrument documentation

All examples are generalized or simulated.

## Status

Early exploration phase.

The first target is to build a small OpenTAP + Python validation example using a virtual or simulated instrument.

## Long-Term Vision

To create a small but practical validation automation toolkit that connects:

```text
Physical testing
↓
OpenTAP automation
↓
Python extensibility
↓
Structured test results
↓
Power BI / analytics
↓
AI-assisted test planning
```

The broader goal is to make hardware and embedded software validation more reusable, explainable, and automation-ready.

---

# README_ja.md

# opentap-python-validation

OpenTAP と Python を用いた、
物理入力を伴う組込み機器評価のための
検証自動化環境を試作・検討するリポジトリです。

## 背景

製造業の評価現場では、現在でも多くの試験が
手作業で実施されています。

例えば、

- サーミスタ抵抗値を手動設定
- 計測器を手操作
- モニターツールを目視確認
- Excelへ結果転記
- 判定を人手で比較

などです。

Python による単発自動化は可能ですが、
属人化しやすく、
「その人しか使えないツール」
で終わるケースも多いと感じています。

そこで本リポジトリでは、
OpenTAP の TestStep 思想を利用し、

```text
手作業
↓
再利用可能な検証部品
```

へ変換することを目指しています。

## このリポジトリで扱うテーマ

- OpenTAP Python Plugin
- 計測器抽象化
- 仮想計測器
- 物理入力自動化
- 組込み機器評価
- ソフトウェア動作確認
- TestPlan構造化
- AI時代向け検証設計

## 想定するユースケース

### 物理入力の抽象化

単なる抵抗値指定ではなく、
現場で理解しやすい意味で入力を扱います。

```text
悪い例:
SetResistance(10000)

良い例:
外気温センサを25℃相当に設定
```

## 仮想計測器

モニターツールや通信ログを、
「状態観測用の計測器」として扱います。

```text
圧縮機周波数取得
運転モード取得
異常コード取得
```

## 判定Step

測定と判定を分離し、
再利用可能な判定部品として扱います。

```text
測定
↓
判定
↓
PASS / FAIL
```

## アーキテクチャ

```text
OpenTAP TestPlan
  ↓
Validation TestStep
  ↓
Python Instrument Driver
  ↓
実計測器 / 仮想計測器
  ↓
センサ / 評価ボード / モニターツール
```

## 今後の予定

- オシロスコープPlugin
- 電源制御Plugin
- サーミスタ入力シミュレータ
- 仮想モニターツール
- 判定Step
- YAMLベースTestPlan
- AIによるTestPlan生成検討

## 設計思想

本リポジトリでは、
SCPIコマンドや機器依存処理を
直接作業者へ見せることを目的としていません。

重要なのは、

```text
機器操作
↓
意味のある試験Step
```

へ変換することです。

例えば、

```text
VOLT 12
```

ではなく、

```text
定格電圧を印加
```

という現場言語で扱えるようにすることを目指します。

## 機密情報について

本リポジトリは、
一般化された検証自動化技術の研究用です。

以下は含みません。

- 社内機密情報
- 製品固有仕様
- 非公開通信仕様
- 実試験条件
- 社内専用ツール

サンプルコード・構成・データは
抽象化またはシミュレーションされたものです。

## 長期ビジョン

将来的には、

```text
物理試験
↓
OpenTAP自動化
↓
Python拡張
↓
構造化ログ
↓
Power BI分析
↓
AIによる試験生成
```

をつなぐ、
小規模でも実用的なValidation Platformを目指しています。


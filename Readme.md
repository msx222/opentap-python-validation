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


```

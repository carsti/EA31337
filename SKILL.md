---
name: mql5-ea31337-framework
description: Use when building, extending, or reviewing a sophisticated MQL4/MQL5 Expert Advisor that needs EA31337-style strategy composition, reusable framework classes, tester configuration, or portfolio-scale risk controls.
---

# MQL5 EA31337 Framework

- Start with `README.md` and `src/EA31337.mq5` to identify the entry point and supported modes.
- Read `src/include/ea.h` and `src/include/common/strategies-manager.h` when adding or coordinating strategies.
- Read the matching `src/include/common/{lite,rider,elite}/` inputs only after choosing a framework tier.
- Use `sets/optimize/` as a record of parameter organization, not pre-validated profitable settings.
- Read `docker/tests/` or `docker/backtest/README.md` only for repeatable compile or backtest automation.

Keep each strategy's signal generation, order lifecycle, and account risk state independently testable. Preserve unique magic-number and symbol/timeframe ownership, fail initialization explicitly when dependencies are unavailable, and introduce framework components incrementally.

Optimization and historical tests do not establish live performance. This project is GPL-licensed; preserve applicable license obligations when redistributing derivative code. Validate in Strategy Tester and on a demo account before live use.

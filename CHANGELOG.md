# Changelog

## [Unreleased]

## [0.2.0] - 2026-01-26

### Changed

- 新增--scheme-policy，适配多个场景，默认auto
- 新增--user-agent，可自定义UA，默认内置随机UA
- tls探测核心重构，支持全版本协议
- 检测逻辑优化

### Removed

- 移除dns解析重试逻辑
- 移除--use-scheme参数，使用--scheme-policy替代

---


## [0.1.1] - 2026-01-25

### Added

- 支持csp域名提取

### Changed

- 优化tls_domain提取逻辑
- 更精准的备案号提取
- 优化并发扫描的超时分配，支持浮点超时(如:0.5)
- 默认不再输出json文件，需通过-o参数指定

### Fixed

- 优化错误处理

- 解决检测器重复初始化问题

### Removed

---

## [0.1.0] - 2026-0-24

### Added

- 初始版本发布  

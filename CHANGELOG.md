# Changelog

## [Unreleased]

## [0.5.0] - 2026-02-13

### Added

- 核心重构，支持部分非http协议，如http/0.9、ssh等tcp协议
- 支持任意多重/无限重定向等畸形目标检测
- 新增支持非http协议字段: raw_response、protocol、protocol_version
- 支持带path的url目标: 如 `"http://192.168.1.1/admin"`
- 新增参数: `--path`、`--path-file`，支持自定义path请求路径
- 新增参数: `-F/--output-format`，支持输出格式流式: 流式JSONL、JSON、TSV、CSV
- 新增参数: `--select/--fields`，支持输出指定字段，方便管道流式适配其他工具执行后续操作

### Changed

- **BREAKING**: 原字段 `"redirect_url"` 已修改为 `"final_url"`。
- 重构输出系统，原有默认输出结果从数组改为JSONL，支持大任务流式输出，如需原有json数组可使用参数 ```-F json/--output-format json```
- 字段严格语义对齐，如scheme、host等
- 内部处理逻辑全阶段严格超时控制
- 性能优化
- 帮助信息美化: 动态渐变色系 + 关键信息聚焦，参数配置一目了然

---

## [0.4.2] - 2026-02-06

### Fixed

- 修复日志输出

### Added

- 新增单文件版本(内嵌资源文件)

### Changed

- 支持加载预编译规则库fp_rule.bin，免索引构建逻辑，启动更快，原fp_rule.json仍兼容支持

---

## [0.4.1] - 2026-02-05

### Fixed

- 修复日志输出

### Changed

- 代码逻辑优化

---

## [0.4.0] - 2026-02-03

### Added

- --tls/--tls-info 参数，允许用户选择是否主动探测 TLS 信息

### Changed

- **BREAKING**: 默认不再主动探测 TLS 信息，如需保持之前版本行为需显式使用 --tls/--tls-info 参数

---

## [0.3.0] - 2026-02-03

### Added

- -x/--proxy，支持通过代理请求
- --dns/--resovers，支持自定义dns服务器

### Changed

- **BREAKING**: 纠正 HTTP 头字段
  - 原字段 `"raw_header"` 已重命名为 `"header"`，并返回字典KV格式。
    原 `"raw_header"` 字段暂时移除(该语义字段获取实现需重构大量代码，下个版本可能提供)
- 优化协议检测错误回退逻辑
- 性能优化：优化字符串传递，进一步减少内存占用

---

## [0.2.1] - 2026-02-01

### Added

- 新增以下功能:
  --probe-methods/--pm，支持自定义请求方法
  --post-data/--pd，支持自定义post-data数据
  --post-file/--pf，支持从文件读取自定义post-data数据
  --content-type/--ct，支持指定content-type类型
- 优化数据文件读取，支持通过环境变量"HPROBE_DATA_ROOT"设置数据文件目录
- 支持管道传递目标:

  ```bash
  cat targets.txt | hprobe
  ```

- 支持被动检测:

  ```bash
  curl -s -i -k -L https://example.com | hprobe --mode passive --td --fp
  ```

- 结果中新增以下字段:
  1、method(请求方法)
  2、target(存储原始目标)
  3、resolved_ips(DNS解析结果)
  4、tls_probe_ip(tls探测ip)
  5、origin_ips(保留扩展后续会考虑接入域名反推真实IP引擎)

### Fixed

- 修复site_owner提取panic问题

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

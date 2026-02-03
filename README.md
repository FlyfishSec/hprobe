
<!--
# crates.io Notice

The Hprobe CLI is distributed as a precompiled binary.
The crate published on crates.io only serves as a name reservation
and metadata placeholder.
-->
<!-- 
# Hprobe 🚀 [![PyPI Downloads](https://static.pepy.tech/personalized-badge/hprobe?period=total&units=INTERNATIONAL_SYSTEM&left_color=BLACK&right_color=GREEN&left_text=downloads)](https://github.com/FlyfishSec/hprobe) -->

# Hprobe 🚀 [![Downloads](https://static.pepy.tech/personalized-badge/hprobe?units=INTERNATIONAL_SYSTEM&left_color=BLACK&right_color=GREEN&left_text=downloads)](https://github.com/FlyfishSec/hprobe) [![Issues](https://img.shields.io/github/downloads/flyfishSec/hprobe/total?label=issue&color=8A2BE2)](None)

A high-performance HTTP probing tool for asset discovery.

高性能 HTTP 探测工具，适用于大规模资产发现/网络空间测绘

---

![Hprobe Screenshot](assets/hprobe.png)

## Core Advantages 📌| 核心优势

1. **Tokio 异步运行时，极致高并发**
   - 基于 Tokio 异步运行时构建，充分利用多核性能，支撑大规模高并发探测

2. **纳秒级 ASN 查询**  
   - 自定义二进制结构体，采用零拷贝设计 + mmap 内存映射 + 二分查找，实现纳秒级 ASN 信息查询

3. **极速 Web 指纹识别**  
   - 集成 17000 + 指纹规则，进程内单例懒加载，10MB HTML 毫秒级指纹识别

## Quick Start⚡| 快速开始

```bash
C:\KVM\hprobe\hprobe.exe -t v9.service-access.cn --asn --td --fp
                        _
  /\  /\_ __  _ __ ___ | |__   ___
 / /_/ / '_ \| '__/ _ \| '_ \ / _ \
/ __  /| |_) | | | (_) | |_) |  __/
\/ /_/ | .__/|_|  \___/|_.__/ \___|
       |_|
                          hprobe v0.3.0
[16:09:35] [i] Wappalyzer technology detection enabled
[16:09:35] [i] Fingerprint detection enabled
[16:09:35] [i] ASN lookup enabled (range count: 460971)
[16:09:36] [i] Probe completed | Total targets: 1 | Valid results: 1 | Time elapsed: 0.837 seconds
[
  {
    "target": "v9.service-access.cn",
    "resolved_ips": [198.51.100.88, 198.51.100.89],
    "tls_probe_ip": 198.51.100.88,
    "host": "v9.service-access.cn",
    "scheme": "https",
    "url": "https://198.51.100.88:443",
    "port": 443,
    "method": GET,
    "status_code": 200,
    "title": "登录 - OCQ",
    "technologies": [
      "Alibaba Cloud CDN",
      "Backstretch",
      "Bootstrap:20180116",
      "Java",
      "Nginx:1.9.9",
      "Vue.js:2.6.12",
      "jQuery:1.10.2"
    ],
    "fingerprints": [
      "Bootstrap",
      "PHP",
      "企业版QQ",
      "登陆页面"
    ],
    "redirect_url": "https://auth.service-access.cn/login",
    "response_time_ms": 1632,
    "asn_info": {
      "as_number": 64532,
      "as_org": "Cloud Infrastructure Network",
      "as_country": "CN",
      "as_range": [
        "198.51.100.0/24"
      ]
    },
    "tls_info": {
      "cert_issuer": "C=US, O=DigiCert Inc, OU=www.digicert.com, CN=Encryption Everywhere DV TLS CA - G1",
      "cert_subject": "CN=portal.service-access.cn",
      "tls_version": "TLSv1.2",
      "tls_cipher": "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256",
      "cert_org": null,
      "cert_cn": null,
      "cert_san": [
        "portal.service-access.cn"
      ]
    },
    "header": {
      "server": "nginx/1.9.9",
      "date": "Sat, 24 Jan 2026 04:54:55 GMT",
      "content-type": "text/html;charset=utf-8",
      "transfer-encoding": "chunked",
      "connection": "keep-alive",
      "vary": "Accept-Encoding",
      "x-bucket-by": "********",
      "set-cookie": "JSESSIONID=********; Path=/; HttpOnly",
      "access-control-allow-origin": "*",
      "access-control-allow-methods": "PUT, GET, POST, OPTIONS, DELETE",
      "access-control-allow-headers": "DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization",
      "access-control-allow-credentials": "true"
    },
    "web_server": "nginx/1.9.9",
    "content_type": "text/html;charset=utf-8",
    "content_length": 46560,
    "tls_domain": "portal.service-access.cn",
    "icp_beian": "粤ICP备16xxxxxx号",
    "pubsec_beian": "粤公网安备13xxxxxx号",
    "identifier_code": "13xxxxxx",
    "contact_phone": 13599811120,
    "site_owner": "xx市人民政府办公室",
    "meta_domain": "portal.service-access.cn",
    "html_urls": [
      "beian.miit.gov.cn",
      "dlsw.baidu.com",
      "android.myapp.com",
      "itunes.apple.com",
      "o.alicdn.com",
      "w.x.baidu.com",
      "wpa.b.qq.com",
      "wpa.qq.com",
      "www.google.cn",
      "www.zensir.com"
    ]
  }
]
```

## Enjoy it! 🚀

Happy hacking with hprobe!

## Data Sources 📚 | 规则源

The following projects are used as rule sources:

- **WebAppAnalyzergo**  
  <https://github.com/projectdiscovery/wappalyzergo>

- **WebAppAnalyzer**  
  <https://github.com/enthec/webappanalyzer>

- **Wappalyzer (HTTPArchive)**  
  <https://github.com/HTTPArchive/wappalyzer>

- **FingerprintHub**  
<https://github.com/0x727/FingerprintHub>

- **EHole**  
 <https://github.com/EdgeSecurityTeam/EHole>

---

## License 📄 | 许可证

Hprobe is distributed as a binary only.

Copyright (c) 2026 FlyfishSec
All rights reserved.

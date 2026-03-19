<!-- 
# Hprobe 🚀 [![PyPI Downloads](https://static.pepy.tech/personalized-badge/hprobe?period=total&units=INTERNATIONAL_SYSTEM&left_color=BLACK&right_color=GREEN&left_text=downloads)](https://github.com/FlyfishSec/hprobe) -->

# Hprobe 🚀 ![](https://komarev.com/ghpvc/?username=FlyfishSec&base=4000&abbreviated=true&color=brightgreen) [![Downloads](https://static.pepy.tech/personalized-badge/hprobe?units=INTERNATIONAL_SYSTEM&left_color=BLACK&right_color=GREEN&left_text=downloads)](https://github.com/FlyfishSec/hprobe) [![Issues](https://img.shields.io/github/downloads/flyfishSec/hprobe/total?label=issues&color=8A2BE2)](../../)

A high-performance HTTP probing tool for asset discovery.

`hprobe` 是一个基于 Rust 实现的 高性能 HTTP 探测引擎，并且支持非HTTP协议识别，在大规模目标场景下能够高效完成web服务探测、TLS 信息解析以及应用指纹与技术栈识别，适用于资产发现、网络空间测绘与自动化安全评估。

---

![Hprobe Screenshot](assets/hprobe.png)

## Core Advantages 📌| 核心优势

1. **Tokio 异步运行时，极致高并发**
   - 基于 Tokio 异步运行时构建，充分利用多核性能，支撑大规模高并发探测

2. **纳秒级 ASN 查询**  
   - 自定义二进制结构体，采用零拷贝设计 + mmap 内存映射 + 二分查找，实现纳秒级 ASN 信息查询

3. **极速 Web 指纹识别**  
   - 集成 17000 + 指纹规则，进程内单例懒加载，10MB HTML 毫秒级指纹识别

## Usage Examples ⚙️ | 使用示例

### Example 1 — Full Feature Scan

```bash
C:\KVM\hprobe\hprobe.exe -t v9.service-access.cn --tls --asn --td --fp -F json
[16:09:35] [INFO] Wappalyzer technology detection enabled
[16:09:35] [INFO] Fingerprint detection enabled
[16:09:35] [INFO] ASN lookup enabled (range count: 460971)
[16:09:36] [INFO] Probe completed | Total targets: 1 | Valid results: 1 | Time elapsed: 0.837 seconds
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
    "technologies": ["Alibaba Cloud CDN", "Backstretch", "Bootstrap:20180116", "Java",
      "Nginx:1.9.9", "Vue.js:2.6.12", "jQuery:1.10.2"],
    "fingerprints": ["Bootstrap", "PHP", "企业版QQ", "登陆页面"],
    "final_url": "https://auth.service-access.cn/login",
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
    "html_urls": ["beian.miit.gov.cn", "dlsw.baidu.com", "android.myapp.com", "itunes.apple.com",
      "o.alicdn.com", "w.x.baidu.com", "wpa.b.qq.com", "wpa.qq.com", "www.google.cn", 
      "www.zensir.com"]
  }
]
```

### Example 2 — Read Targets from STDIN

```bash
C:\KVM\hprobe\>type target.txt | hprobe.exe --si
{"target":"192.168.1.149:80","host":"192.168.1.149","scheme":"http","url":"http://192.168.1.149:80/","port":80,"method":"GET","status_code":200,"title":"欢迎您使用OneinStack","final_url":"http://192.168.1.149/","response_time_ms":390,"header":{"connection":"keep-alive","date":"Thu, 12 Feb 2026 15:20:44 GMT","last-modified":"Wed, 20 Feb 2019 08:35:45 GMT","content-type":"text/html","server":"nginx","etag":"W/\"5c6d1161-423d\"","vary":"Accept-Encoding","transfer-encoding":"chunked"},"web_server":"nginx","content_type":"text/html","content_length":16957,"html_urls":["oneinstack.com","static.oneinstack.com","img.shields.io","linuxeye.com","filezilla-project.org","help.aliyun.com","paypal.me"]}
{"target":"192.168.1.86:6379","host":"192.168.1.86","port":6379,"final_url":"redis://192.168.1.86:6379","response_time_ms":1132,"content_length":1101,"protocol":"redis","response_text":"-DENIED Redis is running in protected mode because protected mode is enabled, no bind address was specified, no authentication password is requested to clients. In this mode connections are only accepted from the loopback interface. If you want to connect from external computers to Redis you may adopt one of the following solutions: 1) Just disable protected mode sending the command 'CONFIG SET protected-mode no' from the loopback interface by connecting to Redis from the same host the server is running, however MAKE SURE Redis is not publicly accessible from internet if you do so. Use CONFIG REWRITE to make this change permanent. 2) Alternatively you can just disable the protected mode by editing the Redis configuration file, and setting the protected mode option to 'no', and then restarting the server. 3) If you started the server manually just for testing, restart it with the '--protected-mode no' option. 4) Setup a bind address or an authentication password. NOTE: You only need to do one of the above things in order for the server to start accepting connections from the outside.\r\n"}
{"target":"192.168.1.102:22","host":"192.168.1.102","port":22,"final_url":"ssh://192.168.1.102:22","response_time_ms":1141,"content_length":43,"protocol":"ssh","response_text":"SSH-2.0-OpenSSH_9.6p1 Ubuntu-3ubuntu13.14\r\n"}
```

### Example 3 — Pipe output to gowitness

```bash
C:\KVM\hprobe\>hprobe -t example.com --si --select url|gowitness.exe scan file -f - --write-stdout
http://example.com:443/
2026/02/13 18:23:20 INFO result 🤖 target=http://example.com:443/ status-code=400 title="400 The plain HTTP request was sent to HTTPS port" have-screenshot=true
http://example.com:80/
2026/02/13 18:23:20 INFO result 🤖 target=http://example.com:80/ status-code=200 title="Example Domain" have-screenshot=true
```

### Example 4 — Pipe output to nuclei

```bash
C:\KVM\hprobe\>hprobe -t example.com --si --select url|nuclei
[INF] Your current nuclei-templates v10.2.2 are outdated. Latest is v10.3.8
[INF] cleaned up 113 orphaned template file(s)
[WRN] Found 2 templates with runtime error (use -validate flag for further examination)
[INF] Current nuclei version: v3.6.2 (outdated)
[INF] Current nuclei-templates version: v10.3.8 (latest)
[INF] New templates added in latest release: 457
[INF] Templates loaded for current scan: 9631
[INF] Executing 9629 signed templates from projectdiscovery/nuclei-templates
[WRN] Loading 2 unsigned templates for scan. Use with caution.
[INF] Targets loaded for current scan: 1
[INF] Templates clustered: 2208 (Reduced 2086 Requests)
[INF] Using Interactsh Server: oast.pro
[dns-waf-detect:cloudflare] [dns] [info] example.com
...
```

### Example 5 — Passive Mode (Pipe from curl)

```bash
C:\KVM\hprobe\>curl -s -i -k -L https://httpbin.org | hprobe --mode passive -F json
[
  {
    "target": "hprobe_passive.local",
    "host": "hprobe_passive.local",
    "url": "Hprobe-passive://raw-http-response",
    "port": 0,
    "status_code": 200,
    "title": "httpbin.org",
    "response_time_ms": 0,
    "header": {
      "connection": "keep-alive",
      "server": "gunicorn/19.9.0",
      "access-control-allow-credentials": "true",
      "content-length": "9593",
      "date": "Thu, 12 Feb 2026 15:26:29 GMT",
      "access-control-allow-origin": "*",
      "content-type": "text/html; charset=utf-8"
    },
    "web_server": "gunicorn/19.9.0",
    "content_type": "text/html; charset=utf-8",
    "content_length": 9593,
    "html_urls": [
      "github.com",
      "fonts.googleapis.com",
      "kennethreitz.org"
    ]
  }
]
```

More...

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

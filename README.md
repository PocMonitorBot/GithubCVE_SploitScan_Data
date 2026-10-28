# GithubCVE_SploitScan_Data

> GithubCVE_SploitScan 生产数据仓库 —— CVE PoC 仓库索引（repos/）+ CVE 情报融合（cves/）
>
> 数据由 [GithubCVE_SploitScan](https://github.com/PocMonitorBot/GithubCVE_SploitScan_Code)（私有源码）的 GitHub Actions 工作流自动更新。

## 仓库结构

```
GithubCVE_SploitScan_Data/
├── repos/                          # 引擎A输出：CVE → PoC 仓库列表
│   ├── {year}/{CVE-ID}.json       #   GitHub API 仓库对象数组 + tags + cve_ids
│   ├── {year}/{CVE-ID}.refs.json  #   外部参考链接（exploit-db/packetstorm/博客）
│   ├── {year}/README.md           #   年份索引（NVD 元数据）
│   ├── dateLog/{date}.json        #   每日新增/更新
│   └── kev.json / hot_cves.json / repo_blacklist.json ...
├── cves/                           # 引擎B输出：CVE 情报 fusion JSON
│   └── {year}/{Nxxx}/{CVE-ID}.json
├── compare/                        # 与原 Poc-Monitor-Data / SploitScanData 的一致性对比报告
└── 状态文件（.cvelist_state.json 等）
```

## 数据格式

详见源码仓库 [docs/OUTPUT-SCHEMA.md](https://github.com/PocMonitorBot/GithubCVE_SploitScan_Code/blob/main/docs/OUTPUT-SCHEMA.md)。

## 工作流

| Workflow | 频率 | 说明 |
|---|---|---|
| repo-monitor | 每小时 :13/:43 | GitHub PoC 仓库搜索入库 |
| repo-merge | 每 2 小时 :20 | PoC-in-GitHub + trickest/cve 上游合并 |
| intel-cvelist | 每小时 :00 | cvelistV5 新 CVE 情报管线 |
| intel-poc | 每 6 小时 :30 | PoC 源变化监控 |
| compare | 每日 03:00 UTC | 与原始两仓库一致性对比 |

## 迁移说明

本仓库于 2026-10-27 从 Poc-Monitor-Data（引擎A）与 SploitScanData（引擎B）bootstrap 合并而来，
初次导入经全量对比验证：**33 万文件 100% 内容一致（零差异）**，见 `compare/compare_report.json`。

## License

MIT

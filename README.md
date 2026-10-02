# SniperPVEZB — 僵尸噩梦

| 项 | 值 |
|---|---|
| GitHub 仓库 | **pvezb** |
| Package | `com.sniper.pvezb` |
| TWEAK_NAME | `SniperPVEZB` |
| 运行时配置 | `Documents/pvezb_config.json` |
| 日志 | `Documents/pvezb_tweak.log` |

## 上传文件清单（放在仓库根目录）

- `Makefile`
- `control`  ← ⚠️ 最容易传错的一个
- `SniperPVEZB.plist`
- `Tweak.xm`
- `.github/workflows/build.yml`
- （可选）`pvezb_config.example.json`、`README.md`

## ⚠️ 别再犯的对调事故（2026-10-02 真实踩坑）

曾经把 `PVE全球行动` 的 control（`Package: com.sniper.pvega`）传到 pvezb 仓库。
结果：deb 的 Package 变成 pvega，但里面装的还是 `SniperPVEZB.dylib`，
**包 ID 与代码不一致** → 症状混乱、难排查。

**上传前务必确认 `control` 第一行是：**

```
Package: com.sniper.pvezb
```

## 上传后怎么确认

Actions 日志里应有两步自检，必须全绿：

1. `Verify identity` → `✅ 身份自洽：Makefile / control / plist 三者匹配`
2. `Verify deb` → `✅ 产物自洽：Package=com.sniper.pvezb 与 dylib=SniperPVEZB.dylib 匹配`

任一步红字 = 文件传错了，**不要装产物**。

## 本地自检（上传前秒级验证，不用等 CI）

在 `DEB分类` 目录运行：

```
python check_before_upload.py
```

全绿再上传。

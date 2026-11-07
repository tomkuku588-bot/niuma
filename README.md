# NiuMa Pages

牛马脱敏器的 GitHub Pages 静态页面仓库，用于托管隐私协议和用户协议，供 HarmonyOS 应用市场上架审核使用。

## 应用信息

- 应用名称：牛马脱敏器（Niuma）
- 包名：com.xmgod.niuma
- 版本：1.0.0（versionCode 1000000）
- 平台：HarmonyOS（phone · tablet · 2in1）
- 应用源码仓库（Gitee）：git@gitee.com:kuku-harmonyos/niu-ma.git
- 上游开源项目：feiyuaq/niuma（MIT License，Copyright (c) 2026 feiyuaq）

## 关键合规事实

页面正文与下列实现事实一一对应，修改应用时需同步核对：

- `entry/src/main/module.json5` 未声明任何系统权限；应用完全离线运行。
- `oh-package.json5` 的 `dependencies` 为空对象，全工程无 HTTP/Socket/fetch 调用，不接入任何第三方 SDK、AI 或云端服务。
- 应用设置（薪资与作息、工作日与调休、加班倍率、发薪日、币符、心愿、语录、显示/主题/防窥）保存在沙箱 preferences（`niuma.cfg`）；桌面卡片使用沙箱文件 `settings.snapshot.json` 与 `widget-forms.json`；不上传、不云同步，也不保存每日收入流水。
- 备份导出/导入通过系统 `DocumentViewPicker` 选择 JSON 文件，明文保存，导入上限 1 MiB，保存位置由用户决定。
- 复制/分享时写入系统剪贴板，仅在用户主动点击后发生。
- 桌面卡片默认隐藏金额，可在设置中开启显示；卡片扩展仅读取本地快照。

## 页面与正本

- `docs/index.html`：GitHub Pages 首页，中文 / English 切换，隐私协议 / 用户协议切换。
- `privacy-policy.md`：中文隐私政策。
- `privacy-policy-en.md`：English privacy policy.
- `terms-of-service.md`：中文用户协议。
- `terms-of-service-en.md`：English terms of service.

四份 Markdown 是协议正本，`docs/index.html` 内的四个正文块（zh/en × privacy/terms）与之一一对应（隐私政策 9 节、用户协议 10 节）。页面不是自动生成物：改正文必须同步改两边。

## 部署说明

仓库已配置 `.github/workflows/pages.yml`，推送到 `main` 分支后自动部署 `docs/` 目录；工作流中的 `configure-pages` 带 `enablement: true`，首次运行会自动启用 GitHub Pages。

公开入口：

- 协议中心首页：https://tomkuku588-bot.github.io/niuma/
- 隐私协议直达：https://tomkuku588-bot.github.io/niuma/?doc=privacy
- 用户协议直达：https://tomkuku588-bot.github.io/niuma/?doc=terms
- 英文版直达：在以上地址追加 `&lang=en`

AGC 提审时「隐私政策 URL」填写隐私政策直达地址。

## 包名一致性核对

当前应用工程 `AppScope/app.json5` 中的 `bundleName` 仍是占位的 `com.example.niuma`，本仓库协议页与 README 已按正式包名 `com.xmgod.niuma` 书写。上架前必须把应用包名改为 `com.xmgod.niuma`，并重新核对页面正文与应用内展示，避免审核时主体信息不一致。

## 已知风险

协议页托管在境外 GitHub Pages（`tomkuku588-bot.github.io`），不是已备案域名。如审核要求备案域名，需要另行迁移并更新 AGC 中的隐私政策 URL。

## 关联远程

```
git remote add origin git@github.com:tomkuku588-bot/niuma.git
git push -u origin main
```

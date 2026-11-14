# 页屿手环端（band 分支）

对应设备：小米手环9

基于 [youshen2/com.bandbbs.ebook（弦电子书）](https://github.com/youshen2/com.bandbbs.ebook) 改造的
非官方二次开发版本，配合手机端「页屿」（Yeyu Reader，`com.yeyu.reader`）传书使用。开发者 **hrk_**。

## 来源声明（这是什么改的）

上游为 moye 弦电子书（AGPL-3.0，作者 youshen2）的 VelaOS 快应用。本分支在其基础上修改：

| 项 | 上游 | 本分支 |
| --- | --- | --- |
| 包名 | `com.bandbbs.ebook` 系 | `com.yeyu.reader`（小米穿戴 SDK 硬约束：与手机端 APK **同包名 + 同签名**，否则 `launchWearApp` 直接失败） |
| 应用名 / 图标 | 弦电子书 | 「页屿」、圆形图标 |
| `/pages/push` 接收页 | 弦电子书协议 | 对接页屿手机端协议：`__hs__` 三段握手、10KB 分片流控、文件命令集、阅读进度 / 时长双向同步 |
| 布局 | — | 按 小米手环9 屏幕适配（`designWidth = 192`；装错型号能装上但界面会错位） |
| 阅读器功能 | 滑动/分页阅读、书签、定时翻页、分类、阅读时长等 | 沿用上游，未删改 |

协议全文见 [yeyu-reader/band_protocol/PROTOCOL.md](https://github.com/hrk666666/yeyu-reader/tree/main/band_protocol)。

## 许可

**AGPL-3.0**（继承上游，本分支 `LICENSE` 为全文），版权归 youshen2 及各贡献者，修改部分归 hrk_。

- 对外分发本分支（含编译出的 `.rpk`）时，**必须一并提供本分支源码与修改说明**，并以 AGPL-3.0 授权。
- 手机端主体基于 fqapp（GPL-3.0）开发，按 GPL-3.0 第 13 条并入 AGPL-3.0 作品后，**双端统一以下兼容的 AGPL-3.0 提供**。

## 非从属关系声明

本项目与小米 / 华米（Xiaomi、REDMI、VelaOS、小米手环、REDMI Watch、小米手表、小米运动健康等
名称与商标归各自所有者）、弦电子书作者 youshen2、fqapp 原作者 ch6vip 均**无任何隶属、授权、
合作或背书关系**。提及第三方名称仅用于说明技术来源与兼容对象；上游对本项目不承担任何责任。

## 免责声明

- 仅供**个人学习与技术研究**使用；不得商用或二次分发侵权内容。
- 安装第三方 rpk / 修改版客户端存在设备稳定性与账号风险，**后果由使用者自行承担**。
- 按「现状」提供，不附带任何明示或默示担保。

## 构建

```bash
# AIoT IDE 或 aiot-cli（VelaOS 快应用）
npx aiot release --enable-custom-component --enable-jsc
```

签名使用 `sign/release/` 下与手机端**同源**的证书（由手机端 keystore 导出，**勿重新生成**，
换签名即无法与手机通信）。各机型分支仅 `designWidth` 与机型适配不同，不要混用。

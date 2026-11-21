# 昔涟 · 拾光（dsh-cyrene-aurora）

粉白毛玻璃主题 + 开机开屏动画，给 DeepSeek Harness 换一套昔涟的浅色观感。

非官方同人作品，与 miHoYo / HoYoverse、DeepSeek 均无隶属或背书关系。

---

## 安装

### 方式一：从仓库直接装（推荐）

DSH 侧边栏「插件」页 → 右上角「安装插件」→ 输入框填：

```text
https://github.com/whr0115/dsh-cyrene-aurora
```

点「安装」，装完启用，**彻底关掉 DSH**（最近任务划掉）再重开。

装的是默认分支当前内容，不经过 npm，也不需要构建。仓库必须是 public。

国内备选地址：

```text
https://gitee.com/wwhhrr0115/dsh-cyrene-aurora
```

### 方式二：从本地目录安装

把 `dsh-cyrene-aurora/` 放到任意位置，在目标 profile 的 `package.json` 加：

```json
{
  "dependencies": {
    "dsh-cyrene-aurora": "file:/绝对路径/dsh-cyrene-aurora"
  },
  "dsh": {
    "profile": {
      "bundles": ["……其它 bundle……", "dsh-cyrene-aurora"]
    }
  }
}
```

然后跑 `pnpm install`，重开 DSH。

### 卸载 / 只关开屏

- 插件页关掉或卸载 `dsh-cyrene-aurora`
- 只关开屏：设置 →「昔涟 · 主题」→「开屏动画」→ 关掉「启动时播放」
- 与 `dsh-cyrene-theme` 争同一组界面槽位，两者不要同时启用

---

## 功能

### 界面

- 粉白渐变毛玻璃 UI、对话框与面板样式
- 侧边栏「✦ 昔涟」人格设定：写下的口吻在每次新对话时沿用
- 表情包（11 张）与自定义上传
- 长期记忆、世界书
- 新会话欢迎页形象与欢迎语、输入框占位提示

### 壁纸

`Background/` 默认留空，界面是粉白渐变底，不铺整页大图。要铺自己的图，把图片（png / jpg / jpeg / gif / webp / avif）放进 `Background/`，在设置页「背景图管理」里切换、开轮换、调色纱浓度。

### 对话区线稿水印

消息区底部一层很淡的角色线稿，浅色 / 深色各一张，默认开启、水平居中。设置里可关或改成「贴右」。

### 开机开屏动画

启动时播一次：角色线稿 + 流转的极光 + 一道掠光 + 一句问候。

- 时长 1–5 秒、立绘高度 240–720px、底色白 / 粉，全在设置里调
- 点画面或按 `Esc` / `Enter` / 空格可跳过
- `prefers-reduced-motion` 开启时自动不播
- 地址栏加 `?cyrene=splash` 可强制播放一次

开屏与主题分开开关，关掉开屏界面仍是原来的样子。

---

## 设置在哪

**设置 → 昔涟 · 主题**（侧边栏底部「✦ 昔涟」打开同一个编辑器）：

- 人格、主题、表情包的启用与关闭
- 人格正文编辑与保存（改完对新对话立即生效）
- 表情包管理、背景图管理、对话线稿水印、长期记忆、世界书
- ✦ 开屏动画：开关、时长、立绘大小、底色切换、预览一次

---

## 更新

查看最新版本：<https://github.com/whr0115/dsh-cyrene-aurora/releases/latest>

```sh
dsh plugin --profile web remove dsh-cyrene-aurora
dsh plugin --profile web add https://github.com/whr0115/dsh-cyrene-aurora
```

然后彻底重启 DSH。更新不会清除本机主题设置与记忆。

---

## 常见问题

- **装完没反应**：只按返回键不算关掉，最近任务里把 DSH 划掉再打开
- **界面冲突**：确认 `dsh-cyrene-theme` 不在 profile 的 bundles 里
- **连不上仓库**：先确认能打开仓库页面，公司网络或代理可能拦截 git

---

## 隐私

- 插件本身不含账号、API Key 或聊天记录
- 人格、壁纸选择、记忆、世界书、开屏设置保存在本机，不随仓库分发、不上传
- 世界书正文仅在手动抓取时联网，之后离线使用

## 许可与来源

主题与开屏的原始设计分别来自 `dsh-cyrene-theme`（MIT，作者 berhbro）与 `dsh-theme-cyrene`（MIT，Cyrene Impressions contributors）。本包整合两者，保留原 MIT 许可，详见 `LICENSE` 与 `THIRD-PARTY-NOTICES.md`。

整合与维护：whr0115。《崩坏：星穹铁道》相关素材权利归米哈游所有。

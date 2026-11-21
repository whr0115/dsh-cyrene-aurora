# 昔涟 · 拾光（dsh-cyrene-aurora）

> 粉白毛玻璃主题 + 开机开屏动画。给每一次启动，留一点光。

这是把两个昔涟主题**整合成一个**的结果：

| 来源 | 拿过来的部分 |
| --- | --- |
| `dsh-cyrene-theme` 0.4.1（原本启用着的那个） | 全部：壁纸轮换、人格设定与引导词、表情包、长期记忆、世界书、欢迎页形象、聊天占位提示……**一行没改** |
| `dsh-theme-cyrene` 0.37.0（原本装着但没启用的「昔涟印象」） | 它的**开机开屏动画**：角色线稿 + 极光 + 光斑 + 一句话问候，可跳过 |

所以这个包 = 你原来那套主题（原样） + 开场那几秒。

> 非官方同人作品，与 miHoYo / HoYoverse、DeepSeek 均无隶属或背书关系。
> 代码与素材来源、版权行见 [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md)。

---

## 安装

### 方式一：从 DSH 插件页直接装 GitHub 仓库（推荐）

1. 打开 DSH 侧边栏的「**插件**」页；
2. 点右上角「**安装插件**」；
3. 在输入框里填仓库地址：

   ```text
   https://github.com/whr0115/dsh-cyrene-aurora
   ```

4. 点「安装」，装完启用；
5. **彻底关掉 DSH**（后台也清掉）再重新打开。

装的是仓库**默认分支的当前内容**，不经过 npm，也不需要构建：本包没有 `prepare`
脚本，pnpm 不会要求你批准构建脚本。

如果插件页不接受 URL，可以在 DSH 终端里用等价命令：

```sh
dsh plugin --profile web add https://github.com/whr0115/dsh-cyrene-aurora
# 或
dsh plugin --profile web add github:whr0115/dsh-cyrene-aurora
```

仓库必须是 **public**；私有仓库需要本机已配置可用的 Git 凭据。

### 方式二：从本地目录安装（开发 / 改代码）

1. 把整个 `dsh-cyrene-aurora/` 目录复制到目标机器任意位置（例如 `~/.dsh/local-plugins/dsh-cyrene-aurora`）；
2. 在目标 profile 的 `package.json` 里给它加一条 `file:` 依赖，并把它列进 `dsh.profile.bundles`：

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

3. 在 profile 目录跑一次 `pnpm install`（本地 `file:` 依赖不需要网络）；
4. 重开 DSH。

### 卸载 / 回退

- 在「插件」页关掉或卸载 `dsh-cyrene-aurora`；
- 只想关开屏：设置 →「昔涟 · 主题」→「开屏动画」→ 关掉「启动时播放」；
- 回退到旧主题：把 profile `dsh.profile.bundles` 里的 `dsh-cyrene-aurora` 换回 `dsh-cyrene-theme`（如果还留着）。

### 常见问题

- **装完没反应**：只按返回键不算关掉。进最近任务列表把 DSH 划掉，再重新打开。
- **和旧主题抢界面**：`dsh-cyrene-theme` 与本插件会争同一组槽位，确认它不在 profile 的 `bundles` 里。
- **GitHub 连不上**：先确认手机能打开仓库页面；公司网络或代理可能拦 `git`。

---

## 它做了什么

### 1. 原来那套，一样不少

- 粉白渐变毛玻璃 UI、对话框与面板样式；
- 整页背景图（`Background/` 目录，可轮换、可压暗）——**默认不铺**：
  `Background/` 现在留空，界面就是粉白渐变底；想铺图把图丢进去即可；
- 侧边栏「✦ 昔涟」人格设定：写什么，之后每次新对话都会照这段口吻回答；
- 表情包（11 张）与自定义上传；
- 长期记忆（`cyrene_memory_add` / `cyrene_memory_search`）；
- 世界书（`cyrene_worldbook_search`，正文从官方 wiki 抓一次后离线用）；
- 新会话欢迎页的形象与欢迎语、输入框占位提示。

**这些都是从现役主题复制过来的，没有重写、没有改外观。** 状态文件也沿用同一个
（`$DSH_HOME/cyrene-theme.json`），所以你之前改过的人格、壁纸选择、记忆都还在。

### 关于壁纸：默认不铺整页大图

2026-11-09 起这一版**不再随包带壁纸**：原来那 6 张 1080×1920 的竖版图已经移到
`~/.dsh/cyrene-wallpaper-backup/moved-out/`（想恢复就把它们丢回 `Background/`，插件会重新扫出来）。
不铺图时界面回到粉白渐变底——既是原主题的默认观感，也省下磁盘与解码内存。

要自己的图：直接把图片放进 `Background/`（支持 png / jpg / jpeg / gif / webp / avif），
设置页「背景图管理」里可以切「背景图 / 简约（无图）」、选当前那张、开轮换、调色纱浓度。

### 对话区线稿水印（也从「昔涟印象」整合）

消息区底部那层很淡的角色线稿——就是你截图里那种「背景」：

- 画在 `[data-conversation-content]` 上（消息区的常驻容器，不跟着滚动走），水印钉在底部，消息从上面滚过去；
- **浅色 / 深色各一张**（`chat-art-light.svg` / `chat-art-dark.svg`）：矢量图没法跟着 CSS 变量换色，所以两张分别是调好的；
- 四边渐隐做在图自己的蒙版里，没有矩形硬边；默认让出底部 160px 给输入框那层；
- 默认开、水平居中；设置页里可以关掉，或改成「贴右」；
- 关掉它不影响其它任何东西。

### 2. 新加的开屏动画

- 启动时播一次：角色线稿 + 流转的极光 + 一道掠光 + 一句问候；
- 时长 **1–5 秒**、立绘高度 **240–720px**、底色白 / 粉，全在设置里调；
- 五句问候用「洗牌袋」轮换，十次开屏里每句正好两次，不会连着两次撞同一句；
- 点画面、按 `Esc` / `Enter` / 空格都能跳过；
- 同一会话里刷新不会重播（换插件版本会再播一次）；
- `prefers-reduced-motion` 开着时自动不播；
- 地址栏加 `?cyrene=splash` 可强制播一次。

开屏**和主题分开开关**：不想要开场，关掉它，界面还是原来的样子。

### 3. 连外壳的启动画面也接住了

页面脚本起来之前，外壳会先画一屏自己的「Loading plugins…」。宿主半通过
`webserver/index-inject` 往 index.html 里提前放一帧同色封面（角色 + 底色），
客户端半一加载就接管它、接着放开场动画——所以不会先闪一下原版界面。
封面自带两道保险：客户端出现后 600ms 撤走、最多 9 秒必撤，永远不会把应用锁在外面。

---

## 设置在哪

**设置 → 昔涟 · 主题**（侧边栏底部「✦ 昔涟」打开的是同一个编辑器）：

- 启用/关闭人格、主题、表情包；
- 人格正文编辑与保存（改完立刻对新对话生效，不必重载）；
- 表情包管理、背景图管理、**对话线稿水印**、长期记忆、世界书；
- **✦ 开屏动画**：启动时播放（开关）、时长滑杆、立绘滑杆、底色切换、预览一次。

开屏的「开关 / 时长 / 底色 / 大小」是跟着状态文件走的（`splash` 字段）。
其中**开机封面那一帧**是在宿主启动时按落盘状态生成的，所以改完这些值后，
新的一帧封面要等下次启动才对得上——开屏动画本身不用等。

---

## 目录结构

```text
dsh-cyrene-aurora/
├─ lib/
│  ├─ index.js       宿主半：人格 section、HTTP 路由（/cyrene/*）、记忆/世界书/表情包/背景/开屏
│  ├─ client.js      客户端半：样式表、设置页、表情包与背景管理、开屏动画
│  └─ worldbook.js   世界书索引/检索
├─ Background/       壁纸目录（默认空：不铺图就是粉白渐变底）
├─ meme/             表情包（11 张）
├─ locale/           插件页显示用的标题与简介（zh / en）
├─ icon.svg          插件页图标
├─ splash-art.svg    开屏立绘（1160×868 挖空线稿，矢量）
├─ chat-art-light.svg / chat-art-dark.svg   对话区线稿水印（浅底 / 深底各一张）
├─ stickers.json     表情包清单
├─ cordis.patch.yml  bundle 声明（插一个 id=ui-cyrene-aurora 的行）
├─ test/             自检（node test/client.smoke.mjs / host.smoke.mjs）
└─ package.json
```

## 自检

```bash
node test/client.smoke.mjs   # 客户端半：bundle 包装、样式作用域、槽位、编辑器写入姿势
node test/host.smoke.mjs     # 宿主半：section、GET/POST 信封、落盘、路由、脏值夹取
```

两份都全绿（192 / 156 项）。它们不启动浏览器、不碰真实 `~/.dsh`，全在临时目录里跑。

## 隐私与数据

- 插件本身**不含账号、API Key 或聊天记录**；
- 运行数据（人格、壁纸选择、记忆、世界书、开屏设置）保存在本机 `$DSH_HOME`，
  不会随仓库分发，也不会上传；
- 世界书正文只在你点按钮抓取时联网，之后离线使用。

## 更新

从 Git 安装的副本不会自动跟随某个版本号。要更新：

```sh
dsh plugin --profile web remove dsh-cyrene-aurora
dsh plugin --profile web add https://github.com/whr0115/dsh-cyrene-aurora
```

然后彻底重启 DSH。更新不会清掉 `$DSH_HOME` 里的主题设置与记忆。

## 权利与来源

- 主题与开屏的原始设计分别来自 `dsh-cyrene-theme`（MIT，作者 berhbro）与
  「昔涟印象」`dsh-theme-cyrene`（MIT，Cyrene Impressions contributors）。本包是两者的整合，
  保留原 MIT 许可（见 `LICENSE` 与 `THIRD-PARTY-NOTICES.md`）。
- 整合、插件元数据补全与后续维护：whr0115。
- 非官方同人作品：与 miHoYo / HoYoverse、DeepSeek 均无隶属或背书关系；
  《崩坏：星穹铁道》素材权利归米哈游所有。

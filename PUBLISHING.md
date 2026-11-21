# 发布与上传说明

这个目录已经是一个**提交好的本地 Git 仓库**（`main` 分支，带 `v1.0.0` 标签）。
按下面的步骤把它放到 GitHub，之后就能在 DSH 插件页里用仓库地址安装。

## 1. 在 GitHub 建空仓库

1. 打开 <https://github.com/new>；
2. Repository name 填 `dsh-cyrene-aurora`；
3. 选 **Public**（私有仓库需要本机 Git 凭据才能装）；
4. **不要**勾选 “Add a README file”“Add .gitignore”“Choose a license”——本地已经有；
5. 点 Create repository。

## 2. 推送

在 `dsh-cyrene-aurora/` 目录里执行（把用户名换成你的）：

```sh
git remote add origin https://github.com/whr0115/dsh-cyrene-aurora.git
git branch -M main
git push -u origin main
git push origin v1.0.0
```

如果提示要登录，用 GitHub 的 **Personal Access Token** 当密码
（Fine-grained token，只给这一个仓库的 Contents: Read and write 就够）。

> 也可以用网页上传 `dsh-cyrene-aurora-v1.0.0.zip` 解压后的内容，但那样**不带 Git 历史与
> `v1.0.0` 标签**。想保留历史，用上面的 `git push`，或把 `.bundle` 克隆出来再推。

## 3. 在 DSH 里安装

侧边栏「插件」→「安装插件」，填：

```text
https://github.com/whr0115/dsh-cyrene-aurora
```

安装后启用，并彻底重启 DSH。

> 这台设备上已经用 `file:` 装过同一个包名的副本。要在当前设备验证 GitHub 安装，
> 先在「插件」页移除 `dsh-cyrene-aurora`，否则会提示 already-installed。
> 移除不会删除 `$DSH_HOME` 里的主题设置、记忆与世界书。

## 4. 以后更新

改完代码后：

```sh
git add -A
git commit -m "描述这次改了什么"
git tag v1.0.1
git push origin main --tags
```

DSH 里从 Git 安装的副本不会自动更新，需要先移除再重新安装（不会丢 `$DSH_HOME` 里的设置）。

## 可选：发布到 npm

不发布也能装。如果以后想用 `dsh plugin add dsh-cyrene-aurora` 这种包名安装，
需要先确认 npm 上的包名没被占用，再 `npm publish`。当前仓库的 `package.json`
已经带好 `files`、`exports`、`repository`、`license` 等字段，可以直接打包：

```sh
npm pack --dry-run   # 先看会打包哪些文件
```

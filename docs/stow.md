# GNU Stow 常用命令

> 用“包目录（package）”管理 dotfiles：把仓库里的文件/目录以软链接方式部署到目标目录（通常是 `~`）。

## 基本用法

在 stow 目录（默认当前目录）执行：

- 预演（不改动）：`stow -n -v -t ~ <PACKAGE...>`
- 生效：`stow -v -t ~ <PACKAGE...>`
- 删除（取消链接）：`stow -D -v -t ~ <PACKAGE...>`
- 重新链接（等价于先删除再生效）：`stow -R -v -t ~ <PACKAGE...>`

常用选项：

- 指定 stow 目录：`-d <DIR>` / `--dir=<DIR>`
- 指定目标目录：`-t <DIR>` / `--target=<DIR>`
- 忽略文件：`--ignore='<REGEX>'`
- 处理包之间的链接冲突：`--defer='<REGEX>'` / `--override='<REGEX>'`
- 导入目标目录已有文件到包内：`--adopt`（高风险，务必先 `-n` 预演）

## 示例

### 本仓库（`agents/`）

在仓库根目录执行：

- 预演：`stow -n -v -t ~ agents`
- 生效：`stow -v -t ~ agents`
- 取消：`stow -D -v -t ~ agents`

### 推荐的 dotfiles 布局（示例）

```text
dotfiles/
  zsh/
    .zshrc
  tmux/
    .tmux.conf
```

然后在 `dotfiles/` 下执行：`stow -n -v -t ~ zsh tmux`

## 小提示

- 遇到“目标文件已存在/冲突”，优先手动清理或移动旧文件，再 stow；确实需要再考虑 `--adopt`。
- 建议统一使用 `-n -v` 先预演再执行。

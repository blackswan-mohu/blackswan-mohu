# 让 3D 贡献图统计「私有库」贡献

默认的 `GITHUB_TOKEN` 只能看到**公开**贡献，所以 3D 图里的数字会偏小
（例如只有 ~60，而你自己登录看到的热力图密密麻麻）。要把私有库也算进来，
需要下面**两步手动操作**（涉及你的账号权限，我无法代劳）：

## 步骤 1 · 开启「私有贡献可见」

GitHub 右上角头像 → **Settings** → **Public profile** →
**Contributions & Activity** → 勾选
**"Include private contributions on my profile"**。

> ⚠️ 这会让任何访客都能在你主页看到你的私有贡献「数量/热力」，
> 但**不会**泄露具体仓库名、内容或代码。

## 步骤 2 · 配一个 Personal Access Token（PAT）

1. **Settings** → **Developer settings** →
   **Personal access tokens** → **Tokens (classic)** → **Generate new token (classic)**
2. 勾选权限：`read:user`（含私有活动统计）；如需更细的私有仓库活动，再加 `repo`
3. 生成后复制该 token（只显示一次）
4. 回到本仓库：**Settings** → **Secrets and variables** → **Actions** →
   **New repository secret**
   - Name：`PROFILE_TOKEN`
   - Secret：粘贴刚才的 token

## 步骤 3 · 重新生成

进入本仓库 **Actions** → 选中 *GitHub Profile 3D Contrib* → **Run workflow**，
或随便推一次 commit。workflow 已配置为**优先使用 `PROFILE_TOKEN`**，
配好后即会把私有贡献一并统计进 3D 图。

（workflow 里的 token 行：`secrets.PROFILE_TOKEN || secrets.GITHUB_TOKEN`，
未配置时自动回退到仅公开贡献，不会报错。）

## 前提条件

- 你已经 fork 了一个 GitHub 仓库。
- 你在 fork 的仓库中做了一些修改。
- 你希望同步源仓库的新提交，但不覆盖自己的修改。
- 主分支假设为 `main`（如果是 `master`，请相应替换）。

---

## 1. 添加上游仓库（Upstream）

如果还没有添加源仓库作为上游：

```bash
git remote add upstream 仓库地址
```
检查是否添加成功：
```bash
git remote -v
```
输出应类似：
```
origin    https://github.com/你的用户名/xxx.git (fetch)
origin    https://github.com/你的用户名/xxx.git (push)
upstream https://github.com/上游的用户名/xxx.git (fetch)
upstream https://github.com/上游用户名/xxx.git (push)
```
## 2. 获取上游更新
```bash
git fetch upstream
```
这会把上游仓库的新提交拉取到本地，但不会自动合并。

## 3. 切换到你要同步的分支

通常是 main：
```bash
git checkout main
```
## 4. 使用 Rebase 同步更新
```bash
git rebase upstream/main
```
当有冲突是需要手动解决冲突然后使用 `git rebase --continue` 继续

如果想中止 rebase（回到原来的状态）`git rebase --abort`

重复以上步骤，直到所有冲突解决完成

## 5. 推送更新到你的 fork

因为 rebase 会重写提交历史，所以需要强制推送：
```bash
git push origin main --force-with-lease
```
---
title: git 修改 commit message
published: 2026-07-28
updated: 2026-07-28
pinned: false
tags: ["git"]
category: git
draft: false
slug: git/commit-message
---

# 修改最近一次提交

```bash
git commit --amend -m "新的提交信息"
```

若已经推送到远程，则

```bash
// 安全推送，检查远端是否有更新
git push --force-with-lease origin 分支名

// 强制推送，直接覆盖远端
git push --force origin 分支名
```

---

# 修改历史 commit 信息

```bash
git rebase -i HEAD~n    # n 为需要修改的 commit 数量
```

然后在打开的编辑器中，将需要修改的 commit 前的 `pick` 改为 `reword`，保存退出后，依次修改 commit 信息即可。

修改完成后，若已经推送到远程，则同样需要使用 `git push --force-with-lease` 或 `git push --force` 来推送修改后的历史记录。

---

# 回滚 rebase 操作

```bash
git rebase --abort
```

---

# 注意事项

- 严禁随意强制推送改写历史 commit 信息，尤其是在多人协作的项目中。
- 只适合个人项目或私有分支进行该操作。
- 最优解为新增 commit 来修正错误，而不是修改历史 commit 信息。
---
uuid: 20220831091239
created: 2022-08-31T09:12:39
alias:
- git commit --amend
---

# [[git amend]]

Позволяет изменить предыдущий коммит и сообщение:

```bash
touch test{1..2}.md
git add test1.md && git commit "First and second"
// Забыли добавить второй файл

git commit --amend
```

>[!warning]
>Remember to **only amend commits that have not been pushed anywhere!**The reason for this is that `git commit --amend` does not simply edit the last commit, it _replaces that commit with an entirely new one_. This means that you could potentially destroy a commit other developers are basing their work on. When rewriting history always make sure that you’re doing so in a safe manner, and that your coworkers are aware of what you’re doing.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[TheOdinProject]]
- 🏷️ Tags:: [[062 Version Control]], [[git]]
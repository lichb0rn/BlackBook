---
uuid: 20221206201327
created: 2022-12-06T20:13:27
alias:
---

# [[Git Diff]]

## Diffing
Допустим у нас уже есть изменения в файле:
```shell
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   book_ideas.md
```

Мы вспомнили, что не всё добавили. Снова делаем изменения:
```shell
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   book_ideas.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   book_ideas.md
```

Один файл сразу и в staged, и unstaged. Посмотреть разницу можно с помощью `git diff`:
```shell
diff --git a/books/book_ideas.md b/books/book_ideas.md
index 1a92ca4..5086b1f 100644
--- a/books/book_ideas.md
+++ b/books/book_ideas.md
@@ -7,4 +7,5 @@
 - [ ] CVS by tutorials
 - [ ] Fortran for fun and profit
 - [x] RxSwift by tutorials
-- [ ] Mastering git
+- [x] Mastering git
+- [ ] Care and feeding of developers
```

Добавляем изменения: `git add .`. После этого `git diff` ничего не покажет. Но можем посмотреть разницу между последним коммитом и stage: `git diff --staged`.

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Git Apprentice]]
-  🏷️ Tags:: [[git]]
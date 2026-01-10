---
uuid: 20221206203112
created: 2022-12-06T20:31:12
alias:
---

# [[Git Log]]

- Чтобы просто посмотреть список коммитов и сообщение, можно выполнить `git log`.
- Если нужно увидеть ещё и [[Git Diff|diff]]'ы: `git log -p`
- `git log -3` - три последних коммита
- `git log --oneline` - отображает лог одной строкой:
```bash
ideas git:(main) git log --oneline
6d2d2e2 (HEAD -> main) Adding .gitignore files and HTML
1ba0c3b Adds all the good ideas about management
eae592f Removes terrible live streaming ideas
0e73e27 Moves platform ideas to website directory
db438f1 Updates book ideas for Symbian and MOS 6510
```

- Можно комбинировать: `git log -1 --oneline`
- `git log --graph` - графический вывод:
```bash
* commit fbc46d3d828fa57ef627742cf23e865689bf01a0
| Author: Chris Belanger <chris@razeware.com>
| Date:   Thu Jan 10 10:18:14 2019 -0400
|
|     Adding files for article ideas
|
*   commit 5fcdc0e77adc11e0b2beca341666e89611a48a4a
|\  Merge: 39c26dd cfbbca3
| | Author: Chris Belanger <chris@razeware.com>
| | Date:   Thu Jan 10 10:14:56 2019 -0400
| |
| |     Merge branch 'video_team'
| |
| * commit cfbbca371f4ecc80796a6c3fc0c084ebe181edf0
| | Author: Chris Belanger <chris@razeware.com>
| | Date:   Thu Jan 10 10:06:25 2019 -0400
| |
| |     Removing brain download as per ethics committee
| |
```
- `git log --oneline --graph`:
```bash
* fbc46d3 Adding files for article ideas
*   5fcdc0e Merge branch 'video_team'
|\
| * cfbbca3 Removing brain download as per ethics committee
| * c596774 Adding some video platform ideas
```
- `git shortlog` - Summarize `git log` output
- `git log --author="Miroslav Taleiko" --oneline` - отфильтровать лог по автору
- `git log --grep=ideas --oneline` - [[grep]] по ключевому слову
- Лог коммитов конкретного файла:
```bash
ideas git:(main) git log --oneline books/book_ideas.md
a1009e8 Added new book entry and marked Git book complete
39c26dd I should write a book on git someday
43b4998 Adding book ideas file
```
- Лог изменений в директории: `git log --oneline books` и подробнее
```bash
➜  ideas git:(main) git log --oneline --stat books
1ba0c3b Adds all the good ideas about management
 books/management_book_ideas.md | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
a1009e8 Added new book entry and marked Git book complete
 books/book_ideas.md | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
39c26dd I should write a book on git someday
 books/book_ideas.md | 1 +
 1 file changed, 1 insertion(+)
43b4998 Adding book ideas file
 books/book_ideas.md | 9 +++++++++
 1 file changed, 9 insertions(+)
becd762 Creating the directory structure
 books/.keep | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
```
- Поиск по внутренностям коммита: `git log -S"Fortran"`:
```bash
➜  ideas git:(main) git log -S"Fortran" -p
commit 43b4998d7bf0a6d7f779dd2c0fa4fe17aa3d2453
Author: Chris Belanger <chris@razeware.com>
Date:   Thu Jan 10 10:12:36 2019 -0400

    Adding book ideas file

diff --git a/books/book_ideas.md b/books/book_ideas.md
new file mode 100644
index 0000000..f924368
--- /dev/null
+++ b/books/book_ideas.md
@@ -0,0 +1,9 @@
+# Ideas for new book projects
+
+- [ ] Hotubbing by tutorials
+- [x] Advanced debugging and reverse engineering
+- [ ] Animal husbandry by tutorials
+- [ ] Beginning tree surgery
+- [ ] CVS by tutorials
+- [ ] Fortran for fun and profit
+- [x] RxSwift by tutorials
```


---


## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Git Apprentice]]
-  🏷️ Tags:: [[git]]
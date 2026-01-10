---
uuid: 20221216172715
created: 2022-12-16T17:27:15
alias: git branch
---

# [[Git Branching]]

- Branch is a reference, or a label, to a commit in your repository.
- `git branch <name>` - команда создания ветки
- Под капотом ветка - это файла с хешем на коммит:
```bash
ideas git:(main) ls -la .git/refs/heads
total 16
drwxr-xr-x  4 lichb0rn  staff  128 Dec 16 18:24 .
drwxr-xr-x  5 lichb0rn  staff  160 Dec  6 19:46 ..
-rw-r--r--  1 lichb0rn  staff   41 Dec  9 15:40 main
-rw-r--r--  1 lichb0rn  staff   41 Dec 16 18:24 testBranch

ideas git:(main) cat .git/refs/heads/testBranch
6d2d2e246633a27265a5e30461ec2f5379bdc4ca

ideas git:(main) git log -1
commit 6d2d2e246633a27265a5e30461ec2f5379bdc4ca (HEAD -> main, testBranch)
Author: Miroslav Taleiko <mtaleiko@gmail.com>
Date:   Fri Dec 9 15:40:19 2022 +0300

    Adding .gitignore files and HTML
```

- `git checkout <name>` - переключиться на другую ветку
- `git branch -d <name>` - удалить ветку
- `git branch --all` - показать все ветки, не только локальные:
```sh
ideas git:(main) git branch --all
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```
- `origin` - the default alias for the location of the remote repository from where you cloned your local repository.
- `git branch --all -v`:
```sh
ideas git:(main) git branch --all -v
* main                6d2d2e2 [ahead 8] Adding .gitignore files and HTML
  remotes/origin/HEAD -> origin/main
  remotes/origin/main f65a790 Updated README.md to reflect current working book title.
```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Git Apprentice]]
-  🏷️ Tags:: [[git]]
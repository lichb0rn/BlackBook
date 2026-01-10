---
uuid: 20230120194104
created: 2023-01-20T19:41:04
alias:
- matching tags
- matching paranthese
---

# [[Matching tags in Markup Language]]

Проверка, соответствуют ли все закрывающие теги открытым с помощью [[Стек|стека]] на [[Python]]

```python
def is_matched_html(raw):  
    S = ArrayStack()  
    j = raw.find('<')  
    while j != -1:  
        k = raw.find('>', j + 1)  
        if k == -1:  
            return False  
        tag = raw[j+1:k]  
        print(f'Found tag: {tag} at [{j+1}:{k}]')  
  
        if not tag.startswith('/'):     # opening tag  
            S.push(tag)  
        else:                           # closing tag  
            if S.is_empty():  
                return False  
            if tag[1:] != S.pop():  
                return False  
  
        j = raw.find('<', k+1)  
    return S.is_empty()
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source:: [[Data Structures and Algorithms in Python]]
- 🏷️ Tags:: [[Matching tags]]
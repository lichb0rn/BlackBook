---
uuid: 20230210191448
created: 2023-02-10T19:14:48
alias: pdf converter
---

# [[Automatic PDF to CSV Converter]]

Sometimes you'll need to convert pdf data to CSV (comma separated value) data so you can use it for further analysis. In those cases, this script can come in handy.

```python
import tabula

filename = input("Enter File Path: ")
df = tabula.read_pdf(filename, encoding='utf-8', spreadsheet=True, pages='1')

df.to_csv('output.csv')
```

You'll need to install the tabula library using pip in order to run this code. After installation you can pass the file into your project.

The library comes with a function `read_pdf()` which takes the file and reads it. You finish the automation by using the `to_csv()` function to convert the output into CSV.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source::  [[freeCodeCamp]]
- 🏷️ Tags:: [[Python]], [[PDF]]
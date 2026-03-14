---
up:
  - "[[99_Archive/Old Vault/2 Areas/Web Development|Web Development]]"
related: "[[tailwind]]"
created: 2025-06-01
---
To use **Tailwind CSS v4 (or v3)** in your **Go project with HTML templates**, **without Vite or a JS bundler**, you can use the Tailwind CLI directly. This setup is simple and works great for Go web apps using templates.

---

## **✅ Step-by-step Guide**

  

### **1.**  **Install Tailwind CSS CLI**

You can install it via npm globally:

```sh
npm install -D tailwindcss
npx tailwindcss init
```

Or if you want to keep it scoped to your project:

```sh
mkdir assets
cd assets
npm init -y
npm install -D tailwindcss
npx tailwindcss init
```

This will create a tailwind.config.js file.

---

### **2.**  **Project Structure Example**

```sh
/your-go-project
├── main.go
├── templates/
│   └── index.html
├── static/
│   └── css/
│       └── style.css  ← generated file
├── assets/
│   └── input.css      ← your Tailwind entry
├── tailwind.config.js
```

---

### **3.**  **Create Tailwind Entry File**
In `assets/input.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

### **4.** **Build Tailwind CSS**

Run this in the project root:

```sh
npx tailwindcss -i ./assets/input.css -o ./static/css/style.css --watch
```

This tells Tailwind to:
- Take `input.css` as input,
- Generate `style.css`,
- Watch for changes.

Use `--minify` for production:

```sh
npx tailwindcss -i ./assets/input.css -o ./static/css/style.css --minify
```

---

### **5.** **Serve Static Files in Go**

```go
http.Handle("/static/", http.StripPrefix("/static/", http.FileServer(http.Dir("static"))))
```

And in your HTML template:

```html
<link href="/static/css/style.css" rel="stylesheet">
```

---

### **6.** **Example index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tailwind in Go</title>
  <link href="/static/css/style.css" rel="stylesheet">
</head>
<body class="bg-gray-100 text-center py-10">
  <h1 class="text-4xl font-bold text-blue-600">Hello from Go + Tailwind!</h1>
</body>
</html>
```

---

### **✅ Summary**

|**Tool**|**Role**|
|---|---|
|Tailwind CLI|Compile CSS from Tailwind directives|
|Go|Serve HTML templates + static files|
|No JS bundler|No Vite/Webpack required|

---

---
uuid: 20220825124043
created: 2022-08-25T12:40:43
alias:
---

# [[Node.js production and dev environment]]

When working in a production environment in [[Node.js]], it is common for the host to set the environment variables. In that instance, you will not want to load the values from an `.env` file. 
A useful pattern is to only load the `dotenv` module in non-production environments:

```javascript
if (process.env.NODE_ENV !== 'production') {
	require('dotenv').config();
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[JavaScript Cookbook]]
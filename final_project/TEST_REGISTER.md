# Testing the Registration Route

## Endpoint
**POST** `http://localhost:5000/register`

## Prerequisites
1. Start the server:
   ```bash
   npm start
   ```
   or
   ```bash
   node index.js
   ```

## Test Cases

### 1. Test Successful Registration

**Using cURL:**
```bash
curl -X POST http://localhost:5000/register \
  -H "Content-Type: application/json" \
  -d "{\"username\":\"testuser\",\"password\":\"testpass123\"}"
```

**Expected Response:**
```json
{
  "message": "User successfully registered. Now you can login"
}
```
**Status Code:** 200

---

### 2. Test Missing Username

**Using cURL:**
```bash
curl -X POST http://localhost:5000/register \
  -H "Content-Type: application/json" \
  -d "{\"password\":\"testpass123\"}"
```

**Expected Response:**
```json
{
  "message": "Unable to register user. Username and/or password are not provided."
}
```
**Status Code:** 404

---

### 3. Test Missing Password

**Using cURL:**
```bash
curl -X POST http://localhost:5000/register \
  -H "Content-Type: application/json" \
  -d "{\"username\":\"testuser\"}"
```

**Expected Response:**
```json
{
  "message": "Unable to register user. Username and/or password are not provided."
}
```
**Status Code:** 404

---

### 4. Test Missing Both Username and Password

**Using cURL:**
```bash
curl -X POST http://localhost:5000/register \
  -H "Content-Type: application/json" \
  -d "{}"
```

**Expected Response:**
```json
{
  "message": "Unable to register user. Username and/or password are not provided."
}
```
**Status Code:** 404

---

### 5. Test Duplicate Username

**Step 1:** Register a user first:
```bash
curl -X POST http://localhost:5000/register \
  -H "Content-Type: application/json" \
  -d "{\"username\":\"duplicateuser\",\"password\":\"pass123\"}"
```

**Step 2:** Try to register the same username again:
```bash
curl -X POST http://localhost:5000/register \
  -H "Content-Type: application/json" \
  -d "{\"username\":\"duplicateuser\",\"password\":\"differentpass\"}"
```

**Expected Response:**
```json
{
  "message": "User already exists!"
}
```
**Status Code:** 404

---

## Using Postman or Thunder Client

1. **Method:** POST
2. **URL:** `http://localhost:5000/register`
3. **Headers:**
   - Key: `Content-Type`
   - Value: `application/json`
4. **Body:** Select "raw" and "JSON", then enter:
   ```json
   {
     "username": "your_username",
     "password": "your_password"
   }
   ```

## Using JavaScript (fetch API)

```javascript
// Successful registration
fetch('http://localhost:5000/register', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    username: 'testuser',
    password: 'testpass123'
  })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

## Quick Test Script

You can also create a simple test file to run multiple tests at once.


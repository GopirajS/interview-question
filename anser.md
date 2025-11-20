<span style="color:green;">================================================================ </span>


# ✅ **What is a `Set`?**

A **Set** is a collection of **unique values** — it **cannot contain duplicates**.

### Example:

```js
const s = new Set([1, 2, 2, 3]);
console.log(s); // Set { 1, 2, 3 }
```

### Key Points:

* Stores **unique** values
* Order is preserved by insertion
* Can store any type of value
* Useful for removing duplicates

---

# ✅ **What is a `Map`?**

A **Map** is a collection of **key–value pairs**, similar to an object — but more powerful.

### Example:

```js
const m = new Map();
m.set("name", "John");
m.set("age", 25);
console.log(m.get("name")); // John
```

### Key Points:

* Keys can be **any type** (objects, numbers, functions, etc.)
* Keeps keys in **insertion order**
* Has better performance for large key-value collections than plain objects

---

# ✅ **What is a `WeakMap`?**

A **WeakMap** is like a Map, but:

* **Keys must be objects**
* Keys are kept **weakly**
  → If the object key is removed elsewhere in the code, it is automatically deleted from the WeakMap.

### Example:

```js
let obj = { id: 1 };
const wm = new WeakMap();

wm.set(obj, "some value");

obj = null; // object is removed → weakmap entry auto removed
```

### Key Points:

* Keys must be **objects only**
* Values can be anything
* Keys can be garbage-collected
* Useful for private data or caching
* **Cannot be iterated** (no size, no keys(), no values())

---

# ✅ **What is a `WeakSet`?**

A **WeakSet** is like a Set, but:

* Only stores **objects**
* Objects are kept **weakly**

### Example:

```js
let user = { name: "Tom" };
const ws = new WeakSet();

ws.add(user);

user = null; // object removed → weakset entry auto removed
```

### Key Points:

* Only objects allowed
* No duplicates
* Automatically removes items when object becomes unreachable
* Cannot be iterated (no size, no forEach)

---

# ⭐ Quick Summary Table

| Feature     | Unique?     | Keys/Values allowed      | Weak? | GC Auto Cleanup | Iterable? |
| ----------- | ----------- | ------------------------ | ----- | --------------- | --------- |
| **Set**     | Yes         | Any values               | No    | No              | Yes       |
| **Map**     | Keys unique | Any type (incl. objects) | No    | No              | Yes       |
| **WeakMap** | Keys unique | **Objects only**         | Yes   | Yes             | **No**    |
| **WeakSet** | Yes         | **Objects only**         | Yes   | Yes             | **No**    |

---

If you want I can also give real-world examples or use-cases for each one.



<span style="color:green;">================================================================ </span>


## ⭐ **What is CSP (Content Security Policy)?**

**CSP (Content Security Policy)** is a security feature added in HTTP response headers that helps prevent attacks like **XSS**, **data injection**, and **clickjacking** by restricting what resources the browser is allowed to load and execute.

It tells the browser **what is allowed**:

* Which scripts can run
* Which styles can load
* Which domains are trusted
* Whether inline scripts are allowed

If something violates the policy, the browser **blocks it automatically**.

---

## ⭐ Why CSP is used?

Mainly to prevent:

* **Cross-Site Scripting (XSS)**
* **Data injection attacks**

---

## ⭐ Example CSP Header

### Block all inline scripts & allow scripts only from your domain:

```
Content-Security-Policy: script-src 'self';
```

### Allow scripts from your domain + trusted CDN:

```
Content-Security-Policy: script-src 'self' https://cdn.example.com;
```

### Block all scripts except trusted ones:

```
Content-Security-Policy: default-src 'self';
```

---

## ⭐ Example of CSP Blocking XSS

If a hacker injects:

```html
<script>alert("Hacked!")</script>
```

CSP will **block it** because inline scripts are disabled.

---

## ⭐ One-line Interview Version

**CSP is a browser security mechanism that helps prevent XSS by controlling which scripts, styles, and resources are allowed to load on a page.**



<span style="color:green;">================================================================ </span>


![CSRF](https://media.geeksforgeeks.org/wp-content/uploads/20221219133429/CSRF-Diagram-(1).png)


**CSRF (Cross-Site Request Forgery)** is a security attack where a malicious website tricks a logged-in user into performing unwanted actions on another website **without their knowledge**.

Because the user is already authenticated (logged in), the browser automatically sends their:

* cookies
* session token
* authentication headers

So the attack looks **legitimate** to the server.

---

## ⭐ Example of a CSRF Attack

1. A user is logged in to `bank.com`.
2. The user visits a malicious website.
3. That website secretly sends a request like:

```html
<img src="https://bank.com/transfer?amount=1000&to=hacker" />
```

4. The browser sends the **session cookies** with the request.
5. The bank thinks the user sent it → money is transferred.

---

## ⭐ Why CSRF Happens?

Because browsers automatically include authentication cookies with every request.

---

## ⭐ How to Prevent CSRF

### ✔ 1. **CSRF Tokens** (most important)

A random token added to forms and AJAX requests.

### ✔ 2. **SameSite Cookies**

Set cookie so it is **not** sent on cross-site requests.

```
Set-Cookie: sessionid=abc; SameSite=Lax;
```

### ✔ 3. **Check Referer/Origin headers**

### ✔ 4. **Use CAPTCHA for critical actions**

### ✔ 5. **Double Submit Cookie technique**

---

## ⭐ One-line Interview Version

**CSRF is an attack where a malicious site tricks a logged-in user into making unwanted actions on another website by abusing their authentication cookies.**


<span style="color:green;">================================================================ </span>


In JavaScript, you can throw custom errors using the `throw` keyword. You can throw either:

1. A built-in `Error` object with a custom message
2. A completely custom error class (cleaner and recommended for large apps)

---

## ✅ **1. Throwing a custom message with built-in Error**

```js
throw new Error("Something went wrong!");
```

You can also throw other types:

```js
throw new TypeError("Invalid type provided!");
throw new RangeError("Value out of range!");
```

---

## ✅ **2. Creating your own custom error class (recommended)**

```js
class MyCustomError extends Error {
  constructor(message) {
    super(message);
    this.name = "MyCustomError"; // Optional: sets the error name
  }
}

function demo() {
  throw new MyCustomError("This is my custom error!");
}

try {
  demo();
} catch (err) {
  console.error(err.name);    // MyCustomError
  console.error(err.message); // This is my custom error!
}
```

This approach makes debugging easier and helps categorize errors.

---

## ⚡ **3. Throwing simple values (not recommended)**

JavaScript allows it but avoid in real projects:

```js
throw "Something bad happened";  // string
throw 404;                       // number
throw { message: "error" };      // object
```

---

### ⭐ Best Practice

Always throw `Error` (or custom classes extending `Error`) so stack traces are meaningful and consistent.


<span style="color:green;">================================================================ </span>



# ✅ **Main Categories of JavaScript Errors**


# ✅ **Built-in JavaScript Error Types**

| Error Type         | When it Happens                                                |
| ------------------ | -------------------------------------------------------------- |
| **Error**          | Generic error                                                  |
| **SyntaxError**    | Invalid JavaScript syntax                                      |
| **ReferenceError** | Using a variable that doesn’t exist                            |
| **TypeError**      | Using a value of the wrong type (e.g., calling a non-function) |
| **RangeError**     | Value out of range (e.g., recursive calls maxed out)           |
| **EvalError**      | Related to `eval()` (rarely used now)                          |
| **URIError**       | Bad `encodeURI()` or `decodeURI()` usage                       |
| **AggregateError** | Multiple errors thrown at once (Promises)                      |





<span style="color:green;">================================================================ </span>

**Minification** is the process of removing all unnecessary characters from your code *without changing how it works*, to make the file size smaller and load faster.

![minifid](https://blog.arahoster.com/wp-content/uploads//image-25.png)


# ✅ What Minification Removes

Minification removes things that are not needed for execution:

* **Whitespace**
* **Line breaks**
* **Comments**
* **Long variable names** (renamed to short ones)
* **Unnecessary semicolons**
* **Unused code (if supported by tool)**

---

# ✅ Example Before Minification

```js
function addNumbers(a, b) {
    // This function returns sum
    return a + b;
}
```

### After Minification:

```js
function addNumbers(a,b){return a+b;}
```

---

# ✅ Why Minification Is Used

* Faster page load
* Smaller JavaScript/CSS files
* Better performance for mobile users
* Less bandwidth usage
* Makes code harder to read (light obfuscation)

---

# ✅ Tools That Minify Code

Common tools include:

* **Terser**
* **UglifyJS**
* **Babel Minify**
* **Google Closure Compiler**
* **Webpack (built-in minification)**
* **ESBuild**

---

If you want, I can show how to minify JS using Webpack, Vite, or a single CLI tool.



<span style="color:green;">================================================================ </span>


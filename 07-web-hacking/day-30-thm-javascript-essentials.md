# Day 30 — THM JavaScript Essentials

## Room Details

- **Platform:** TryHackMe
- **Learning Path:** Cyber Security 101
- **Module:** Web Hacking
- **Room:** JavaScript Essentials
- **Status:** Completed

## Learning Objectives

- Understand basic JavaScript syntax and behaviour.
- Understand how JavaScript is integrated into HTML.
- Use variables, functions, conditions, loops, and browser dialogue functions.
- Recognise why client-side controls can be bypassed.
- Inspect and beautify minified JavaScript.
- Identify security risks caused by exposed or unsafe client-side code.

---

## 1. What JavaScript Does

JavaScript adds behaviour and interactivity to HTML and CSS pages.

Common uses include:

- Form validation
- Button click actions
- Pop-up messages
- Animations
- Updating page content
- Sending requests to servers
- Handling user input

From a cybersecurity perspective, JavaScript is important because client-side code is delivered to the user's browser and can be inspected or modified.

```text
Client-side JavaScript should not be trusted to enforce critical security controls.
```


## 2. Variables and Data Types

```javascript
let username = "Rohit";
const port = 443;
var legacyVariable = true;
```

```text
let   → value can be reassigned
const → value should not be reassigned
var   → older variable declaration style
```

Common data types:

```javascript
let name = "Rohit";       // String
let attempts = 3;         // Number
let loggedIn = false;     // Boolean
let result = null;        // Null
let unknown;              // Undefined
```

## 3. Operators and Comparisons

```javascript
let role = "user";  // assignment

5 == "5";           // true
5 === "5";          // false
```

```text
=   → assigns a value
==  → compares values after type conversion
=== → compares both value and data type
```

Strict comparison is normally safer and clearer:

```javascript
if (role === "admin") {
    console.log("Access granted");
}
```


## 4. Functions and Control Flow

Functions group reusable code:

```javascript
function greet(name) {
    return "Hello, " + name;
}
```

Conditional statement:

```javascript
if (password === "SecurePassword") {
    console.log("Access granted");
} else {
    console.log("Access denied");
}
```

Loop:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

Security lesson:

```text
Client-side checks improve user experience.
Server-side checks enforce security.
```

A user controls the browser and may modify variables, functions, and conditions.

---

## 5. JavaScript in HTML

Inline JavaScript:

```html
<script>
    console.log("Inline JavaScript");
</script>
```

External JavaScript:

```html
<script src="script.js"></script>
```

External files may reveal:

- API endpoints
- Hidden parameters
- Validation logic
- Debug information
- Hard-coded credentials or tokens
- Functions that can be called directly

Sensitive information should never be trusted simply because it is hidden inside a JavaScript file.


## 6. Dialogue Functions

Alert:

```javascript
alert("Hello");
```

Prompt:

```javascript
let username = prompt("Enter your username");
```

Confirm:

```javascript
let proceed = confirm("Do you want to continue?");
```

```text
true  → user selected OK
false → user selected Cancel
```

Security concern: user-controlled input must not be trusted automatically. An attacker may change the script, modify variables, bypass the expected flow, or submit unexpected values.

---

## 7. Bypassing Client-Side Control Flow

```javascript
let age = prompt("Enter your age");

if (age >= 18) {
    document.write("Access allowed");
} else {
    document.write("Access denied");
}
```

This is not a reliable security control because the user can:

- Modify the JavaScript
- Change variable values
- Skip the condition
- Call another function directly
- Send a request without using the page

```text
Never rely only on JavaScript for authentication, authorisation, pricing, or privilege checks.
```

The server must validate all important values independently.


## 8. Browser Developer Tools

Important areas:

```text
Console  → run JavaScript and inspect errors
Sources  → inspect JavaScript files
Network  → inspect requests and responses
Elements → inspect and modify HTML
Storage  → inspect cookies and local/session storage
```

Useful examples:

```javascript
console.log("Testing");
document.title;
typeof someVariable;
```

Developer tools can help identify:

- Client-side validation
- Hidden endpoints
- Interesting parameters
- Authentication tokens
- Error messages
- Exposed secrets
- DOM manipulation

---

## 9. Minified JavaScript

Readable code:

```javascript
function checkPassword(password) {
    if (password === "secret") {
        return true;
    }
    return false;
}
```

Minified code:

```javascript
function a(b){return b==="secret"}
```

```text
Minification makes code harder to read.
It does not encrypt or securely hide logic or secrets.
```

Minified code can be reformatted using browser developer tools, beautifiers, or code editors.

Look for:

- Strings
- URLs and API paths
- Tokens
- Password comparisons
- Hidden function names
- Request parameters
- Source maps


## 10. Common Client-Side Security Weaknesses

### Hard-coded secrets

```javascript
const apiKey = "EXPOSED_KEY";
```

Anything sent to the browser can be inspected.

### Client-side-only validation

```javascript
if (username === "admin") {
    allowAccess();
}
```

The logic can be changed or skipped.

### Unsafe use of user input

```javascript
element.innerHTML = userInput;
```

This may create a cross-site scripting risk when untrusted input is inserted without proper handling.

Safer text insertion:

```javascript
element.textContent = userInput;
```

### Dangerous dynamic execution

Avoid:

```javascript
eval(userInput);
```

### Sensitive comments

Comments inside client-side files are visible to users and may expose internal information.


## 11. Best Practices

- Validate important values on the server.
- Do not store passwords, private API keys, database credentials, or secret tokens in JavaScript.
- Use strict comparisons where appropriate.
- Treat all user input as untrusted.
- Prefer safe DOM methods such as `textContent`.
- Avoid `eval()` and similar unsafe dynamic execution.
- Keep JavaScript dependencies updated.
- Use security headers such as Content Security Policy.
- Remove debugging data and sensitive comments before deployment.

---

## 12. Cybersecurity Investigation Workflow

When inspecting JavaScript during an authorised assessment:

```text
1. Identify JavaScript files
2. Read or beautify the code
3. Search for URLs, endpoints, tokens, and interesting strings
4. Identify client-side validation
5. Inspect functions and control flow
6. Compare browser checks with server behaviour
7. Inspect Network requests
8. Test only within authorised scope
9. Document findings and evidence
```

Useful search terms:

```text
password
admin
token
api
secret
key
auth
fetch
XMLHttpRequest
innerHTML
eval
document.cookie
localStorage
sessionStorage
```


## 13. Practical Interpretation

### What did I check?

- JavaScript variables and data types
- Functions, conditions, and loops
- JavaScript integration with HTML
- Dialogue functions
- Client-side control flow
- Browser developer tools
- Minified JavaScript
- Common client-side security risks

### What did I find?

- JavaScript delivered to a browser can be inspected and modified.
- Client-side validation can often be bypassed.
- Dialogue input should not be trusted.
- Minified code is still recoverable and readable.
- Secrets should never be stored in public client-side files.
- Browser developer tools are important for web-security analysis.

### What does it mean?

- Security decisions must be enforced by the server.
- Frontend controls are not reliable barriers against an attacker.
- JavaScript analysis can reveal endpoints, hidden logic, and insecure assumptions.
- Basic JavaScript knowledge is necessary before studying XSS and deeper web attacks.

### What would I do next?

- Practise reading JavaScript in browser developer tools.
- Learn more about the DOM and event handling.
- Understand HTTP requests generated by `fetch`.
- Practise identifying unsafe input handling.
- Continue into introductory web vulnerabilities and Burp Suite.
- Keep testing limited to authorised lab environments.


## Commands and Examples Practised

```javascript
console.log("message");
alert("message");
prompt("Enter value");
confirm("Continue?");
```

```javascript
if (condition) {
    // action
} else {
    // alternative
}
```

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

```javascript
function example(value) {
    return value;
}
```

```html
<script src="script.js"></script>
```

---

## Security and Ethics

All JavaScript inspection and manipulation performed for this room was completed inside an authorised TryHackMe learning environment.

Do not inspect, modify, or test applications without explicit permission.

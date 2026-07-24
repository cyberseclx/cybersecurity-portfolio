# Day 31 – TryHackMe: Burp Suite — The Basics

## Block

**D31-B01 | THM Lab | Burp Suite: The Basics**

## Room Status

- Platform: TryHackMe
- Module: Web Hacking
- Room: Burp Suite: The Basics
- Status: Completed
- Day: 31

---

## Objective

The purpose of this room was to understand how Burp Suite works as an intercepting proxy between a browser and a web application.

The room introduced the main Burp Suite interface, proxy configuration, request interception, request history, scope control, site mapping, and some of the important tools available inside Burp Suite.

---

## What Is Burp Suite?

Burp Suite is a web application security testing platform.

It can sit between a browser and a web server and inspect the HTTP or HTTPS traffic passing between them.

Normal connection:

```text
Browser → Web Server
```

Connection through Burp Suite:

```text
Browser → Burp Suite Proxy → Web Server
```

This allows a tester to:

- View HTTP requests and responses
- Modify requests before they reach the server
- Inspect headers, cookies, parameters, and request bodies
- Repeat and manually test requests
- Map the structure of a web application
- Send requests to other Burp tools

Burp Suite must only be used against systems that I own or have permission to test, including authorised TryHackMe labs.

---

## Burp Suite Editions

### Community Edition

The free edition used mainly for manual web application testing and learning.

### Professional Edition

The paid edition containing advanced tools, including automated scanning and faster testing features.

### Enterprise Edition

Designed for large-scale and continuous web application security scanning across organisations.

---

## Main Burp Suite Interface

The Burp Suite interface is divided into different tabs. Each tab contains tools for a specific part of web application testing.

Important areas introduced in this room included:

- Dashboard
- Target
- Proxy
- Repeater
- Intruder
- Decoder
- Comparer
- Sequencer

Some advanced features are limited or unavailable in the Community Edition.

---

## Dashboard

The Dashboard provides an overview of Burp Suite activity.

It can show:

- Tasks
- Event logs
- Issue activity
- Errors and warnings
- Background processes

The event log is useful when troubleshooting problems such as proxy errors or failed connections.

---

## Target Tab

The Target tab helps organise information about the web application being tested.

### Site Map

The Site Map records the hosts, paths, files, directories, parameters, and endpoints observed by Burp Suite.

It helps create a structured map of the application.

Example:

```text
http://target.thm/
├── login
├── dashboard
├── profile
└── api
```

### Scope

Scope defines which hosts or URLs belong to the authorised testing target.

Using scope helps:

- Reduce unrelated traffic
- Prevent accidental testing of third-party services
- Keep the Site Map organised
- Focus testing on the intended application

A target should be added to scope before deeper testing.

---

## Proxy Tab

The Proxy tab is one of the most important parts of Burp Suite.

It controls the intercepting proxy that sits between the browser and the web server.

### Default Proxy Listener

Burp Suite commonly listens on:

```text
127.0.0.1:8080
```

This means the browser sends its traffic to Burp Suite on local port `8080`.

### Intercept Is On

When interception is enabled, Burp pauses the request before forwarding it to the server.

This allows the request to be:

- Inspected
- Modified
- Forwarded
- Dropped
- Sent to another Burp tool

### Forward

The **Forward** button sends the intercepted request to the server.

### Drop

The **Drop** button discards the request and prevents it from reaching the server.

### Intercept Is Off

When interception is disabled, requests pass through Burp without being manually paused.

Burp can still record the traffic in HTTP history.

---

## HTTP History

The HTTP history records requests and responses that passed through the proxy.

It can contain:

- Host
- HTTP method
- URL
- Status code
- Request parameters
- Cookies
- Response length
- MIME type

HTTP history is useful because I can review traffic even when interception is turned off.

---

## Embedded Browser

Burp Suite includes a built-in Chromium-based browser that is already configured to use Burp Proxy.

This avoids manually changing the proxy settings of another browser.

The embedded browser can be opened from:

```text
Proxy → Intercept → Open Browser
```

It is useful for quickly starting an authorised web application test.

---

## HTTPS and Burp CA Certificate

HTTPS traffic is encrypted.

To inspect HTTPS traffic, Burp Suite acts as an intermediary and presents its own certificate to the browser.

The browser must trust the Burp Certificate Authority certificate for HTTPS interception to work without certificate warnings.

This certificate should only be installed in a dedicated testing browser or lab environment.

---

## Important HTTP Request Components

Example intercepted request:

```http
POST /login HTTP/1.1
Host: target.thm
Content-Type: application/x-www-form-urlencoded
Cookie: session=abc123
Content-Length: 32

username=rohit&password=test123
```

### Request Line

```http
POST /login HTTP/1.1
```

It contains:

- HTTP method
- Requested path
- HTTP version

### Host Header

```http
Host: target.thm
```

It identifies the target web server.

### Cookie Header

```http
Cookie: session=abc123
```

It may contain session or authentication data.

### Request Body

```text
username=rohit&password=test123
```

It contains data submitted to the application.

Burp allows these values to be inspected and changed before the request is forwarded.

---

## Burp Suite Tools

### Repeater

Repeater allows a request to be modified and sent repeatedly.

Typical workflow:

```text
Proxy → HTTP History → Select Request → Send to Repeater
```

Common shortcut:

```text
Ctrl + R
```

Use cases:

- Testing different parameter values
- Examining application responses
- Repeating requests without using the browser
- Manually checking input validation

---

### Intruder

Intruder automates repeated requests using selected payload positions.

Potential authorised uses include:

- Fuzzing parameters
- Testing input handling
- Checking multiple values
- Discovering hidden behaviour

The Community Edition intentionally limits Intruder speed.

---

### Decoder

Decoder converts or transforms data between different formats.

Examples:

- URL encoding
- Base64 encoding
- HTML encoding
- Hexadecimal
- Plain text

Encoding is not the same as encryption.

---

### Comparer

Comparer highlights differences between two pieces of data.

It can compare:

- Two requests
- Two responses
- Two tokens
- Two application outputs

This can help detect small changes in server behaviour.

---

### Sequencer

Sequencer analyses the randomness and quality of generated tokens.

It may be used to assess values such as:

- Session tokens
- Password-reset tokens
- Anti-CSRF tokens

Weak or predictable tokens can create security risks.

---

## Useful Burp Shortcuts

```text
Ctrl + R       Send request to Repeater
Ctrl + I       Send request to Intruder
Ctrl + Shift+B Base64 encode
Ctrl + Shift+U URL encode
```

Shortcuts may vary depending on the Burp Suite version and operating system.

---

## Basic Burp Testing Workflow

```text
1. Start Burp Suite
2. Open the Burp embedded browser
3. Add the authorised target to scope
4. Browse the application
5. Review Proxy HTTP history
6. Enable interception when a request must be changed
7. Forward or drop the request
8. Send useful requests to Repeater
9. Modify one value at a time
10. Compare the server responses
11. Record findings and evidence
```

---

## Practical Understanding

### What Did I Check?

I checked how Burp Suite captures browser traffic and how intercepted HTTP requests can be viewed before reaching the server.

### What Did I Find?

I found that Burp Suite can record requests in HTTP history, pause them through Intercept, modify headers or parameters, and send selected requests to tools such as Repeater.

### What Does It Mean?

It means Burp Suite provides visibility and control over the communication between the browser and web application.

This makes it possible to test how an application handles manipulated inputs in an authorised environment.

### What Would I Do Next?

I would practise:

- Capturing GET and POST requests
- Identifying parameters and cookies
- Sending requests to Repeater
- Changing one parameter at a time
- Comparing the resulting responses
- Keeping the target restricted to scope

---

## Key Lessons

1. Burp Suite works as an intercepting proxy between a browser and a web server.
2. Proxy Intercept can pause, inspect, modify, forward, or drop HTTP requests.
3. HTTP history records traffic even when interception is disabled.
4. The Target Site Map helps organise discovered application endpoints.
5. Scope keeps testing focused on authorised systems.
6. Repeater is used for controlled manual request testing.
7. Intruder automates repeated requests using payload positions.
8. Decoder transforms encoded data, while Comparer highlights differences.
9. The embedded browser is preconfigured to work with Burp Proxy.
10. Burp Suite must only be used where explicit permission exists.

---

## Commands and Paths to Remember

```text
Default Burp proxy: 127.0.0.1:8080
Open browser: Proxy → Intercept → Open Browser
View traffic: Proxy → HTTP history
View application map: Target → Site map
Send to Repeater: Right-click request → Send to Repeater
```

---

## Personal Reflection

Before this room, I understood Burp Suite mainly as a tool used to capture web requests.

After completing the room, I now understand its wider workflow: setting a target scope, mapping application traffic, inspecting requests through Proxy, reviewing HTTP history, and moving requests into specialised tools such as Repeater.

The most important concept is that Burp Suite gives controlled visibility into HTTP communication. It does not automatically find every vulnerability; the tester must understand the request, modify values logically, and interpret the server response.

---

## Completion Evidence

- [x] Burp Suite introduction completed
- [x] Burp Suite editions reviewed
- [x] Interface and dashboard explored
- [x] Target and Site Map understood
- [x] Scope concept understood
- [x] Proxy listener reviewed
- [x] Request interception practised
- [x] HTTP history reviewed
- [x] Embedded browser used
- [x] Core Burp tools reviewed
- [x] TryHackMe room completed

---

## Suggested Repository Path

```text
07-web-hacking/day-31-thm-burp-suite-the-basics.md
```

---

## Next Step

Continue the Web Hacking module and practise sending captured requests from Proxy to Repeater for controlled manual testing.

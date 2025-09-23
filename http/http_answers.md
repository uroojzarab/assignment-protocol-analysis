# HTTP Trace Analysis Report

### 1. What is the name of the website?

The name of the website, as shown in the **Host** field of the GET request, is:

**httpbin.org**

---

### 2. Find the packet that contains the first GET request for the website you have accessed.

The first GET request found in the trace is:
GET /basic-auth/user/passwd HTTP/1.1
Host: httpbin.org
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 ...
Sec-Purpose: prefetch;prerender
Purpose: prefetch
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,/;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9

---

### 3.Describe all headers and their values in this GET request message.

# Headers:

- **Host:** httpbin.org → The target server.
- **Connection:** keep-alive → Client requests a persistent connection.
- **Upgrade-Insecure-Requests:** 1 → Browser prefers secure resources if possible.
- **User-Agent:** Mozilla/5.0 … → Identifies the browser and operating system.
- **Sec-Purpose:** prefetch;prerender → Request was preloaded.
- **Purpose:** prefetch → Confirms prefetching.
- **Accept:** Lists acceptable content types.
- **Accept-Encoding:** gzip, deflate → Supported compression formats.
- **Accept-Language:** en-US,en;q=0.9 → Preferred languages.

---

### 4.4. Identify the status code in the first server response.

# Status Code in First Server Response

The status code in the first server response is:

**401 Unauthorized**

---

### 5. 5. How many HTTP response messages are exchanged in total?

# Total HTTP Response Messages

There are **4 HTTP response messages** exchanged in total:

1. 401 Unauthorized
2. 401 Unauthorized
3. 200 OK
4. 404 Not Found

---

### 6. Persistent Connection Check

The connection **is persistent**.

**Evidence:**

- `Connection: keep-alive` is present in both client requests and server responses.
- Multiple requests and responses are exchanged over the same TCP connection without closing after each response.

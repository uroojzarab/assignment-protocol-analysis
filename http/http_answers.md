# HTTP Trace Analysis Report

### 1. What is the name of the website?

The name of the website, as shown in the **Host** field of the GET request, is:

**httpbin.org**

---

### 2. Find the packet that contains the first GET request for the website you have accessed.
The first get request is in frame #257


---

### 3.Describe all headers and their values in this GET request message.

# Headers:
Host: httpbin.org

Connection: keep-alive

DNT: 1

Upgrade-Insecure-Requests: 1

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36 Avast/131.0.0.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7

Accept-Encoding: gzip, deflate

Accept-Language: en-US,en;q=0.9

---

### 4.4. Identify the status code in the first server response.

# Status Code in First Server Response
The first response  at Frame #377 has Status Code: 200 OK.

---

### 5. 5. How many HTTP response messages are exchanged in total?

# Total HTTP Response Messages

There are ** 2 HTTP response messages** exchanged in total:
at frame no
#377
#572


---

### 6. Persistent Connection Check

The connection **is persistent**.

**Evidence:**

- `Connection: keep-alive` is present in both client requests and server responses.
- Multiple requests and responses are exchanged over the same TCP connection without closing after each response.

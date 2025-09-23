HTTPS ANALYSIS:

For the HTTPS based website access, answer the following:

a. What is the name of website?
www.wikipedia.org

---

b. Find the packet that contains the ClientHello message for the website you are accessing.
The ClientHello message for www.wikipedia.org is in Packet #337 (Time: 21.247093).

---

c. List all the TLS extensions included in the ClientHello.  

 Extracted Extensions List

1. Reserved (GREASE) (len=0)
2. compress_certificate (len=3)
3. key_share (len=1263) → X25519MLKEM768, x25519
4. signed_certificate_timestamp (len=0)
5. supported_groups (len=12)
6. signature_algorithms (len=18)
7. supported_versions (len=7) → TLS 1.3, TLS 1.2
8. encrypted_client_hello (len=186)
9. extended_master_secret (len=0)
10. session_ticket (len=0)
11. server_name (len=22) → name=www.wikipedia.org
12. psk_key_exchange_modes (len=2)
13. application_layer_protocol_negotiation (len=14)
14. renegotiation_info (len=1)
15. status_request (len=5)
16. ec_point_formats (len=2)
17. Unknown type 17613 (len=5)
18. Reserved (GREASE) (len=1)
19. pre_shared_key (len=251)

---

d. Identify the ServerHello message. What cipher suite is chosen by the server?
• The ServerHello message is in Packet #340 (same TCP stream as the ClientHello fo www.wikipedia.org).
• The server selected: TLS version 1.2
• with the cipher suite: TLS_AES_128_GCM_SHA256 (0X1301)

---

e. Locate the Certificate message. Extract the server’s certificate information (issuer, subject, validity dates)?

• Packet : #340 (Server Hello for TLS 1.2)

• Handshake Type: Server Hello / Certificate (encrypted in TLS 1.2)

• TLS Version: 1.2

• Cipher Suite: TLS_AES_128_GCM_SHA256

Reason certificate details are not visible:

The certificate and application data appear encrypted because TLS uses session keys derived during the handshake. Without these keys, Wireshark cannot decrypt the messages. In TLS 1.3, certificates are always encrypted for privacy, and in TLS 1.2, ephemeral key exchanges (DHE/ECDHE) can also cause the certificate to be encrypted. Similarly, all HTTP traffic is encrypted after the handshake to ensure confidentiality and prevent eavesdropping.

---

f. After the TLS handshake, identify the first encrypted application data packet. Why can’t you directly see the HTTP headers in this packet?

The first Application Data packet (Content Type = 23, e.g., Packet #01) appears immediately after the TLS handshake is complete.
This packet carries the encrypted HTTP request/response.

Reason headers are hidden:

All HTTP traffic is encrypted after the TLS 1.2 handshake. Without the session keys, Wireshark cannot decrypt the packet, so the HTTP headers and content are not visible.

---

# QUIC Wireshark Analysis

## 1. Find the packet that contains the Initial QUIC handshake. What information is exchanged here?  
- Filter used: `quic && quic.long.packet_type == 0`  
- The Initial QUIC handshake packet contains:  
  - **Connection IDs**: Destination Connection ID = `be5b4395809dc4d2`, Source Connection ID = `0` (in this trace).  
  - **Token**: A long random value used for address validation.  
  - **QUIC Version**: `1 (0x00000001)`  
  - **CRYPTO Frames**: Carry fragments of the TLS 1.3 handshake.  
- This packet establishes the QUIC connection context and begins negotiating TLS keys.  

---

## 2. Identify the QUIC packet that contains the TLS ClientHello (QUIC embeds TLS handshake inside QUIC).  
- Found inside the **Initial Packet → CRYPTO Frame → TLSv1.3 Record Layer → Handshake Protocol: Client Hello**.  
- The ClientHello contains:  
  - **TLS Version**: 1.3 (recorded as `0x0303`)  
  - **Cipher Suites**: 3 suites offered  
  - **Extensions**:  
    - `key_share`: `x25519`  
    - `application_layer_protocol_negotiation (ALPN)`: `h3`  
    - `compress_certificate`  
    - `supported_versions`: TLS 1.3  
    - `server_name (SNI)`: `ssl.gstatic.com`  
    - `supported_groups`: `x25519`  
    - `quic_transport_parameters`  
    - `encrypted_client_hello`  
    - `early_data`, `pre_shared_key`  
- **Summary:** The TLS ClientHello is carried in the QUIC Initial packet via CRYPTO frames and contains SNI, ALPN (`h3`), cipher suites, and QUIC-specific transport parameters.  

---

## 3. Which QUIC version is used in your trace?  
- Observed in the Initial packet header:  
  - **Version: 1 (0x00000001)**  
- This corresponds to **QUIC v1**, the standardized version in use today.  

---

## 4. Locate the packet where 0-RTT or 1-RTT keys are first used.  
- After the handshake packets, Wireshark shows packets with:  
  - **Packet Number Space = 1-RTT**  
- The first such packet in the trace is the point where QUIC transitions to fully encrypted communication.  
- **Answer:** The first 1-RTT packet indicates session keys are now being used for encrypted data.  

---

## 5. Find the first packet that carries application data (HTTP/3).  
- Filter used: `http3`  
- The first packet shows **HTTP/3 application data** (e.g., a `HEADERS` frame containing an HTTP GET request).  
- **Difference from HTTP over TCP:**  
  - HTTP/3 runs directly over QUIC (UDP), not TCP.  
  - No TCP 3-way handshake is required.  
  - Multiplexing avoids Head-of-Line blocking seen in TCP.  
  - TLS is integrated into QUIC instead of layered separately.  

---

# Notes
- QUIC handshake = QUIC Initial packet + embedded TLS 1.3 handshake.  
- The TLS ClientHello is carried inside **QUIC CRYPTO frames**.  
- HTTP/3 over QUIC avoids TCP entirely, enabling faster connection setup and improved multiplexing.  

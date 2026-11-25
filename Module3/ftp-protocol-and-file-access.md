# 11. File Transfer Protocol (FTP): Working, File Access Mechanisms, Advantages, and Disadvantages

## Introduction

**FTP (File Transfer Protocol)**—standardized in **RFC 959**—is a standard application-layer client–server protocol built on **TCP** used to transfer files reliably between a local host (client) and a remote host (server) across a TCP/IP network.

---

## 1. Dual-Connection Architecture of FTP

A defining feature of FTP is that it uses **two separate TCP connections** simultaneously:

1. **Control Connection (TCP Port 21):**
   * Remains open for the **entire duration** of the FTP session.
   * Carries **out-of-band** control commands (`USER`, `PASS`, `LIST`, `RETR`, `STOR`, `QUIT`) and server status codes (e.g., `200 OK`, `530 Not logged in`).
2. **Data Connection (TCP Port 20 in Active Mode):**
   * Opened **only when a file or directory listing is being transferred**, and closed immediately after the transfer completes.
   * Carries the actual file contents.

```text
+------------------+                                  +------------------+
|    FTP Client    |                                  |    FTP Server    |
|                  |  --- Control Connection ------>  |                  |
|  User Interface  |       (TCP Port 21: Persistent)  |  Control Process |
|                  |                                  |                  |
|  Data Transfer   |  <== Data Connection =========>  |  Data Transfer   |
|     Process      |       (TCP Port 20: Per-File)    |     Process      |
+------------------+                                  +------------------+
```

---

## 2. File Access & Transfer Mechanisms in FTP

Unlike remote file systems (such as NFS) that allow random byte-level reads/writes on a mounted remote disk, FTP uses a **whole-file copy mechanism** with the following operational modes:

### A. Active vs. Passive Mode (Establishing the Data Connection)
* **Active Mode:**
  1. Client connects to Server Port 21 (Control) and sends a `PORT` command advertising a client port.
  2. Server initiates the Data Connection from **Server Port 20** back to the client's advertised port.
  * *Drawback:* Often blocked by client-side firewalls/NAT.
* **Passive Mode (`PASV`):**
  1. Client connects to Server Port 21 and sends `PASV`.
  2. Server opens an ephemeral port and tells the client; the **client initiates** both Control and Data connections to the server.
  * *Benefit:* Works cleanly behind client firewalls and NAT.

### B. Data Representation & Transmission Modes
* **File Types:**
  * **ASCII Mode:** Translates text files (converting line endings like `CRLF` $\leftrightarrow$ `LF`) between heterogeneous OSes.
  * **Binary (Image) Mode:** Transfers files bit-by-bit without modification (used for images, executables, archives).
* **Transmission Modes:**
  * **Stream Mode:** Default mode; data sent as a continuous stream of bytes (EOF signaled by closing the data connection).
  * **Block Mode:** Data sent in blocks with headers, enabling checkpointing and **resume** after interruption.
  * **Compressed Mode:** Uses simple Run-Length Encoding (RLE) to compress repeated bytes.

---

## 3. Advantages of FTP

1. **High-Speed Bulk Transfer:** Optimized for transferring large files and multiple files in batches (`mget`, `mput`).
2. **Resume Capability:** Supports restarting interrupted transfers from the last checkpoint rather than starting over.
3. **Cross-Platform Interoperability:** Abstracts differences in OS directory structures and text encodings (ASCII vs. Binary).
4. **Out-of-Band Control (Multitasking):** Separate control and data channels allow users to browse directories or abort transfers while data is moving.
5. **Automation & Scripting:** Easily scripted for scheduled backups and automated server synchronization.

---

## 4. Disadvantages of FTP

1. **No Encryption (Severe Security Risk):** Standard FTP transmits usernames, passwords, commands, and file contents in **plain text**, making it vulnerable to packet sniffing and Man-in-the-Middle (MitM) attacks.
2. **Compliance Failures:** Fails modern security standards (HIPAA, PCI-DSS, GDPR) unless replaced by **FTPS** (FTP over SSL/TLS) or **SFTP** (SSH File Transfer Protocol).
3. **Firewall / NAT Complications:** Active mode requires the server to open a connection back to the client, which firewalls frequently block.
4. **High Connection Overhead:** Maintaining two TCP connections per user increases server resource consumption.
5. **No Partial/Random File Access:** Cannot edit a few bytes of a remote file in place; the entire file must be downloaded, edited, and re-uploaded.

---

## References & Study Hints

* **GeeksforGeeks — FTP Working & Benefits:** [https://www.geeksforgeeks.org/computer-networks/ftp-server-working-and-its-benefits/](https://www.geeksforgeeks.org/computer-networks/ftp-server-working-and-its-benefits/)
* **GeeksforGeeks — FTP vs. SFTP:** [https://www.geeksforgeeks.org/computer-networks/difference-between-file-transfer-protocol-ftp-and-secure-file-transfer-protocol-sftp/](https://www.geeksforgeeks.org/computer-networks/difference-between-file-transfer-protocol-ftp-and-secure-file-transfer-protocol-sftp/)
* **Exam Tip (5–10 Marks):** Always draw the **dual-connection diagram** (Port 21 Control vs. Port 20 Data), explain **Active vs. Passive mode** and **ASCII vs. Binary** transfer, and list 4–5 clear Advantages & Disadvantages (highlighting plaintext insecurity and **FTPS/SFTP** alternatives).

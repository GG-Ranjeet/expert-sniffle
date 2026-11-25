# 13. Electronic Mail Systems and SMTP

## Introduction

**Electronic Mail (Email)** is one of the oldest and most widely used asynchronous application-layer services on the Internet. It enables users to compose, send, store, and retrieve text and multimedia messages across global networks using a **client–server, store-and-forward architecture**.

---

## 1. Architecture and Core Components of an Email System

1. **User Agent (UA):**
   * The email client software used to compose, read, reply to, and manage messages (e.g., Outlook, Thunderbird, Apple Mail, or webmail like Gmail).
2. **Mail Server & Spool / Mailbox:**
   * **Outgoing Queue (Spool):** Holds messages waiting to be transmitted.
   * **Mailbox:** Stores incoming messages for a specific user until retrieved.
3. **Message Transfer Agent (MTA):**
   * Server-side daemon (e.g., Postfix, Sendmail) that relays messages from the sender's mail server to the recipient's mail server using **SMTP**.
4. **Message Access Agent (MAA):**
   * Server-side service that allows the recipient's User Agent to pull/sync emails from their mailbox using **POP3** or **IMAP**.

### Email System Architecture Diagram

```text
[ Sender Side ]                                               [ Receiver Side ]
+----------------+                                            +----------------+
| User Agent (UA)|                                            | User Agent (UA)|
| (Client App)   |                                            | (Client App)   |
+-------+--------+                                            +-------+--------+
        |                                                             ^
        | SMTP (Push: Port 25/587)                                    | POP3 (110) /
        v                                                             | IMAP (143)
+----------------+          DNS MX Lookup +                   +-------+--------+
| Sender's Mail  | =======  SMTP Relay (Port 25) ===========> | Receiver's Mail|
| Server (MTA)   |                                            | Server (MAA)   |
+----------------+                                            +----------------+
```

---

## 2. Step-by-Step Working of Email Delivery

1. **Composition:** Alice composes a message to `bob@example.com` in her **User Agent (UA)** and clicks Send.
2. **Submission (UA $\rightarrow$ Sender MTA):** Alice's UA pushes the message to her mail server using **SMTP** (typically Port 587).
3. **DNS MX Lookup & Relay (Sender MTA $\rightarrow$ Receiver MTA):**
   * Sender's MTA queries **DNS** for the **`MX` (Mail Exchange)** record of `example.com` to find the IP address of Bob's mail server.
   * Sender's MTA opens a TCP connection on **Port 25** and relays the email via **SMTP** to Bob's mail server.
4. **Storage:** Bob's mail server places the email into Bob's **Mailbox**.
5. **Retrieval (Receiver MAA $\rightarrow$ Receiver UA):** Bob's UA connects to his mail server using **POP3** or **IMAP** to read the email.

---

## 3. Short Notes on SMTP (Simple Mail Transfer Protocol)

* **Definition:** **SMTP** (RFC 5321) is a text-based, connection-oriented application-layer protocol running over **TCP Port 25** (and Port 587 for authenticated submission; 465 for SMTPS).
* **Push Protocol:** SMTP is strictly a **push protocol**—used to *send* mail from client to server and *relay* mail from server to server. It cannot pull mail from a mailbox.
* **Key SMTP Commands:**
  * `HELO` / `EHLO` — Identifies the sending client/server.
  * `MAIL FROM:<addr>` — Specifies the sender's address.
  * `RCPT TO:<addr>` — Specifies the recipient's address.
  * `DATA` — Marks the start of the email headers and body (terminated by `<CRLF>.<CRLF>`).
  * `QUIT` — Closes the SMTP TCP connection.
* **MIME Extension:** Because original SMTP only supported 7-bit ASCII text, **MIME (Multipurpose Internet Mail Extensions)** is used to encode non-ASCII characters, images, audio, and file attachments (via Base64).

---

## 4. Mail Retrieval Protocols: POP3 vs. IMAP

| Feature | POP3 (Post Office Protocol v3) | IMAP (Internet Message Access Protocol) |
| :--- | :--- | :--- |
| **Default Port** | TCP `110` (POP3S: `995`) | TCP `143` (IMAPS: `993`) |
| **Storage Model** | **Download-and-Delete** (stored locally; removed from server by default). | **Server-Side Sync** (messages remain on server; folders/read-status sync across devices). |
| **Best Use Case** | Single-device offline access. | Multi-device access (laptop, phone, webmail). |

---

## References & Study Hints

* **GeeksforGeeks — Introduction to Electronic Mail:** [https://www.geeksforgeeks.org/computer-science-fundamentals/introduction-to-electronic-mail/](https://www.geeksforgeeks.org/computer-science-fundamentals/introduction-to-electronic-mail/)
* **Exam Tip (5–10 Marks):** Draw the **UA $\rightarrow$ MTA $\rightarrow$ MTA $\rightarrow$ MAA $\rightarrow$ UA** diagram, clearly label **SMTP (Push)** vs. **POP3/IMAP (Pull)** with their port numbers (`25`, `110`, `143`), and include key SMTP commands (`HELO`, `MAIL FROM`, `RCPT TO`, `DATA`, `QUIT`) plus **MIME**.

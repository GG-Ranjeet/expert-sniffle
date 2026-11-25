### 1. Primary Roles and Responsibilities of the Transport Layer

* **Process-to-Process Delivery (Port Addressing):** Delivers messages to specific applications or processes on the host using port numbers rather than just host-to-host delivery.
* **Segmentation and Reassembly:** Divides large data streams from the application layer into smaller segments at the sender side and reassembles them in proper order at the receiver side.
* **Reliability, Flow Control & Error Control:** Provides end-to-end reliability (in TCP) through acknowledgments, sequence numbers, checksum error detection, retransmissions, and sliding-window flow control to prevent buffer overflow.

---

### 2. Advantages of UDP over TCP

* **Lower Latency & No Handshake Overhead:** UDP is connectionless and does not require a three-way handshake before transmission, making transmission start immediately.
* **Minimal Header Overhead:** UDP has a fixed, compact 8-byte header compared to TCP's 20- to 60-byte header, conserving bandwidth.
* **No Retransmission Delays or Head-of-Line Blocking:** Real-time applications (such as VoIP, live streaming, DNS, and online gaming) prefer dropping occasional packets over waiting for retransmissions.
* **Supports Multicasting and Broadcasting:** Unlike TCP (which is strictly point-to-point unicast), UDP supports one-to-many and one-to-all transmissions.

---

### 3. Design Issues of the Session Layer

* **Dialog Management & Control:** Determining who transmits at a given time and whether transmission is simplex, half-duplex, or full-duplex.
* **Synchronization & Checkpointing:** Inserting checkpoints into long data streams so that upon failure, transmission resumes from the last confirmed checkpoint rather than from the beginning.
* **Session Establishment, Maintenance, and Graceful Termination:** Managing session lifecycles, ensuring both ends cleanly close connections without premature data loss.

---

### 4. Remote Procedure Call (RPC)

**Remote Procedure Call (RPC)** is a client-server communication mechanism that allows a computer program to execute a subroutine, procedure, or function on a remote computer or address space as if it were a normal local procedure call, abstracting away underlying network communication details (using client stubs and server skeletons for serialization/marshaling).

---

### 5. Data Compression

**Data compression** is the process of encoding information using fewer bits than the original representation to reduce storage requirements and transmission bandwidth across a network. It is categorized into:
* **Lossless Compression:** The original data can be perfectly reconstructed (e.g., Run-Length Encoding, Huffman coding, LZW), essential for text and executable files.
* **Lossy Compression:** Approximates original data by discarding imperceptible details to achieve higher compression ratios (e.g., JPEG, MP3, MPEG), suitable for multimedia.

---

### 6. Example of File Access in the Application Layer

* **NFS (Network File System):** Allows a client computer to access and manipulate files on a remote server as if they were stored on its own local disk (providing transparent remote read/write/seek access without needing to download the entire file first).
* *(Alternative standard example: **TFTP / WebDAV**).*

---

### 7. Two Services / Features Provided by FTP

* **Dual-Channel Architecture:** Separates control information and actual data by using two dedicated connections:
  * **Control Connection (Port 21):** For transmitting commands, login authentication, and status codes.
  * **Data Connection (Port 20):** Dedicated solely to file data transfer.
* **Heterogeneous System Support & File Management:** Transfers files transparently between different operating systems (resolving differences in directory structures, character sets, and line endings) while supporting directory browsing, file renaming, and file deletion.

---

### 8. Virtual Terminal

A **virtual terminal** is a software abstraction or logical emulation that represents a standardized terminal device across a network. It maps diverse physical terminal hardware codes, display characteristics, and keystrokes into a universal Network Virtual Terminal (NVT) format, allowing any client terminal to interact with any remote host regardless of manufacturer or operating system.

---

### 9. Telnet

**Telnet (Telecommunication Network)** is an application-layer client-server protocol (operating on well-known TCP port 23) that provides a bidirectional, text-based interactive command-line interface for remotely logging in to and administering computers over an IP network using a Network Virtual Terminal (NVT).

---

### 10. DNS and Why It Is Required

* **Definition:** **DNS (Domain Name System)** is a hierarchical, decentralized naming and directory system (operating on UDP/TCP port 53) that translates human-readable hostnames/domain names (e.g., `www.google.com`) into machine-routable numerical IP addresses (e.g., `142.250.190.46`).
* **Why It Is Required:** Humans easily remember meaningful alphanumeric names, whereas network devices and routing protocols require numeric binary/IP addresses to locate destinations. DNS eliminates the need for users to remember complex numeric IP strings and allows server IP addresses to change without changing domain names.

---

### 11. Definition of HTTP

**HTTP (HyperText Transfer Protocol)** is a stateless, application-layer request-response protocol (standardized on TCP port 80; port 443 for HTTPS) used for transmitting hypermedia documents (such as HTML, images, stylesheets, scripts, and API payloads) across the World Wide Web between web clients (browsers) and web servers.

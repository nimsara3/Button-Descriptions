# Understanding TCP: How Computers Establish and Close Connections

## 1. What is TCP?
**TCP (Transmission Control Protocol)** is a protocol that allows computers to **reliably send and receive data** over the network.  

It makes sure that:
- Data arrives **in order**
- No data is lost
- Connections are properly opened and closed  

TCP is used for many common applications like **web browsing (HTTP/HTTPS)**, **email**, and **file transfers**.

---

## 2. Where TCP Works in the Network
- **Network Layer:** Transport Layer (Layer 4 in OSI model)  
- **Transport Protocol:** TCP itself  
- **Ports:** Each application has a port number (e.g., HTTP uses port 80, HTTPS uses 443)  
- **Roles:**  
  - **Client:** Initiates the connection  
  - **Server:** Accepts the connection

---

## 3. TCP Connection Establishment: Three-Way Handshake

TCP connections are established using a **three-step process**:

### Step 1: SYN (Synchronize)
- The client sends a **SYN packet** to the server to request a connection  
- Marks the start of communication

**Observed Traffic:**  
- Packet from client to server with **SYN flag set**  

---

### Step 2: SYN-ACK (Synchronize-Acknowledge)
- The server responds with a **SYN-ACK packet**  
- It acknowledges the client’s request and indicates it is ready to communicate

**Observed Traffic:**  
- Packet from server to client with **SYN and ACK flags set**

---

### Step 3: ACK (Acknowledge)
- The client sends an **ACK packet** to the server  
- Confirms that the connection is established

**Observed Traffic:**  
- Packet from client to server with **ACK flag set**  
- Now the connection is open and data can be exchanged

| Step | Packet  | Source → Destination | Flags    | Notes                                                                        |
| ---- | ------- | -------------------- | -------- | ---------------------------------------------------------------------------- |
| 1    | SYN     | Client → Server      | SYN      | Client wants to start a connection; initial sequence number `x`              |
| 2    | SYN-ACK | Server → Client      | SYN, ACK | Server acknowledges client (`ACK=x+1`) and sends its own sequence number `y` |
| 3    | ACK     | Client → Server      | ACK      | Client acknowledges server (`ACK=y+1`); connection established               |

---

## 4. TCP Connection Termination

TCP connections are closed using a **four-step process**:

### Step 1: FIN (Finish) from Client
- Client wants to close the connection  
- Sends a **FIN packet** to the server

### Step 2: ACK from Server
- Server acknowledges with an **ACK packet**  
- Client enters **FIN_WAIT_2** state

### Step 3: FIN from Server
- Server wants to close the connection too  
- Sends a **FIN packet** to the client

### Step 4: ACK from Client
- Client acknowledges with **ACK**  
- Connection is now closed

**Observed Traffic:**  
- Flags: **FIN, ACK**  
- Usually you see multiple packets marking the close process

| Step | Packet | Source → Destination | Flags | Notes                                                     |
| ---- | ------ | -------------------- | ----- | --------------------------------------------------------- |
| 1    | FIN    | Client → Server      | FIN   | Client wants to close the connection; sequence `x`        |
| 2    | ACK    | Server → Client      | ACK   | Server acknowledges client (`ACK=x+1`)                    |
| 3    | FIN    | Server → Client      | FIN   | Server wants to close connection too; sequence `y`        |
| 4    | ACK    | Client → Server      | ACK   | Client acknowledges server (`ACK=y+1`); connection closed |


---

## 5. Things to See in Packet Captures
- **SYN, SYN-ACK, ACK flags** for handshake  
- **FIN and ACK flags** for connection tear-down  
- Source and destination ports for the session  
- Sequence and acknowledgment numbers to ensure data order  

---

## 6. Common Issues in TCP Connections
- SYN packets sent but no SYN-ACK returned → server unreachable  
- Delayed ACKs causing slow connections  
- Unexpected FIN packets leading to premature disconnections  
- Multiple retransmissions due to packet loss

---

## 7. Learning Outcomes for Undergraduates
By analyzing TCP traffic, students will learn:

- How a TCP connection starts and ends  
- How flags like SYN, ACK, and FIN control communication  
- How sequence numbers and acknowledgments ensure reliability  
- How to interpret packet captures for real connections

---

## 8. Beginner-Friendly References
- [Cloudflare: TCP Explained](https://www.cloudflare.com/learning/networking/tcp/)  
- [TCP Three-Way Handshake Guide](https://www.geeksforgeeks.org/tcp-three-way-handshake/)  
- [Wireshark TCP Analysis Tutorial](https://www.wireshark.org/docs/wsug_html_chunked/ChAdvTCP.html)


# Understanding DHCP: How Computers Get IP Addresses Automatically

## 1. What is DHCP?
**DHCP (Dynamic Host Configuration Protocol)** is a service that automatically gives computers **IP addresses and other network settings** so they can communicate on a network.  

Without DHCP, you would have to **manually set IP addresses** on every computer — which is slow and error-prone.

In a network traffic tool, DHCP is great for beginners to see **how computers request and receive an IP address**.

---

## 2. Where DHCP Works in the Network
- **Network Layer:** Application Layer (top layer where apps like your system network service run)  
- **Transport Protocol:** UDP  
  - Client → Server: UDP port 67  
  - Server → Client: UDP port 68  
- **Client Role:** Computer or device requesting an IP address  
- **Server Role:** DHCP server assigning IP addresses and network settings

---

## 3. Key Components in DHCP
- **DHCP Client:** The computer/device asking for an IP  
- **DHCP Server:** Gives out IP addresses from a pool and provides network info  
- **DHCP Relay (optional):** For larger networks; forwards DHCP messages between clients and servers

---

## 4. Step-by-Step DHCP Operation

### Step 1: DHCP Discover
- The client doesn’t have an IP yet  
- It sends a **broadcast message** asking “Is there a DHCP server?”  

**Observed Traffic:**  
- UDP broadcast from client to network  
- Message type: **DHCP Discover**

---

### Step 2: DHCP Offer
- DHCP server receives the broadcast  
- Picks an available IP from its pool  
- Sends an **offer message** to the client with:  
  - Proposed IP address  
  - Subnet mask  
  - Gateway, DNS servers  
  - Lease time  

**Observed Traffic:**  
- Server → Client, usually broadcast

---

### Step 3: DHCP Request
- Client chooses one of the offers (usually the first it receives)  
- Sends a **request message** back to the server asking to use that IP  

**Observed Traffic:**  
- UDP broadcast from client  
- Message type: **DHCP Request**

---

### Step 4: DHCP Acknowledgment (ACK)
- Server confirms the assignment  
- Client can now configure its IP and other network settings  

**Observed Traffic:**  
- Server → Client  
- Message type: **DHCP ACK**  

At this point, the client is **online and ready to communicate**.

---

## 5. DHCP IP Renewal Process
- IP addresses are leased for a limited time (TTL)  
- **Renewal:** When half the lease time passes, the client tries to renew the IP by sending a **DHCP Request** directly to the server  
- **Rebinding:** If the server doesn’t respond, the client broadcasts a request to any available server  

**Observed Traffic:**  
- Request and ACK messages like the initial assignment, but typically sent directly to the original server

---

## 6. Things to See in Captures
- Multiple message types: **Discover → Offer → Request → ACK**  
- Transaction IDs to match messages  
- IP addresses being assigned dynamically  
- Broadcast messages vs direct unicast messages

---

## 7. Common Fields in DHCP Messages
- **Client MAC Address:** Identifies the client  
- **Offered IP Address:** Proposed IP from server  
- **Subnet Mask:** Network size  
- **Default Gateway:** Router address  
- **Lease Time:** Duration client can use the IP  
- **DNS Server Addresses:** Optional, for name resolution  

---

## 8. Common Problems in DHCP
- IP conflicts if server misconfigured  
- No DHCP server available → client gets APIPA address (`169.254.x.x`)  
- Lease expiry issues causing temporary loss of connectivity  
- Broadcast messages may be blocked by network equipment

---

## 9. What You Will Learn
By analyzing DHCP traffic, beginners will learn:

- How a client gets an IP address automatically  
- The meaning of DHCP message types and their order  
- How IP leases and renewals work  
- How to identify problems in DHCP operations

---

## 10. Beginner-Friendly References
- [Cloudflare: What is DHCP?](https://www.cloudflare.com/learning/networking/dhcp/)  
- [Cisco: Understanding DHCP](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/15-sy/dhcp-15-sy-book/iad-dhcp.html)  
- [IETF RFC 2131 – DHCP](https://www.rfc-editor.org/rfc/rfc2131)


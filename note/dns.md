# Understanding DNS: How Your Computer Finds Websites

## 1. What is DNS?
The **Domain Name System (DNS)** is like the phonebook of the internet. It helps your computer turn **website names** like `www.example.com` into **IP addresses** like `93.184.216.34` that computers can understand.  

Without DNS, you would have to type IP addresses to visit websites instead of names — which would be very hard to remember!

In a network traffic tool, DNS is a great way for beginners to see **how computers talk to each other** when looking up a website.

---

## 2. Where DNS Works in the Network
- DNS works at the **application layer** (the top layer where apps like browsers work)  
- **How it sends messages:**  
  - Usually **UDP on port 53** (fast queries)  
  - Sometimes **TCP on port 53** (bigger responses)  
- **Who does what:**  
  - Your computer is the **DNS client**  
  - DNS servers (recursive, root, TLD, authoritative) do the searching for the IP

---

## 3. Parts of DNS

When your computer looks up a website, it talks to different parts:

- **DNS Client (your computer):** Sends the request  
- **Recursive Resolver:** The first server that starts looking for the answer  
- **Root Server:** Points to the right top-level domain server (like `.com`)  
- **TLD Server:** Points to the server that actually knows the domain  
- **Authoritative Server:** Gives the final IP address

        +------------------+
        |   Your Computer  |
        |   (DNS Client)   |
        +--------+---------+
                 |
                 | DNS Query (UDP/TCP 53)
                 v
        +------------------+
        | Recursive Resolver|
        +--------+---------+
                 |
                 | Query to Root Server
                 v
        +------------------+
        |   Root Server    |
        +--------+---------+
                 |
                 | Points to TLD Server
                 v
        +------------------+
        |    TLD Server    |
        +--------+---------+
                 |
                 | Points to Authoritative Server
                 v
        +------------------+
        | Authoritative DNS|
        +------------------+


---

## 4. Step-by-Step: How DNS Works

### Step 1: Your Computer Asks
- You type a website name into the browser  
- Your computer checks its **cache** first  
- If it doesn’t know the IP, it sends a query

**What you see in traffic:** A DNS query from your computer

---

### Step 2: Resolver Checks
- The query goes to a **recursive resolver** (usually your ISP or Google DNS)  
- Resolver checks its cache  
- If it doesn’t know the answer, it asks other DNS servers

**What you see:** Queries leaving the resolver

---

### Step 3: Root Server Helps
- The resolver asks a **root DNS server**  
- Root server doesn’t know the IP  
- It tells the resolver which **TLD server** to ask

**What you see:** Response with TLD server info

---

### Step 4: TLD Server Responds
- Resolver asks the **TLD server** (like `.com`)  
- TLD server points to the **authoritative server** for the website

**What you see:** Response with authoritative server info

---

### Step 5: Authoritative Server Gives Answer
- Resolver asks the **authoritative server**  
- It responds with the **IP address** for the website

**What you see:** Response with final IP

---

### Step 6: Resolver Returns Answer
- Resolver sends the IP back to your computer  
- Your computer caches it for a while so next time it’s faster

**What you see:** DNS response arriving at your computer

---

## 5. Things You Can See in Captures
- Multiple queries and responses  
- How queries travel from your computer to different servers  
- How caching makes repeated requests faster  
- How each DNS response is labeled with a **transaction ID** to match queries

---

## 6. Common DNS Record Types
- **A:** IPv4 address  
- **AAAA:** IPv6 address  
- **CNAME:** Alias for another domain  
- **NS:** Name server that knows the domain  
- **MX:** Mail server for the domain  

---

## 7. Common Problems in DNS
- Repeated queries because cache expired  
- Slow responses if a server is unreachable  
- Wrong configurations causing **domain not found (NXDOMAIN)**  
- Lots of DNS traffic could mean a misconfiguration or attack

---

## 8. What You Will Learn
By watching DNS traffic, beginners will learn:

- How computers find websites  
- How queries travel through different servers  
- How caching improves speed  
- How to match queries and responses in packet captures

---

## 9. Beginner-Friendly References
- [Cloudflare: What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)  
- [Google Developers: DNS Overview](https://developers.google.com/speed/public-dns/docs/overview)  
- [Simple Explanation of DNS](https://www.cloudflare.com/learning/dns/what-is-dns/)  


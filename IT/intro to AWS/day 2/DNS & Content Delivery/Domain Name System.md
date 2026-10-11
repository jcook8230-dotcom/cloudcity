The **Domain Name System (DNS)** serves as the phonebook of the internet. It is a decentralized, hierarchical system that translates human-readable domain names (like `google.com`) into computer-readable IP addresses (like `142.250.190.46`), allowing your browser to locate and load internet resources.

Understanding DNS requires looking at its structural hierarchy, the server handshake, and core record types.

---

1. The DNS Hierarchy (How Domains Are Structured)

Domain names are organized like an upside-down tree, read from right to left, separated by dots:

```
                  [ . ] (Root Zone)
                    │
         ┌──────────┴──────────┐
      [ .com ]               [ .org ] (Top-Level Domains - TLDs)
         │
    [ google ] (Second-Level Domain)
         │
      [ www ] (Subdomain)
```

- **Root Zone (`.`):** The absolute top of the hierarchy. While invisible in daily browsing, it directs requests to the correct Top-Level Domain servers.
- **Top-Level Domain (TLD):** The suffix at the end of a domain name (e.g., `.com`, `.org`, `.edu`, `.gov`, or country codes like `.uk`).
- **Second-Level Domain:** The unique name you register (e.g., `google` in `google.com`).
- **Subdomain:** A prefix added to a domain to segregate different departments or functions of a website (e.g., `www`, `blog`, or `api`).

---

2. The DNS Resolution Process (The 4-Server Handshake)

When you type a web address into your browser, a lookup process occurs involving four distinct types of servers to track down the correct IP address:

1. **DNS Recursor (Recursive Resolver):** Usually provided by your Internet Service Provider (ISP) or third parties (like Google Public DNS `8.8.8.8`). It acts as a librarian, traveling across the internet to fetch the correct IP address on your behalf.
2. **Root Nameserver:** The first stop for the recursor. It reads the TLD suffix of your request (e.g., `.com`) and tells the recursor where to find the specific TLD Nameserver.
3. **TLD Nameserver:** The second stop. It manages all domains sharing that specific suffix and directs the recursor to the authoritative server hosting that exact domain.
4. **Authoritative Nameserver:** The final destination. This server holds the actual database of DNS records for the domain name. It returns the exact IP address back to the recursor, which delivers it to your browser.

---

3. Core DNS Record Types Compared

Inside an Authoritative Nameserver, domain records are organized into a lookup table by specific types:

|Record Type|Stands For|What It Does|Practical Use Case|
|---|---|---|---|
|**A**|Address|Maps a domain directly to an **IPv4 address**.|Points `example.com` to your web server's IP `192.0.2.1`.|
|**AAAA**|Quad-A|Maps a domain directly to an **IPv6 address**.|Points a domain to a modern IPv6 network address.|
|**CNAME**|Canonical Name|Aliases one domain name to another domain name.|Maps `://example.com` to point to the base `example.com`.|
|**MX**|Mail Exchanger|Specifies the mail servers responsible for receiving email.|Routes emails sent to `@example.com` to Google Workspace or Outlook.|
|**TXT**|Text|Stores arbitrary text notes, often used for security vetting.|Used for domain ownership verification and **SPF/DKIM spam prevention**.|
|**NS**|Name Server|Delegates a DNS zone to use a specific authoritative server.|Tells the internet that AWS Route 53 is managing your records.|

---

4. TTL (Time-To-Live) and Caching

To prevent billions of devices from overwhelming authoritative servers with constant lookups, DNS utilizes aggressive caching.

**Time-To-Live (TTL)** is a numerical value (measured in seconds) attached to every DNS record. It tells recursive resolvers and your operating system exactly how long they are allowed to store and reuse a DNS result locally before they are forced to discard it and fetch a fresh copy from the authoritative server.

- **High TTL (e.g., 86400 seconds / 24 hours):** Great for stable sites; reduces server load and speeds up load times for users.
- **Low TTL (e.g., 300 seconds / 5 minutes):** Essential when migrating servers or updating infrastructure, ensuring users see changes quickly.
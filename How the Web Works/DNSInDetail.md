
# DNS (Domain Name System)

DNS provides a simple way for us to communicate with devices on the internet without remembering complex numbers. Every computer on the internet has its own unique address used for communication, called an IP address.

When you want to visit a website, it's not very convenient to remember a complicated set of numbers. That’s where DNS helps. Instead of remembering something like 104.26.10.229, you can simply remember **website.com**.

## Domain Hierarchy 

### TLD (Top Level Domain)

A TLD is the most right-hand part of a domain name. There are two main types of TLD:

- **gTLD (Generic Top-Level Domain)** – tells the user the general purpose of the domain.  
  Examples: `.com`, `.gov`, `.edu`

- **ccTLD (Country Code Top-Level Domain)** – used for geographical or country-specific purposes.  
  Examples: `.ca`, `.uk`, `.br`



### Second-Level Domain

Taking **GenericWebsite.com** as an example, `.com` is the TLD and `GenericWebsite` is the Second-Level Domain.

When registering a domain name, the second-level domain is limited to 63 characters and can only use:

- Letters a–z  
- Numbers 0–9  
- Hyphens (-)

Rules:
- Cannot start or end with a hyphen  
- Cannot have consecutive hyphens

### Subdomain

A subdomain sits on the left-hand side of the Second-Level Domain and is separated by a period. For example, in **admin.GenericWebsite.com**, the **admin** part is the subdomain.

A subdomain follows the same naming rules as a Second-Level Domain:
- Up to 63 characters per label  
- Can use a–z, 0–9, and hyphens  
- Cannot start or end with a hyphen  

You can use multiple subdomains separated by periods to create longer names, such as **jupiter.servers.GenericWebsite.com**

However, the full domain name (including dots) must be **253 characters or fewer**.

There is no strict limit to the number of subdomains you can create, as long as the total length restriction is respected.


## DNS Record Types

DNS isn't just for websites, and multiple types of DNS records exist.

### A Record

These records resolve a domain name to an IPv4 address, for example 104.26.10.229.

### AAAA Record

These records resolve a domain name to an IPv6 address, for example 2606:4700:20::681a:be5.

### CNAME Record

These records resolve a domain name to another domain name (an alias). For example, GenericWebsite's online shop might use the subdomain **store.genericwebsite.com**, which returns a CNAME record pointing to **shops.shopify.com**. Another DNS request would then be made to **shops.shopify.com** to find its IP address.

### MX Record

These records specify the mail servers responsible for receiving email on behalf of a domain. For example, an MX record response for **genericwebsite.com** might look like **alt1.aspmx.l.google.com**.

MX records also include a priority value. This tells the sending mail server the order in which to try the mail servers. If the main server is unavailable, email can be delivered to a backup server instead.

### TXT Record

TXT records are free-text fields where any text-based data can be stored. TXT records have multiple uses, but some common ones include listing servers that are authorized to send email on behalf of a domain (such as SPF records, which help prevent spam and spoofed email). They can also be used to verify ownership of a domain name when signing up for third-party services.


## Making A Request

What happens when you make a DNS request:

1. **Requesting** – When you request a domain name, your computer first checks its local cache to see if you’ve looked up the address recently. If not, a request is sent to your Recursive DNS Server.

2. **Recursive DNS Server** – A Recursive DNS Server is usually provided by your ISP, but you can also choose a public one (such as Google DNS or Cloudflare DNS). This server also has a cache of recently looked-up domain names.  
If a result is found locally, it is sent back to your computer, and your request ends here (this is common for popular services such as Google, Facebook, and Twitter).  
If the request cannot be found locally, a journey begins to find the correct answer, starting with the internet's root DNS servers.

3. **Root DNS Server** – The root servers act as the DNS backbone of the internet. Their job is to redirect the request to the correct Top-Level Domain (TLD) server depending on the domain.  
For example, if you request **www.genericwebsite.com**, the root server recognizes the TLD `.com` and refers you to the TLD server responsible for `.com` domains.

4. **Authoritative** – The TLD server does not hold the final DNS record but instead knows where to find the authoritative server for the domain. The authoritative server is often called the **nameserver** for the domain.  
For example, the nameservers for **genericwebsite.com** might be **kip.ns.cloudflare.com** and **uma.ns.cloudflare.com**. Domains usually have multiple nameservers for redundancy in case one goes down.

5. **Storing the Domain** – The authoritative DNS server is responsible for storing the DNS records for a particular domain name and where updates to DNS records are made.  
Depending on the record type, the DNS response is sent back to the Recursive DNS Server, where a local copy is cached for future requests, and then relayed back to the original client that made the request.  

DNS records all come with a **TTL (Time To Live)** value. This value, measured in seconds, determines how long the response should be cached before it must be looked up again. Caching reduces the need to perform a full DNS lookup every time you communicate with a server.

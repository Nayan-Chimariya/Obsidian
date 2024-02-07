The process of DNS resolution involves converting a hostname (such as example.com) into a computer-friendly IP address (such as 192.168.1.1).

DNS lookup occurs "behind the scenes" and requires no interaction from the user’s computer apart from the initial request.

## What is a domain name?

A domain name is a string of text that maps to an alphanumeric IP address, used to access a website from client software. In plain English, a domain name is the text that a user types into a browser window to reach a particular website. For instance, the domain name for Google is ‘google.com’.

The actual address of a website is a complex numerical IP address (e.g. 192.0.2.2), but thanks to DNS, users are able to enter human-friendly domain names and be routed to the websites they are looking for. This process is known as a DNS lookup.
## Difference between a domain name and a URL

A uniform resource locator (URL), sometimes called a web address, contains the domain name of a site as well as other information, including the protocol and the path. For example, in the URL `https://cloudflare.com/learning/`, `cloudflare.com` is the domain name, while` https` is the protocol and `/learning/` is the path to a specific page on the website.
## There are 4 DNS servers involved in loading a webpage:

- **DNS recursor** - the _recursor_ is then responsible for making additional requests in order to satisfy the client’s DNS query.

- **Root nameserver** - The _root server_ is the first step in translating (resolving) human readable host names into IP addresses. It serves as a reference to other more specific locations.

- **TLD nameserver** - The _top level domain server_ (TLD)  is the next step in the search for a specific IP address, and it hosts the last portion of a hostname (In example.com, the TLD server is “com”)

- **Authoritative nameserver** - The authoritative nameserver is the last stop in the nameserver query. If the authoritative name server has access to the requested record, it will return the IP address for the requested hostname back to the DNS Recursor that made the initial request.

## The steps in a DNS lookup:

1. A user types `example.com` into a web browser and the query travels into the Internet and is received by a DNS recursive resolver.
2. The resolver then queries a DNS root nameserver (.).
3. The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .NET), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD.
4. The resolver then makes a request to the .com TLD.
5. The TLD server then responds with the IP address of the domain’s nameserver, example.com.
6. Lastly, the recursive resolver sends a query to the domain’s nameserver.
7. The IP address for example.com is then returned to the resolver from the nameserver.
8. The DNS resolver then responds to the web browser with the IP address of the domain requested initially.

Once the 8 steps of the DNS lookup have returned the IP address for `example.com`, the browser is able to make the request for the web page:

1. The browser makes a [[HTTP]] request to the IP address.
2. The server at that IP returns the webpage to be rendered in the browser.

![[DNS lookup.png]]

## DNS Caching
The purpose of caching is to temporarily stored data in a location that results in improvements in performance and reliability for data requests. DNS caching involves storing data closer to the requesting client so that the DNS query can be resolved earlier and additional queries further down the DNS lookup chain can be avoided, thereby improving load times and reducing bandwidth/CPU consumption.

## What is a DNS record?

DNS records (aka zone files) are instructions that live in authoritative DNS servers and provide information about a domain including what IP address is associated with that domain and how to handle requests for that domain. These records consist of a series of text files written in what is known as DNS syntax. DNS syntax is just a string of characters used as commands that tell the DNS server what to do. All DNS records also have a ‘TTL’,  which stands for time-to-live, and indicates how often a DNS server will refresh that record.

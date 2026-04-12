BIND is the open source DNS server used by the majority of DNS servers on the planet.

BIND is distributed by the Internet Systems Consortium, the ISC.

### DNS class
In DNS, every record has three components: name, type, and class.
Class was designed to allow DNS to work across different network types:
![img_3.png](img_3.png)

When DNS was designed in the early 1980s, the internet wasn't the only network around. The class field was a forward-looking design to support multiple network types under one DNS system.

In practice, Chaosnet and Hesiod died out, and the internet (IN) class won entirely. So today:

- Every A, AAAA, MX, CNAME, etc. record is class IN
- dig defaults to IN automatically
- The field is essentially vestigial — it's always IN

####  Why we need dns class?

Imagine it's 1983. You have two separate networks running in your university:

- Chaosnet — MIT's network, with its own addressing, its own protocol
- ARPANET/TCP/IP — what became the internet

These networks are incompatible. A Chaosnet address and an IP address are completely different things.

Now you want one DNS system to serve both. The problem:

"What is the address of mail.mit.edu?"

The answer depends on which network you're asking for:
- On Chaosnet → give me a Chaosnet address
- On TCP/IP → give me an IP address

Without a class field, DNS can't distinguish. So the class was the way to say:

`TCP/IP client asking:`

mail.mit.edu  IN  A  18.72.0.3       ← internet address

`Chaosnet client asking:`

mail.mit.edu  CH  A  MIT-AJAX        ← chaosnet address

Same name, same record type (A), but different class = different answer.

The class let a single DNS server hold records for multiple network types and return the right answer depending on who was asking.

Since Chaosnet died and TCP/IP won, you always ask IN, always get an IP address, and the class field became pointless — but the slot in the record format remains.                         
                  

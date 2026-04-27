# Request-Response Model

## The 5 steps

### 1) Client sends a request
- The client really needs to define what a *request* is, and the backend really needs to understand what a *request* is.
- The data that you send is **not like mail**; it's usually a **continuous stream of data** (commonly over TCP).

### 2) Server parses the request
- The server needs to **parse the data** to find:
  - where the request **starts**
  - where the request **ends**
- Once we parse the request, we can understand the request.

### 3) Server processes the request
- Knowing you received a `GET` request is one thing.
- Executing that request (fetch an API, query the database, etc.) is another thing.
- These are the processing aspects of the request.

### 4) Server sends response back
- Once processing is finished, the server sends a response back to the client.

### 5) Client parses the response and consumes it
- The concept of a response is very similar to a request.
- How does the client know where the response **starts** and where the response **ends**?
- The client parses the response and consumes it.

## Where does serialization come in?

For example, if I have:
- JSON as a payload
- XML as a payload
- Protocol Buffers as a payload

This is actually part of "processing a request" (if you believe it or not), because parsing a request is:
- "Hey, this is where it starts, this is where it ends"
- then you have to **deserialize** whether this content is something I can understand in my programming language (server-side)

But there is a **cost** to deserialization.

Like why do people move from SOAP to XML to JSON REST?
- One reason is the expense of parsing: parsing XML is way higher than parsing JSON.
- Actually parsing JSON is also slow - that's why people move to Protocol Buffers (a quicker parser).

This is where **plain text vs human-readable** comes into the picture:
- JSON is nice: I can look at it and understand it.
- XML is nice: I can look at it and understand it.
- But the cost is **size** and the cost is **parsing**.

So where is it used?
* Web, HTTP, DNS, SSH
* RPC (remote procedure call)
* SQL and Database Protocols 
* APIs (REST/SOAP/GRAPHQL)



DNS: A system that converts domain names (like google.com) into IP addresses so computers can find servers.
HTTP: A protocol that defines how a browser requests data from a server and receives a response.
HTTPS: HTTP with encryption (SSL/TLS) that keeps data safe while traveling between browser and server.
    1 - SSL (Secure Sockets Layer): An older security technology that encrypts data between your browser and a server so it can’t be read by hackers.
    2 - TLS (Transport Layer Security): The modern, improved version of SSL that is more secure and is what HTTPS actually uses today.
SSH: A secure protocol used to remotely access and control servers through command line.


An IP address (Internet Protocol address) is a unique number assigned to every device or server on the internet, like a digital home address. When you open a website, your computer first uses DNS to find the website’s IP address, then sends an HTTP/HTTPS request to that IP, which identifies the exact server hosting the website. That server receives the request, processes it, and sends back a response to your IP, so your browser can show the website. In short, IP is what actually lets data travel to the correct machine on the internet, while DNS just helps you find it and HTTP is the language they use to talk.

RPC (Remote Procedure Call) is a way for your app to ask a server to run a function and send back the result. You don’t manually do all the steps on the frontend—instead, you just call one function, and the server handles everything inside it, like database queries, joins, or calculations, and returns the final output. It is useful when you have complex work that should be done on the backend in one place. REST APIs are used when you simply want to get or update data like users or posts, while RPC is used when you want the server to do some work and give you the final result.

When we deploy a Supabase edge function, it creates a bundle, which means it takes all the code required to run that function and bundles everything into a compact, performant ESZIP format, which is very quick to download and execute.
After bundling, it is uploaded to the Supabase backend, and a URL is created for your edge function.
Now we can invoke this function from our app. This will make a call to that created URL for our edge function.
When we perform any action that invokes the edge function, it sends a request to the edge function’s URL. This request first hits the global API gateway of Supabase, which is responsible for routing the request to the nearest Supabase edge location.

# Request Response Model
1 - Client Sends a request
The Client really need to deffine what a request is and backend realy need to understand waht a request is, because you see, the data that you send (its not like mail), its a continous usually in TCP its a continous
stream of data 
2 - Server Parses the request
that server need to parse the data to look for the start of the request and the end of the request once we parse the reuqest and understand the request.
3 - Server processes the request
and then acutally executing a request is different, if you receive a get request knowing that this is a get request is one thing and executing that request to fetch an API or query the database is anotehr thing so these are the processing aspects of request and the server offcourse 
4 - server sends repsonse back 
once the process is finished it sends response back to the client 
5 - CLient parses the response and consume 
, even the concept of response is very similar to request, how does the client know that this where the response starts and this is where the response ends? and then the client parses the response and consume 

Where does serialization comes in place here? 
for example if i have json as a payload or i have XML as a payload or i have a protocol buffer as a payload , this is actually like processing a request if you beleive it or not, because pasrsing a request 
is just to understand Hey, this is where it starts, this is where it ends, and then you have to deserialize whether this content is something i can understand in my programming language in the server side but htere is a cost to deserialization, like why do people  move from soap to xml to JSON rest? one of the reason is expense of parsing XML is way higher than parsing JSON, acutally parsing JSON is also slow thats why people move to a protocol buffers as a quick parser and this is where plain text versus normal in human readable 
thing comes into the picture, JSON is nice i can look it and understnad it, XML is nice i can look at it and udnersatnd it but hte cost is size, the cost is parsing, so where it is used? 

Overview:
HTTP/1.1, released in 1999, built upon HTTP/1.0 by introducing several important improvements and optimizations, such as support for persistent connections, more efficient caching mechanisms, and better handling of chunked transfer encoding. 
HTTP/1.1 became the de facto standard for web communication and continues to be widely used today.

Key Features of HTTP/1.1:
* Persistent Connections: In HTTP/1.1, the connection between the client and the server remains open after a response, allowing multiple requests and responses to be sent over the same connection. This reduced the overhead of opening new connections for each request.

* Pipelining: HTTP/1.1 supports pipelining, where multiple requests can be sent without waiting for responses. However, it is not widely used because of issues with out-of-order responses.

* Improved Caching: HTTP/1.1 introduced more sophisticated caching mechanisms with headers like Cache-Control, If-Modified-Since, and ETag, allowing better control over how resources are cached and served.

* Host Header: The Host header is mandatory in HTTP/1.1 requests, allowing multiple websites to be hosted on the same IP address. This was essential as virtual hosting became more common.

* Chunked Transfer Encoding: HTTP/1.1 supports chunked transfer encoding, which allows the server to send data in chunks, improving efficiency when the full size of the response is unknown at the start of the transmission.

* Status Codes: HTTP/1.1 introduced new status codes, such as 408 Request Timeout and 413 Payload Too Large, to provide more detailed information about request handling.


Limitations of HTTP/1.1:
1. Head-of-Line Blocking: HTTP/1.1 still suffers from head-of-line blocking when pipelining, meaning if one request is delayed, all subsequent requests are also delayed.

2. No Multiplexing: Despite the persistent connections, HTTP/1.1 cannot send multiple responses simultaneously over a single connection without blocking, which led to inefficiencies in loading resources.


C# 1.1
using System;
using System.Net;
using System.IO;

class HttpRequest
{
    static void Main()
    {
        // Create an HTTP request for a page using HTTP/1.1
        string url = "http://example.com/my-page.html";
        
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
        request.Method = "GET"; // HTTP/1.1 supports methods like GET, POST, PUT, etc.
        request.ProtocolVersion = HttpVersion.Version11; // Specify HTTP/1.1

        // Add headers
        request.Headers.Add("Host", "example.com");
        request.Connection = "keep-alive"; // Keep the connection open for future requests

        // Send the request and get the response
        HttpWebResponse response = (HttpWebResponse)request.GetResponse();
        
        // Read the response content
        StreamReader reader = new StreamReader(response.GetResponseStream());
        string responseText = reader.ReadToEnd();

        // Display the content
        Console.WriteLine("Response from server:");
        Console.WriteLine(responseText);

        // Close the response and reader
        reader.Close();
        response.Close();
    }
}

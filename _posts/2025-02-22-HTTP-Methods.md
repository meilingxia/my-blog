# HTTP Requests
![image](https://github.com/user-attachments/assets/6990f062-d72d-4442-bdbd-062c831b57fb)

![image](https://github.com/user-attachments/assets/5b5ec176-e58e-4dd9-b37d-59fbf203763d)

#### GET
Get information from web server.
| Visiting web | HTTP Request |
| --- | ----------- |
| example.com **/page?id=123** | **GET** **/page?id=123** HTTP/1.1 <br>Host: example.com |

**/page?id=123** Explanation
1. **/page?id=123** → The request target (path + query string):
2. **/page** → The path (the resource being requested).
3. **?id=123** → The query string (extra information sent to the server).

| Visiting web | HTTP Request |
| --- | ----------- |
| example.com **/123** | **GET** **/123** HTTP/1.1 <br>Host: example.com |

**/123** Explanation
1. **/123** → The request target, the path but without query string

#### POST
Send data to the web server.
| Sample | Explanation |
| --- | ----------- |
|**POST** /login HTTP/1.1|First Line <br> /login → The resource (endpoint) we are sending data to.|
|Host: example.com <br> Content-Type: application/x-www-form-urlencoded <br>Content-Length: 25|Headers (Metadata for the request)<br>Content-Type: Specifies the format of the data being sent.|           
|username=admin&password=1234|Request Body (Actual data being sent) <br>username=admin&password=1234 → The login credentials being submitted.|

|Another sample|Expanation|
| --- | ----------- |
|**POST** /submit-comment HTTP/1.1<br>Host: myblog.com <br><br>Content-Type: application/x-www-form-urlencoded<br><br>Content-Length: 36<br><br>name=Alice&comment=Hello+World%21|The client is sending data to /submit-comment on myblog.com. <br><br><br><br> The data is URL-encoded.<br><br> The body contains 36 bytes of data.<br><br>Body, Name = "Alice"<br>comment="Hello World!", %21 is the encoded version of "!".|

#### Q&A with chatgpt
**Question:**
About "Content-Type: application/x-www-form-urlencoded → Specifies the format of the data being sent (URL-encoded form data).", what role does "application" take here?

**Anasswers from chatgpt**
![image](https://github.com/user-attachments/assets/2eb4d9e8-5fe1-4000-997d-985fc1f23eb8)



#### PUSH
**to be updated**

#### DELETE
**to be updated**

*The content of this blog is based on my learning experience on TryHackMe. 
I am a paid member of TryHackme and I use ChatGPT to help me understand the relevant knowledge. 
All articles are based on my personal study summaries and are not direct copies of TryHackMe's official contents.
Instead, these blogs reflect my understanding and organization of the courses.*

*本博客的内容来源于我在 TryHackMe 上的学习经验，我是其付费会员，并使用 ChatGPT 来帮助理解相关知识。
所有文章均基于我个人的学习总结，并非直接复制 TryHackMe 的官方内容，而是我对课程的理解和整理。*

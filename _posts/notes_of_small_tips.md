It'https://crackstation.net/
(which has a database of billions of hash to value results) to see if we can find any matches.


https://www.base64decode.org/

https://www.base64encode.org/

好的，让我用中文解释一下 Base64 编码，以及你提供的两个网站（base64decode.org 和 base64encode.org）的作用：

**什么是 Base64 编码？**

Base64 是一种将二进制数据（例如图像、音频、或其他任何类型的文件）转换成 ASCII 字符串的编码方式。

**为什么需要 Base64 编码？**

* **传输二进制数据：** 有些传输协议（例如电子邮件、HTTP）只能传输文本数据。Base64 编码允许我们将二进制数据转换成文本，以便在这些协议中传输。
* **嵌入数据：** 我们可以将 Base64 编码后的数据直接嵌入到 HTML、CSS 或其他文本文件中，而无需单独的文件。
* **避免字符集问题：** 有些字符在不同的系统或应用程序中可能被错误地解释。Base64 编码使用一组固定的字符，避免了这些问题。

**Base64 编码的工作原理：**

1.  **分组：** 将二进制数据分成 6 位一组。
2.  **转换：** 将每组 6 位转换成一个十进制数（0-63）。
3.  **映射：** 使用一个包含 64 个字符的字符集（A-Z、a-z、0-9、+、/）将每个十进制数映射到一个字符。
4.  **填充：** 如果二进制数据的长度不是 24 位的倍数，则在末尾添加填充字符“=”。

**你提供的两个网站的作用：**

* **base64encode.org：**
    * 这个网站用于将文本或文件编码成 Base64 字符串。
    * 你可以在网站上输入要编码的数据，然后点击“Encode”按钮，网站会生成对应的 Base64 编码。
* **base64decode.org：**
    * 这个网站用于将 Base64 字符串解码成原始的文本或文件。
    * 你可以在网站上输入 Base64 编码的字符串，然后点击“Decode”按钮，网站会还原出原始数据。

**简单来说：**

* Base64 编码就像是一个翻译器，它把计算机看得懂的二进制数据，翻译成人类看得懂的文本。
* 这两个网站，一个负责把普通文本翻译成base64，另一个负责把base64翻译回普通文本。

**应用场景：**

* 在电子邮件中发送附件。
* 在 HTML 中嵌入图像（data URI）。
* 在 Web API 中传输二进制数据。
* 在配置文件中存储二进制数据。

希望这个解释对你有所帮助！





You're right to question how we know it's `/cookie-test` specifically! There are several ways to determine the path of a web resource, especially in a learning or penetration testing context:

**1. Context from the Learning Material:**

* **TryHackMe or similar platforms:** In the TryHackMe room or similar learning environments, the challenge or task description will almost always explicitly tell you the correct URL or path. This is done to guide you and ensure you're focusing on the intended vulnerability. In your case, the previous explanations and the surrounding text specifically state that the page being tested is /cookie-test.
* **Walkthroughs and hints:** If you're stuck, look for walkthroughs, hints, or forum discussions related to the challenge. These resources will often provide the necessary information.

**2. Web Application Discovery (Reconnaissance):**

If you were approaching a real-world scenario or a "black box" test (where you have minimal information), you'd use various techniques to discover web resources:

* **Directory and File Brute-Forcing:**
    * Tools like `ffuf`, `gobuster`, or `dirb` can be used to scan a web server for known or common directories and files.
    * These tools use wordlists to guess potential paths.
    * For example, you could run `ffuf -w wordlist.txt -u http://10.10.26.233/FUZZ` and see what paths return a 200 OK status code.
* **Web Spidering:**
    * Tools like `Burp Suite's spider` or `OWASP ZAP's spider` can automatically crawl a website, following links and discovering new pages.
    * This can reveal hidden directories and files.
* **Manual Exploration:**
    * Simply browsing the website and examining the URL structure can provide clues.
    * Looking at the website's source code (View Page Source) can also reveal hidden links or JavaScript files.
* **Checking robots.txt:**
    * The `robots.txt` file (e.g., `http://10.10.26.233/robots.txt`) can sometimes list directories or files that the website owner wants to prevent search engines from indexing. While it is meant for robots, it can also give hints to attackers.
* **Developer Tools:**
    * Using your browser's developer tools (usually accessed by pressing F12) and looking at the "Network" tab, you can see all the requests and responses made by the website. This can reveal the paths of various resources.

**3. Server Response Analysis:**

* **HTTP Status Codes:** If you try accessing a non-existent path (e.g., `http://10.10.26.233/something-else`), you'll likely get a 404 Not Found error.
* **Response Content:** The content of the server's response can also provide clues. For example, a 403 Forbidden error might indicate that a directory exists, but you don't have permission to access it.

**In summary:**

* In a controlled learning environment, the path is usually provided.
* In a real-world scenario, you'd use a combination of automated and manual techniques to discover web resources.



marblog@customer.acmeitsupport.thm
Marblog12345#

好的，让我们用中文详细解释这个逻辑缺陷的实际案例：

**逻辑缺陷实战：重置密码功能漏洞**

我们将分析 Acme IT 支持网站（[http://10.10.26.233/customers/reset](http://10.10.26.233/customers/reset)）的“重置密码”功能。

1.  **初始步骤：验证邮箱**
    * 首先，网站会要求你输入与账户关联的邮箱地址。
    * 如果输入的邮箱无效，你会收到错误信息：“Account not found from supplied email address”（未找到提供的邮箱对应的账户）。
    * 为了演示，我们使用有效的邮箱地址：robert@acmeitsupport.thm。
    * 然后，网站会进入下一步，要求你输入与该邮箱关联的用户名。

2.  **验证用户名**
    * 如果输入正确的用户名（例如：robert），并点击“Check Username”按钮，你会收到确认信息，提示密码重置邮件将发送到 robert@acmeitsupport.thm。

3.  **漏洞分析：GET 和 POST 混合使用**
    * 你可能会想，这个应用似乎很安全，因为需要同时知道邮箱和用户名，并且重置链接会发送到账户所有者的邮箱。
    * 但是，这个应用在处理请求时存在逻辑缺陷：
        * 在第二步，用户名通过 POST 请求发送到服务器。
        * 邮箱地址通过 GET 请求的查询字符串发送。
    * 我们可以使用 `curl` 命令来模拟这些请求：

    * **Curl Request 1:**
        ```bash
        user@tryhackme$ curl 'http://10.10.26.233/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
        ```
        * `-H 'Content-Type: application/x-www-form-urlencoded'`：设置请求头，告诉服务器我们发送的是表单数据。

4.  **PHP $_REQUEST 变量的缺陷**
    * 网站通过查询字符串（GET）获取用户账户信息，但密码重置邮件的发送地址却使用了 PHP 的 `$_REQUEST` 变量。
    * `$_REQUEST` 是一个数组，包含来自查询字符串（GET）和 POST 请求的数据。
    * **关键问题：** 如果查询字符串和 POST 请求使用了相同的键名（例如：`email`），`$_REQUEST` 优先使用 POST 请求中的值。
    * 因此，我们可以通过在 POST 请求中添加一个 `email` 参数，来控制密码重置邮件的发送地址。

5.  **漏洞利用：篡改邮件发送地址**
    * **Curl Request 2:**
        ```bash
        user@tryhackme$ curl 'http://10.10.26.233/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=marblog@customer.acmeitsupport.thm'
        ```
        * 在这个请求中，我们添加了 `email=attacker@hacker.com` 到 POST 数据中。
        * 由于 `$_REQUEST` 优先使用 POST 数据，密码重置邮件将被发送到 attacker@hacker.com，而不是 robert@acmeitsupport.thm。

6.  **实际操作：获取 Robert 账户的访问权限**
    * 为了完成这个练习，你需要先在 Acme IT 支持网站的客户区创建一个账户。你的账户邮箱格式为 `{username}@customer.acmeitsupport.thm`。
    * 然后，再次运行 Curl Request 2，但这次将 `email` 参数的值设置为你的账户邮箱：
        ```bash
        user@tryhackme:~$ curl 'http://10.10.26.233/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=marblog@customer.acmeitsupport.thm'
        ```
    * 这样，密码重置链接将被发送到你的账户邮箱，并在你的工单中显示。
    * 通过这个链接，你就可以以 Robert 的身份登录，并查看他的工单，其中包含一个 flag。

**总结：**

这个案例展示了如何利用 PHP `$_REQUEST` 变量的特性，通过混合使用 GET 和 POST 请求，篡改密码重置邮件的发送地址，从而获取目标账户的访问权限。这个漏洞的根本原因是应用程序没有正确验证和过滤用户输入，以及对 GET 和 POST 请求的处理不当。


The primary security vulnerability in the code snippet you provided is a **weak and predictable access control mechanism** based solely on the URL's prefix. Here's a breakdown of the problems:

**1. Client-Side Validation (Implied):**

* If this code is executed on the client-side (e.g., in JavaScript within a web browser), it's trivial for an attacker to bypass it. They can simply modify the URL in their browser's address bar or use browser developer tools to alter the JavaScript code.
* Client-side checks should *never* be relied upon for security-sensitive operations.

**2. Simple String Matching:**

* The code uses a basic string comparison (`url.substr(0,6) === '/admin'`). This is highly susceptible to manipulation.
* Consider these scenarios:
    * `/admin-panel` would be blocked, even if intended for admins.
    * `/adminanything` would be allowed.
    * `/admin%20` would be allowed. URL encoding can be used to bypass simple string comparisons.
    * `/Admin` case sensitivity issues.
* It lacks robustness and doesn't account for variations or more complex URL structures.

**3. Lack of Authentication and Authorization:**

* The code only checks the URL. It doesn't verify the user's identity or their permissions.
* An attacker could simply change the URL to `/admin` and gain access, even if they're not a legitimate admin.
* Proper authentication (verifying *who* the user is) and authorization (verifying *what* they're allowed to do) are essential.
* There is no session management.

**4. Location of the code.**

* If this code is located within the web page itself, it is easily viewable by anyone. Therefore, any checks within the page itself are easily bypassed.

**How to Fix It (General Principles):**

1.  **Server-Side Validation:**
    * Perform all access control checks on the server-side, where the user cannot directly manipulate the code.
2.  **Robust Authentication:**
    * Implement a secure authentication mechanism (e.g., using sessions, JWTs, or OAuth) to verify the user's identity.
3.  **Proper Authorization:**
    * Use a role-based access control (RBAC) or attribute-based access control (ABAC) system to manage user permissions.
    * Store user roles or permissions securely in a database or configuration file.
4.  **URL Parsing:**
    * Use a reliable URL parsing library or function to extract and analyze URL components.
    * Avoid simple string comparisons.
5.  **Input Validation:**
    * Validate all user inputs, including URLs, to prevent injection attacks and other vulnerabilities.
6.  **Principle of Least Privilege:**
    * Grant users only the minimum necessary permissions.
7.  **Regular Updates:**
    * Keep your server software and libraries up-to-date to patch known vulnerabilities.

**Example (Conceptual - Python/Flask):**

```python
from flask import Flask, request, session, redirect, url_for

app = Flask(__name__)
app.secret_key = "your_secret_key" #very important to change this.

def is_admin():
    # Check if the user is logged in and has admin role
    if 'username' in session and session['role'] == 'admin':
        return True
    return False

@app.route('/admin/<path:subpath>') #Catch any path after admin
def admin_panel(subpath):
    if is_admin():
        # Admin-specific code
        return f"Admin panel: {subpath}"
    else:
        return redirect(url_for('login')) #redirect to login page.

@app.route('/login')
def login():
    #login logic
    session['username'] = "testuser" #example of setting a session variable.
    session['role'] = "admin" #example of setting a session variable.
    return "logged in"

@app.route('/')
def home():
    return "home page"

if __name__ == '__main__':
    app.run(debug=True)

```

In this conceptual flask example, the server side checks the session variables, that are only set upon login. The client cannot set these variables. The server also uses a path variable, and will catch any path after /admin. This prevents the /adminanything problem.



当然，我会用中文解释这个 `curl` 命令：

这个 `curl` 命令的作用是向一个特定的网址（`http://10.10.27.136/customers/reset`）发送一个 HTTP 请求，模拟用户在网页上提交一个表单。它的目的是重置一个用户的密码，这个用户由电子邮件地址和用户名指定。

下面是命令的详细分解：

* **`curl`**: 这是一个命令行工具，用于发送 HTTP 请求。
* **`'http://10.10.27.136/customers/reset?email=robert%40acmeitsupport.thm'`**:
    * 这是要请求的网址。
    * `http://10.10.27.136` 是服务器的 IP 地址。
    * `/customers/reset` 是服务器上处理密码重置的路径。
    * `?email=robert%40acmeitsupport.thm` 是 URL 查询字符串，它传递了一个名为 `email` 的参数，值为 `robert@acmeitsupport.thm`。请注意，`%40` 是 `@` 符号的 URL 编码。
* **`-H 'Content-Type: application/x-www-form-urlencoded'`**:
    * `-H` 选项用于添加 HTTP 请求头。
    * `Content-Type: application/x-www-form-urlencoded` 指定了请求体的 MIME 类型。这意味着数据将以 URL 编码的格式发送，就像 HTML 表单提交的数据一样。
* **`-d 'username=robert'`**:
    * `-d` 选项用于发送 POST 数据。
    * `username=robert` 指定了一个名为 `username` 的参数，值为 `robert`。

**总结一下：**

这个命令模拟了以下操作：

1.  用户在网页上输入了他们的电子邮件地址 `robert@acmeitsupport.thm` 和用户名 `robert`。
2.  然后，用户点击了一个“重置密码”按钮。
3.  浏览器将这些数据以 `application/x-www-form-urlencoded` 格式发送到服务器上的 `/customers/reset` 路径。
4.  服务器接收到请求，并尝试重置 `robert@acmeitsupport.thm` 用户的密码。

**安全注意事项：**

* 这种密码重置机制可能存在安全漏洞，例如：
    * 如果服务器没有正确验证电子邮件地址和用户名，攻击者可能会重置其他用户的密码。
    * 如果服务器没有使用安全的密码重置令牌，攻击者可能会猜测或窃取令牌。
    * 如果服务器没有对请求的来源做验证，就会发生CSRF（跨站请求伪造）攻击。
* 如果服务器没有对请求的速率做限制，攻击者可能会进行暴力破解。

因此，在实际应用中，密码重置功能需要进行严格的安全检查和保护。



#### ffuf

**will display all the ouput**
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.78.180/customers/signup -mr "username already exists"

**will filter with Status code = 200**
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.143.64/customers/signup -mr "username already exists" -mc 200


The ffuf tool and wordlist come pre-installed on the AttackBox or can be installed locally by downloading it from https://github.com/ffuf/ffuf.

Let's break down this `ffuf` command, which is commonly used in web application security testing, especially for fuzzing.

**`ffuf`**

* This is the command itself. `ffuf` stands for "Fuzz Faster U Fool." It's a web fuzzer designed for speed and efficiency.

**`-w /usr/share/wordlists/SecLists/Usernames/Names/names.txt`**

* `-w` specifies the wordlist to use.
* `/usr/share/wordlists/SecLists/Usernames/Names/names.txt` is the path to a file containing a list of usernames. `SecLists` is a very popular collection of wordlists for security testing. This part of the command tells ffuf to use every line of the names.txt file as input.

**`-X POST`**

* `-X` specifies the HTTP method to use. In this case, it's `POST`. This indicates that the request will send data to the server. This is important because signup forms typically use the POST method.

**`-d "username=FUZZ&email=x&password=x&cpassword=x"`**

* `-d` specifies the data to be sent in the POST request.
* `username=FUZZ&email=x&password=x&cpassword=x` is the data itself.
    * `username=FUZZ`: This is the crucial part. `FUZZ` is a placeholder that `ffuf` will replace with each username from the wordlist. So, it will try `username=john`, `username=jane`, etc.
    * `email=x&password=x&cpassword=x`: These are static values. The fuzzer is only testing the username field, so the other fields are given arbitrary values. In a real world attack, or more in depth pentest, you may fuzz all of the fields.

**`-H "Content-Type: application/x-www-form-urlencoded"`**

* `-H` specifies an HTTP header.
* `Content-Type: application/x-www-form-urlencoded` tells the server that the data being sent is in the standard URL-encoded format, which is typical for HTML forms.

**`-u http://10.10.78.180/customers/signup`**

* `-u` specifies the target URL.
* `http://10.10.78.180/customers/signup` is the URL of the signup page that's being tested.

**`-mr "username already exists"`**

* `-mr` specifies a match regex.
* `"username already exists"` is the regular expression to match.
    * This tells `ffuf` to look for the string "username already exists" in the server's response. If it finds this string, it means that the username being tested is already in use. This is how the fuzzer determines which usernames are valid.

**In summary:**

This `ffuf` command is designed to brute-force usernames on a signup page. It sends POST requests to the signup URL, trying each username from the provided wordlist. It then checks the server's response for the message "username already exists" to identify valid usernames. This is a common technique for enumerating user accounts.





```
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.78.180/customers/login -fc
```

This `ffuf` command is designed to perform a brute-force attack on a login form. Let's break it down:

**`ffuf`**

* As before, this is the web fuzzer tool.

**`-w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2`**

* `-w` specifies the wordlists.
* `valid_usernames.txt:W1`: This indicates that the `valid_usernames.txt` file will be used as a wordlist, and the placeholder `W1` will be replaced with each username from this file.
* `/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2`: This indicates that the `10-million-password-list-top-100.txt` file will be used as a wordlist, and the placeholder `W2` will be replaced with each password from this file.
* The colon and W1 and W2 are used to designate which wordlist will populate which part of the post request. This allows you to use multiple wordlists at the same time.

**`-X POST`**

* `-X` specifies the HTTP method, which is `POST` in this case. Login forms typically use POST to send credentials.

**`-d "username=W1&password=W2"`**

* `-d` specifies the data to be sent in the POST request.
* `username=W1&password=W2`: This is the data itself.
    * `username=W1`: `W1` will be replaced with usernames from the `valid_usernames.txt` wordlist.
    * `password=W2`: `W2` will be replaced with passwords from the `10-million-password-list-top-100.txt` wordlist.
    * This sets up ffuf to test every combination of username and password from the two wordlists.

**`-H "Content-Type: application/x-www-form-urlencoded"`**

* `-H` specifies the HTTP header.
* `Content-Type: application/x-www-form-urlencoded`: This tells the server that the data is in the standard URL-encoded format.

**`-u http://10.10.78.180/customers/login`**

* `-u` specifies the target URL, which is the login page.

**`-fc`**

* `-fc` this stands for "filter status code". By default ffuf displays all status codes. If you want to only see successful logins, or failed logins you can filter them. Without any numbers following the -fc flag, it filters out all 403 status codes. 403 status codes mean "forbidden". This is useful because many login pages return 403 when a login fails.

**In summary:**

This `ffuf` command performs a brute-force attack on the login form at `http://10.10.78.180/customers/login`. It tries every combination of usernames from `valid_usernames.txt` and passwords from `10-million-password-list-top-100.txt`. By using the `-fc` flag, it filters out 403 errors, so that the results are easier to read.



#### 好的，以下是关于“自动化发现”的中文翻译：

**什么是自动化发现？**

自动化发现是指使用工具来发现内容，而不是手动进行。这个过程是自动化的，因为它通常包含对Web服务器的数百、数千甚至数百万个请求。这些请求检查网站上是否存在文件或目录，从而使我们能够访问以前不知道存在的资源。这个过程是通过使用一种名为“字典”的资源实现的。

**什么是字典？**

字典只是包含常用单词长列表的文本文件；它们可以涵盖许多不同的用例。例如，密码字典将包含最常用的密码，而我们在这里寻找的是内容，因此我们需要一个包含最常用目录和文件名的列表。一个优秀的字典资源（预安装在THM AttackBox上）是[https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)，由Daniel Miessler维护。

**自动化工具**

尽管有许多不同的内容发现工具可用，它们各有特点和缺点，但我们将介绍三个预安装在我们的攻击机上的工具：ffuf、dirb和gobuster。

在AttackBox上执行以下三个命令，以Acme IT Support网站为目标，并查看你得到的结果。

**关键术语解释：**

* **Automated Discovery (自动化发现):** 使用工具自动查找网站上的隐藏文件和目录的过程。
* **Wordlists (字典):** 包含大量单词或短语的文本文件，用于自动化发现或密码破解等任务。
* **AttackBox:** 在TryHackMe环境中提供的攻击机，预装了各种渗透测试工具。
* **ffuf, dirb, gobuster:** 用于Web目录和文件发现的常用工具。




#### S3 Buckets的中文翻译：

**S3存储桶**

S3存储桶是亚马逊AWS提供的一种存储服务，允许人们在云端保存文件，甚至静态网站内容，并通过HTTP和HTTPS访问。文件所有者可以设置访问权限，使文件公开、私有甚至可写。有时，这些访问权限设置不正确，无意中允许访问本不应公开的文件。S3存储桶的格式是http(s)://{名称}.s3.amazonaws.com，其中{名称}由所有者决定，[例如tryhackme-assets.s3.amazonaws.com](https://www.google.com/search?q=%E4%BE%8B%E5%A6%82tryhackme-assets.s3.amazonaws.com)。S3存储桶可以通过多种方式发现，例如在网站的页面源代码、GitHub存储库中查找URL，甚至可以自动化该过程。一种常见的自动化方法是使用公司名称，后跟常见术语，例如{名称}-assets、{名称}-www、{名称}-public、{名称}-private等。

**关键术语解释：**

* **S3 Buckets (S3存储桶):** 亚马逊AWS提供的云存储服务，用于存储各种类型的数据。
* **AWS (Amazon Web Services):** 亚马逊网络服务，提供云计算服务的集合。
* **HTTP (Hypertext Transfer Protocol):** 超文本传输协议，用于在网络上传输数据的协议。
* **HTTPS (Hypertext Transfer Protocol Secure):** 安全超文本传输协议，HTTP的加密版本。
* **Access Permissions (访问权限):** 控制用户或应用程序对资源访问级别的设置。
* **Static Website Content (静态网站内容):** 不随用户交互而变化的网站内容，例如HTML、CSS和JavaScript文件。
* **Page Source (页面源代码):** 网页的HTML代码。
* **GitHub Repositories (GitHub存储库):** 用于托管软件开发项目的在线存储库。




#### github
You can use GitHub's search feature to look for company names or website names to try and locate repositories belonging to your target. Once discovered, you may have access to source code, passwords or other content that you hadn't yet found.

#### Wayback Machine

The Wayback Machine (https://archive.org/web/) is a historical archive of websites that dates back to the late 90s. You can search a domain name, and it will show you all the times the service scraped the web page and saved the contents. This service can help uncover old pages that may still be active on the current website.

#### Wappalyzer (https://www.wappalyzer.com/)
is an online tool and browser extension that helps identify what technologies a website uses, such as frameworks, Content Management Systems (CMS), payment processors and much more, and it can even find version numbers as well.


/robots.txt

![image](https://github.com/user-attachments/assets/57fee8da-8159-4382-b9d7-05809a968791)

favicon

![image](https://github.com/user-attachments/assets/d6eabfee-805f-4755-b16f-7bc6bcf44976)

sitemap.xml

![image](https://github.com/user-attachments/assets/7eba1341-cc05-4bb8-8cde-ceadc7f7ead7)

https://en.wikipedia.org/wiki/Google_hacking



## tips of google

useful tips to help you search more effectively using Google:

1. 引号，精确搜索，"global warming effects"
2. 减号，排除，apple -fruit
3. 通配符，"a * saved is a * earned"
4. 指定网站，site:example.com tips
5. 类似网站，related:nytimes.com
6. 或者，vacation tips OR holiday advice
7. 数字范围，camera $50..$100
	Around(3)
8. 名词解释，或者定义，define:photosynthesis
9. 查看网页的缓存版本 cache:example.com
10. 标题(单个关键字)，intitle:garden
11. 多个关键字出现在标题，或者链接, 或者正文里。 allintitle:education online， allinurl:education onlin, allintext:
12. 指定文件类型report filetype:pdf，doc
13. 地理位置，election location:australia
14. 网站信息，info:example.com
15. 天气，时间 of a place,  weather espoo， time espoo
16. 计算，10 USD to EUR or 45*12
17. Use inanchor: for Specific Anchor Text: Finds pages with links containing specific anchor text. Example: inanchor:"click here".
18. Location-Based Searches: Set a location preference in 'settings' to get country-specific results without adding location in every search.
19. Find Pages Linking to a URL: Use link: to see who’s linking to a specific page. Example: link:nytimes.com.
20. Explore with Google Books: Use books.google.com to search for books; useful for in-depth resource material.
21. Find Public Data: Simply search for "[topic] data" to find datasets; Google curates and often presents them at a glance.
22. Search by Date: Use Google’s date filter features in “Tools” to specify custom date ranges for results.
23. Use Google Trends: Visit trends.google.com to compare searches and see what’s trending over time.
24. Translate Quickly: w2 “translate [word] to [language]” directly into the search bar for fast translations.
25. Exclude Sensitive Content: Use safe search filters in settings for more family-friendly results.
26. Search on Mobile with Voice: Don't type, speak your query by clicking the microphone icon in mobile Google search.
27. Check Stock Prices: Simply type a stock ticker symbol like TSLA for Tesla to get the latest stock price.
28. Check Movie Showtimes: Enter the name of a movie and a zip/postal code to find showtimes in your area.
29. Discover Quick Recipes: Type “recipe” followed by a dish name for a selection of recipes with ratings.
30. Use Stopwatch or Timer: Type “stopwatch” or “timer” to start these tools directly in your browser.
31. Check Flight Statuses: Enter a flight number directly into Google search to get the departure and arrival times.
32.  以图搜图（反向图片搜索）Use Google Images to perform a reverse image search.
33. 从特定新闻来源获取新闻结果
34. 学术文章、期刊和专利
35. 高级搜索
谷搜索页面提供了一些额外的选项，可以更精确地控制搜索结果。以下是如何使用谷歌高级搜索的步骤：

1. **访问谷歌高级搜索页面**：
   - 打开浏览器，搜索“谷歌高级搜索”或直接访问 [谷歌高级搜索页面](https://www.google.com/advanced_search)。

2. **输入搜索条件**：
   - 页面上有多个输入框和选项，帮助你定义更具体的搜索标准：
     - **包含所有这些词的网页**：在这个框中输入必须同时存在的多个关键词。
     - **包含这个确切词组的网页**：输入需要完整匹配的短语或句子。
     - **含有任一这些词的网页**：输入多个可能的关键词，结果会包含其中任意一个。
     - **不包含这些词的网页**：输入你想排除的词，结果将不包含这些词。

3. **设置其他搜索过滤器**：
   - 你可以通过各种下拉菜单进一步过滤结果：
     - **语言**：选择结果限制于特定的语言。
     - **区域**：选择结果来源于特定国家或地区。
     - **最后更新时间**：限制结果为最近更新的页面。
     - **网站或域**：限制结果显示来自特定网站或顶级域名（如 .edu, .gov）。
     - **文件类型**：选择特定的文件格式，如 PDF、Word 文档等。
     - **使用权**：选择使用权限，如可自由使用或共享的内容。

4. **执行搜索**：
   - 根据设置好的条件，点击页面底部的“高级搜索”按钮，谷歌会根据这些更加具体的条件返回搜索结果。

通过这样的高级搜索功能，你可以更高效地找到更贴合需求的搜索结果，有效节省时间和精力。

![image](https://github.com/user-attachments/assets/c7c9f45f-acf1-48b3-80b0-fe0551a1f06d)

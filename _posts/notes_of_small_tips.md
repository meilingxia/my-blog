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

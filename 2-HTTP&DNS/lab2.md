# <center>实验报告</center>

### <center>实验二 HTTP与DNS</center>

### <center>Lab1 HTTP & DHS</center>

##### <p align="right">罗晏宸</br>PB17000297</br>2019.9.23</p>

***
## 实验目的

1. **研究学习HTTP协议**  
	1. 认识学习基础请求响应的报文交互  
	2. 熟悉HTTP报文格式与内容  
	3. 利用HTTP协议取回大型HTML文件  
	4. 利用HTTP取回嵌有对象的HTML文件  
	5. HTTP授权与安全

***
## 实验内容

### 基础请求响应(GET/response)报文交互

1. 在Wireshark中对捕获的分组应用HTTP协议过滤   

2. 浏览给定网址  
	http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html
	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\1_0.png)
	
3. 捕获如下分组  

     1. HTTP GET 报文  
        ```http
        GET /wireshark-labs/HTTP-wireshark-file1.html HTTP/1.1\r\n
        Host: gaia.cs.umass.edu\r\n
        Connection: keep-alive\r\n
        Upgrade-Insecure-Requests: 1\r\n
        User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3\r\n
        Accept-Encoding: gzip, deflate\r\n
        Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
        \r\n
        ```
        ![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\1_1.png)
        
     2. HTTP 响应报文  
     	```http
     	HTTP/1.1 200 OK\r\n
     	Date: Mon, 23 Sep 2019 01:58:39 GMT\r\n
     	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
     	Last-Modified: Sun, 22 Sep 2019 05:59:01 GMT\r\n
     	ETag: "80-5931dfff61479"\r\n
     	Accept-Ranges: bytes\r\n
     	Content-Length: 128\r\n
     	Keep-Alive: timeout=5, max=100\r\n
     	Connection: Keep-Alive\r\n
     	Content-Type: text/html; charset=UTF-8\r\n
     	\r\n
     	```
     	```html
     	<html>\n
     	Congratulations.  You've downloaded the file \n
     	http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html!\n
     	</html>\n
     	```
     	
     	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\1_2.png)  

4. 阅读分组具体内容，对实验问题的回答如下
	1. 本地浏览器运行的HTTP版本是1.1，服务器运行HTTP 1.1  
	2. 由内容`Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n`可知，浏览器显示可从服务器接收英文(en-US)和中文(zh-CN, zh)  
	3. 本机IP地址为`114.214.173.138`，服务器IP地址为`128.119.245.12`  
	4. 从服务器返回的状态码为`200`  
	5. 由内容`Last-Modified: Sun, 22 Sep 2019 05:59:01 GMT\r\n`可知，取回的HTML文件最后修改时间为格林威治时间2019年9月22日5:59:01  
	6. 由内容`File Data: 128 bytes`可知，返回浏览器的内容大小为128字节  
	7. 有部分没有出现在列表中的条目标题，比如`Connnection: `等  


### 条件请求响应(GET/response)报文交互  

1. 清除浏览器缓存  

2. 设置Wireshark捕获  

3. 浏览给定网址
	http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file2.html
	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\2_0.png)
	
4. 刷新网页

5. 捕获如下分组
     1. HTTP请求报文
  	```http
  	GET /wireshark-labs/HTTP-wireshark-file2.html HTTP/1.1\r\n
  	Host: gaia.cs.umass.edu\r\n
  	Connection: keep-alive\r\n
  	Upgrade-Insecure-Requests: 1\r\n
  	User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
  	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3\r\n
  	Accept-Encoding: gzip, deflate\r\n
  	Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
  	\r\n
  	```

     2. HTTP响应报文
  	```http
  	HTTP/1.1 200 OK\r\n
  	Date: Mon, 23 Sep 2019 04:03:15 GMT\r\n
  	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
  	Last-Modified: Sun, 22 Sep 2019 05:59:01 GMT\r\n
  	ETag: "173-5931dfff60ca9"\r\n
  Accept-Ranges: bytes\r\n
  	Content-Length: 371\r\n
  [Content length: 371]
  	Keep-Alive: timeout=5, max=100\r\n
  Connection: Keep-Alive\r\n
  	Content-Type: text/html; charset=UTF-8\r\n
  	\r\n
  	```
	
  	```html
  	\n
  	<html>\n
  	\n
  	Congratulations again!  Now you've downloaded the file lab2-2.html. <br>\n
  	This file's last modification date will not change.  <p>\n
  	Thus  if you download this multiple times on your browser, a complete copy <br>\n
  	will only be sent once by the server due to the inclusion of the IN-MODIFIED-SINCE<br>\n
  	field in your browser's HTTP GET request to the server.\n
  	\n
  	</html>\n
  	```
  	
  	
     3. HTTP请求报文
  	```http
  	GET /wireshark-labs/HTTP-wireshark-file2.html HTTP/1.1\r\n
  	Host: gaia.cs.umass.edu\r\n
  	Connection: keep-alive\r\n
  	Cache-Control: max-age=0\r\n
  	Upgrade-Insecure-Requests: 1\r\n
  	User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
  	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3\r\n
  Accept-Encoding: gzip, deflate\r\n
  	Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
  If-None-Match: "173-5931dfff60ca9"\r\n
  	If-Modified-Since: Sun, 22 Sep 2019 05:59:01 GMT\r\n
  \r\n
  	```

     4. HTTP响应报文
  	```http
  	HTTP/1.1 304 Not Modified\r\n
  	Date: Mon, 23 Sep 2019 04:03:19 GMT\r\n
  	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
  	Connection: Keep-Alive\r\n
  	Keep-Alive: timeout=5, max=98\r\n
  	ETag: "173-5931dfff60ca9"\r\n
  	\r\n
  	```

  ![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\2.png)

6. 阅读分组具体内容，对实验问题的回答如下

  8. 在第一次请求报文中，相关内容没有出现

  9. 在第一次的响应报文中，服务器显式地返回了html文件内容

  10. 内容`If-Modified-Since: Sun, 22 Sep 2019 05:59:01 GMT\r\n`出现于第二次请求报文  

  11. 第二次响应报文的状态码为`304`，响应短语为`Not Modified`，意为在上次请求响应之后，内容没有修改，因此这次响应报文不再显式地返回文件内

  

### 取回长文档

1. 清除浏览器缓存  

2. 设置Wireshark捕获  

3. 浏览给定网址
	http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html
	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\3_0.png)
	
4. 捕获如下分组

     1. HTTP请求报文
        ```http
        GET /wireshark-labs/HTTP-wireshark-file3.html HTTP/1.1\r\n
        Host: gaia.cs.umass.edu\r\n
        Connection: keep-alive\r\n
        Upgrade-Insecure-Requests: 1\r\n
        User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3\r\n
        Accept-Encoding: gzip, deflate\r\n
        Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
        \r\n
        ```
     
        ![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\3_1.png)
     
     2. HTTP响应报文
        ```http
        HTTP/1.1 200 OK\r\n
        Date: Mon, 23 Sep 2019 06:51:50 GMT\r\n
        Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
        Last-Modified: Mon, 23 Sep 2019 05:59:01 GMT\r\n
        ETag: "1194-593321dccac20"\r\n
        Accept-Ranges: bytes\r\n
        Content-Length: 4500\r\n
        [Content length: 4500]
        Keep-Alive: timeout=5, max=100\r\n
        Connection: Keep-Alive\r\n
        Content-Type: text/html; charset=UTF-8\r\n
        \r\n
        ```
        ```html
        <html><head> \n
        <title>Historical Documents:THE BILL OF RIGHTS</title></head>\n
        \n
        \n
        <body bgcolor="#ffffff" link="#330000" vlink="#666633">\n
        <p><br>\n
        </p>\n
        <p></p><center><b>THE BILL OF RIGHTS</b><br>\n
          <em>Amendments 1-10 of the Constitution</em>\n
        </center>\n
        \n
        <p>The Conventions of a number of the States having, at the time of adopting\n
        the Constitution, expressed a desire, in order to prevent misconstruction\n
        or abuse of its powers, that further declaratory and restrictive clauses\n
        should be added, and as extending the ground of public confidence in the\n
        Government will best insure the beneficent ends of its institution; </p><p>  Resolved, by the Senate and House of Representatives of the United\n
        States of America, in Congress assembled, two-thirds of both Houses concurring,\n
        that the following articles be proposed to the Legislatures of the several\n
        States, as amendments to the Constitution of the United States; all or any\n
        of which articles, when ratified by three-fourths of the said Legislatures,\n
        to be valid to all intents and purposes as part of the said Constitution,\n
        namely:    </p><p><a name="1"><strong><h3>Amendment I</h3></strong></a>\n
        \n
        <p></p><p>Congress shall make no law respecting an establishment of\n
        religion, or prohibiting the free exercise thereof; or\n
        abridging the freedom of speech, or of the press; or the\n
        right of the people peaceably to assemble, and to petition\n
        the government for a redress of grievances.\n
        \n
        </p><p><a name="2"><strong><h3>Amendment II</h3></strong></a>\n
        \n
        <p></p><p>A well regulated militia, being necessary to the security\n
        of a free state, the right of the people to keep and bear\n
        arms, shall not be infringed.\n
        \n
        </p><p><a name="3"><strong><h3>Amendment III</h3></strong></a>\n
        \n
        <p></p><p>No soldier shall, in time of peace be quartered in any house,\n
        without the consent of the owner, nor in time of war, but\n
        in a manner to be prescribed by law.\n
        \n
        </p><p><a name="4"><strong><h3>Amendment IV</h3></strong></a>\n
        \n
        <p></p><p>The right of the people to be secure in their persons, houses,\n
        papers, and effects, against unreasonable searches and seizures,\n
        shall not be violated, and no warrants shall issue, but upon\n
        probable cause, supported by oath or affirmation, and\n
        particularly describing the place to be searched, and the\n
        persons or things to be seized.\n
        \n
        </p><p><a name="5"><strong><h3>Amendment V</h3></strong></a>\n
        \n
        <p></p><p>No person shall be held to answer for a capital, or otherwise\n
        infamous crime, unless on a presentment or indictment of a grand\n
        jury, except in cases arising in the land or naval forces,\n
        or in the militia, when in actual service in time of war\n
        or public danger; nor shall any person be subject for the\n
        same offense to be twice put in jeopardy of life or limb;\n
        nor shall be compelled in any criminal case to be a witness\n
        against himself, nor be deprived of life, liberty, or property,\n
        without due process of law; nor shall private property be\n
        taken for public use, without just compensation.\n
        \n
        </p><p><a name="6"><strong><h3>Amendment VI</h3></strong></a>\n
        \n
        <p></p><p>In all criminal prosecutions, the accused shall enjoy the right\n
        to a speedy and public trial, by an impartial jury of the state\n
        and district wherein the crime shall have been committed, which\n
        district shall have been previously ascertained by law, and\n
        to be informed of the nature and cause of the accusation;\n
        to be confronted with the witnesses against him; to have\n
        compulsory process for obtaining witnesses in his favor,\n
        and to have the assistance of counsel for his defense.\n
        \n
        </p><p><a name="7"><strong><h3>Amendment VII</h3></strong></a>\n
        \n
        <p></p><p>In suits at common law, where the value in controversy shall\n
        exceed twenty dollars, the right of trial by jury shall be\n
        preserved, and no fact tried by a jury, shall be otherwise\n
        reexamined in any court of the United States, than according\n
        to the rules of the common law.\n
        \n
        </p><p><a name="8"><strong><h3>Amendment VIII</h3></strong></a>\n
        \n
        <p></p><p>Excessive bail shall not be required, nor excessive fines\n
        imposed, nor cruel and unusual punishments inflicted.\n
        \n
        </p><p><a name="9"><strong><h3>Amendment IX</h3></strong></a>\n
        \n
        <p></p><p>The enumeration in the Constitution, of certain rights, shall\n
        not be construed to deny or disparage others retained by the people.\n
        \n
        </p><p><a name="10"><strong><h3>Amendment X</h3></strong></a>\n
        \n
        <p></p>\n
        <p>The powers not delegated to the United States by the Constitution, nor prohibited \n
          by it to the states, are reserved to the states respectively, or to the people.</p>\n
        </body></html>
       ```
       
       ![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\3_2.png)

  	

5. 阅读分组具体内容，对实验问题的回答如下

	12. 浏览器发送了1个请求报文，在响应报文的第203、204、205与206分组中包含了相关内容 

	​	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\3_3.png)

	13. 在响应报文的第203分组中包含了状态码和与请求报文相关的状态短语

	14. 状态码为`200`，短语为`OK`
	15. 共计4861字节



### 嵌有对象的HTML文档

1. 清除浏览器缓存  

2. 设置Wireshark捕获  

3. 浏览给定网址
	http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html

	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\4_0.png)

4. 捕获如下分组

     1. HTTP请求报文
	```http
	GET /wireshark-labs/HTTP-wireshark-file4.html HTTP/1.1\r\n
	Host: gaia.cs.umass.edu\r\n
	Connection: keep-alive\r\n
	Upgrade-Insecure-Requests: 1\r\n
	User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3\r\n
	Accept-Encoding: gzip, deflate\r\n
	Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
	\r\n
	```

     2. HTTP响应报文
	```http
	HTTP/1.1 200 OK\r\n
	Date: Mon, 23 Sep 2019 13:45:01 GMT\r\n
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
	Last-Modified: Mon, 23 Sep 2019 05:59:01 GMT\r\n
	ETag: "2ca-593321dccfa41"\r\n
	Accept-Ranges: bytes\r\n
	Content-Length: 714\r\n
	Keep-Alive: timeout=5, max=100\r\n
	Connection: Keep-Alive\r\n
	Content-Type: text/html; charset=UTF-8\r\n
	\r\n
	```
	```html
	<html>\n
	<head>\n
	<title>Lab2-4 file: Embedded URLs</title>\n
	<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1">\n
	</head>\n
	\n
	<body bgcolor="#FFFFFF" text="#000000">\n
	\n
	<p>\n
	<img src="http://gaia.cs.umass.edu/pearson.png" WIDTH="70" HEIGHT="41" > </p>\n
	<p>This little HTML file is being served by gaia.cs.umass.edu. \n
	It contains two embedded images. <br> The image above, also served from the \n
	gaia.cs.umass.edu web site, is the logo of our publisher, Pearson. <br>\n
	The image of our 5th edition book cover below is stored at, and served from, the www server caite.cs.umass.edu:</p>\n
	<p align="left"><img src="http://manic.cs.umass.edu/~kurose/cover_5th_ed.jpg" width="168" height="220"></p>\n
	</body>\n
	</html>\n
	```

     3. HTTP请求报文
     
		```http
		GET /pearson.png HTTP/1.1\r\n
		Host: gaia.cs.umass.edu\r\n
		Connection: keep-alive\r\n
		User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
		Accept: image/webp,image/apng,image/*,*/*;q=0.8\r\n
		Referer: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html\r\n
		Accept-Encoding: gzip, deflate\r\n
		Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
		\r\n
		```

     4. HTTP请求报文
     
		```http
		GET /~kurose/cover_5th_ed.jpg HTTP/1.1\r\n
		Host: manic.cs.umass.edu\r\n
		Connection: keep-alive\r\n
		User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
		Accept: image/webp,image/apng,image/*,*/*;q=0.8\r\n
		Referer: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html\r\n
		Accept-Encoding: gzip, deflate\r\n
		Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
		\r\n
		```

     5. HTTP响应报文
     
		```http
		HTTP/1.1 200 OK\r\n
		Date: Mon, 23 Sep 2019 13:45:02 GMT\r\n
		Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
		Last-Modified: Sat, 06 Aug 2016 10:08:14 GMT\r\n
		ETag: "cc3-539645c7f1ee7"\r\n
		Accept-Ranges: bytes\r\n
		Content-Length: 3267\r\n
		Keep-Alive: timeout=5, max=99\r\n
		Connection: Keep-Alive\r\n
		Content-Type: image/png\r\n
		\r\n
		```

5. 阅读分组具体内容，对实验问题的回答如下

	1. 浏览器发送了3个请求报文，都是向128.119.245.12发送的  
	2. 由于两个响应报文并非同时，因此浏览器是依序下载这两张图片的  

### HTTP授权  

1. 清除浏览器缓存  

2. 设置Wireshark捕获  

3. 浏览给定网址
	http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file5.html
	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\5_0_0.png)

4. 键入用户名`wireshark-students `与密码`network`

	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\5_0_1.png)

5. 捕获如下分组
	1. HTTP请求报文

		```http
		GET /wireshark-labs/protected_pages/HTTP-wireshark-file5.html HTTP/1.1\r\n
		Host: gaia.cs.umass.edu\r\n
		Connection: keep-alive\r\n
		Upgrade-Insecure-Requests: 1\r\n
		User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
		Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3\r\n
		Accept-Encoding: gzip, deflate\r\n
		Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
		\r\n
		```

		

	2. HTTP响应报文

		```http
		HTTP/1.1 401 Unauthorized\r\n
		Date: Mon, 23 Sep 2019 15:32:01 GMT\r\n
		Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
		WWW-Authenticate: Basic realm="wireshark-students only"\r\n
		Content-Length: 381\r\n
		Keep-Alive: timeout=5, max=100\r\n
		Connection: Keep-Alive\r\n
		Content-Type: text/html; charset=iso-8859-1\r\n
		\r\n
		```

		```html
		<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">\n
		<html><head>\n
		<title>401 Unauthorized</title>\n
		</head><body>\n
		<h1>Unauthorized</h1>\n
		<p>This server could not verify that you\n
		are authorized to access the document\n
		requested.  Either you supplied the wrong\n
		credentials (e.g., bad password), or your\n
		browser doesn't understand how to supply\n
		the credentials required.</p>\n
		</body></html>\n
		```

		

	3. HTTP请求报文

		```http
		GET /wireshark-labs/protected_pages/HTTP-wireshark-file5.html HTTP/1.1\r\n
		Host: gaia.cs.umass.edu\r\n
		Connection: keep-alive\r\n
		Authorization: Basic d2lyZXNoYXJrLXN0dWRlbnRzOm5ldHdvcms=\r\n
		Credentials: wireshark-students:network
		Upgrade-Insecure-Requests: 1\r\n
		User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.87 Safari/537.36\r\n
		Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3\r\n
		Accept-Encoding: gzip, deflate\r\n
		Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7\r\n
		\r\n
		```

		

	4. HTTP响应报文

		```http
		HTTP/1.1 200 OK\r\n
		Date: Mon, 23 Sep 2019 15:32:12 GMT\r\n
		Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16 mod_perl/2.0.10 Perl/v5.16.3\r\n
		Last-Modified: Mon, 23 Sep 2019 05:59:01 GMT\r\n
		ETag: "84-593321dcd1d69"\r\n
		Accept-Ranges: bytes\r\n
		Content-Length: 132\r\n
		Keep-Alive: timeout=5, max=100\r\n
		Connection: Keep-Alive\r\n
		Content-Type: text/html; charset=UTF-8\r\n
		\r\n
		```

		```html
		\n
		<html>\n
		\n
		This page is password protected!  If you're seeing this, you've downloaded the page correctly <br>\n
		Congratulations!\n
		</html>
		```

	![](D:\private\File\课程相关\计算机网络\Labs\2-HTTP&DNS\5_1.png)

	

6. 阅读分组具体内容，对实验问题的回答如下
	18. 对于首次请求，服务器的响应为`401 Unauthorized`，意为未授权

	19. 第二次请求访问包含了如下的内容

		```http
		Authorization: Basic d2lyZXNoYXJrLXN0dWRlbnRzOm5ldHdvcms=\r\n
		Credentials: wireshark-students:network
		```

		提供了服务器要求的凭据  

		

## 实验总结

<p>作为本学期计算机网络课程的第一次观察实验，通过对于Wireshark软件的尝试与摸索，掌握了其基本功能及部分使用方法，包括捕获分组、查看分组头部细节、打印输出捕获结果等。进一步地，通过一个简单HTTP协议的例子，观察了实际分组的细节，回顾了已学习的相关知识。经过本次入门实验，引入了本学期观察实验的重要工具Wireshark，为今后的实验学习与实践提供了背景与工具。</p>  
## 附
本报告中出现的所有设计与测试源代码文件以及相关截图与照片可见[GitHub@lyc0930](https://github.com/lyc0930/Wireshark-Labs)

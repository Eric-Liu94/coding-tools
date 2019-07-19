# HTTP Client

文档地址: [https://www.jetbrains.com/help/go/http-client-in-product-code-editor.html](https://www.jetbrains.com/help/go/http-client-in-product-code-editor.html)

## 实时模板

默认提供了一些实时模板: `gtrp`, `gtr`, `ptr`, `ptrp`, `mptr`, `fptr`

```http request

### gtrp

GET http://localhost:80/api/item?id=99
Accept: application/json

### gtr

GET http://localhost:80/api/item
Accept: application/json

### ptr 

POST http://localhost:80/api/item
Content-Type: application/json

{}

### ptrp

POST http://localhost:80/api/item
Content-Type: application/x-www-form-urlencoded

id=99&content=new-element

### mptr

POST http://localhost:80/api/item
Content-Type: multipart/form-data; boundary=WebAppBoundary

--WebAppBoundary
Content-Disposition: form-data; name="field-name"

field-value
--WebAppBoundary--

### fptr

POST http://localhost:80/api/item
Content-Type: multipart/form-data; boundary=WebAppBoundary

--WebAppBoundary
Content-Disposition: form-data; name="field-name" filename="file.txt"

< ./relative/path/to/local_file.txt
--WebAppBoundary--

```

## 环境变量

首先要定义环境变量文件: `http-client.env.json`或`rest-client.env.json`, 当然也可以定义`http-client.private.env.json`和`rest-client.private.env.json`文件, 后者是私有文件, 主要用于存放一些用户密码之类比较隐私的内容, 如果前后两者文件都出现, 默认后者会覆盖前者, 后者也不建议放到版本控制工具中.

`http-client.env.json`的文件内容类似于这样: 

```json
{
    "development": {
        "host": "localhost",
        "id-value": 12345,
        "username": "",
        "password": "",
        "my-var": "my-dev-value"
    },
    "production": {
        "host": "example.com",
        "id-value": 6789,
        "username": "",
        "password": "",
        "my-var": "my-prod-value"
    }
}
``` 

在`xxx.http`文件中使用环境变量:

```http request
GET http://{{host}}/api/item?id=99
Accept: application/json
``` 

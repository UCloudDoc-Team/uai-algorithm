

# FAQ

## 1. 图片文件的API请求总是返回body格式不正确，可能是什么原因？

图片文件的body要求是multipart/form-data格式，很有可能请求的body并非该格式。该格式是一种高效传输二进制内容的http body格式，并非只将Content-Type强行设置为multipart/form-data，而是要将body的参数按照该格式组织。

## 2. 我有非常高的并发需求，如何处理？

可通过官网、热线等方式联系我们工作人员。


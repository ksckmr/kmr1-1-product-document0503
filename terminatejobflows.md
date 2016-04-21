## TerminateJobFlows


* **功能描述**

　　释放指定的一个或者多个集群。当集群释放时，尚未完成的作业将被取消，集群所使用的云主机都将被释放，但如果集群设置了日志归集功能（创建集群时给出了LogUri），则所有日志都会被完整的上传至KS3。
  
　　请求允许释放的最大集群数量为10。集群释放是一个异步操作，请求会立即返回，根据集群的配置，可能需要5-20分钟才能完全释放掉集群所有的资源，比如云主机实例。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考2.2[公共参数](gong_gong_can_shu.md)
  
　　**JobFlowIds.member.N**
  
　　　　需要释放的集群ID列表。
　　　　类型：String列表
　　　　长度限制：最小0个，最大10个
　　　　是否必须：是
    
返回参数

　　返回结果不包含任何字段

错误信息

　　关于所有操作使用的通用错误信息，参考2.4通用错误信息

　　InternalServerError
　　　　当KMR服务出现内部错误时出现该错误信息类型
　　　　HTTP状态码：500
    
　　BadRequest
　　　　当用户输入信息有误时出现该错误信息
　　　　HTTP状态码：400

样例

　　请求样例

```
POST / HTTP/1.1
Content-Type: application/json
X-Ksc-Target: ElasticMapReduce_V1.TerminateJobFlows
{
    "JobFlowIds": ["26e6d8af-18e2-49b6-b7d1-040dfb170b3b"]
}```


　　返回样例
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 2
{}```


3.3 SetTerminationProtection
功能描述
设置集群释放保护锁。保护集群和云主机不会因为用户干预（控制台、API调用等）而被释放。
如果集群设置了自动释放功能，而且所有作业运行完毕，则集群将不受释放保护功能的影响，可以自动释放。
如果想释放开启了释放保护锁的集群，则必须要先调通此API，将释放保护设置为false，然后释放集群。
请求参数
关于所有操作使用的通用参数信息，请参考2.2公共参数
JobFlowIds.member.N
需要释放的集群ID列表。
类型：String列表
长度限制：最小0个，最大10个
是否必须：是
TerminationProtected
指示是否开启释放保护功能的布尔值。
类型：Boolean
是否必须：是
返回参数
返回结果不包含任何字段
错误信息
关于所有操作使用的通用错误信息，参考2.4通用错误信息
InternalServerError
当KMR服务出现内部错误时出现该错误信息类型
HTTP状态码：500
BadRequest
当用户输入信息有误时出现该错误信息
HTTP状态码：400

样例
请求样例
POST / HTTP/1.1
Content-Type: application/json
X-Ksc-Target: ElasticMapReduce_V1.SetTerminationProtection
{
    "JobFlowIds": ["26e6d8af-18e2-49b6-b7d1-040dfb170b3b"],
    "TerminationProtected": true
}

返回样例
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 2
{}
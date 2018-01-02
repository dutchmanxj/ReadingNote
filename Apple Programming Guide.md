## 阅读Apple Notification的心得体会
Apple的Notification主要分类本地通知和远端通知(remote Notification)。其中本地通知主要是通过系统层面的控制来展示到前端界面，而Remote Notification需要APP这边推送通知的平台接入苹果统一的推送服务 _Apple Push Notification service_ (APNs) 
下面是一个简单的示意图
![img](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Art/remote_notif_simple_2x.png)
这张图上面的Provider是开发者自己需要部署的消息推送后台，Provider按照约定接入APNs以后，就能够使用部署的后台进行远端消息的推送。

为了推送一条消息，Provider需要经过一个如下的流程：
1. 按照Apple官方给出的[推送格式规则](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CreatingtheNotificationPayload.html#//apple_ref/doc/uid/TP40008194-CH10-SW1)构筑内容，并构建一个包含通知内容的JSON字典；
2. 将通知内容,全局唯一token和其他需要传递的信息放进HTTP请求。
3. 最后将这个包含了令牌证书或者密码凭证的通过一个持久安全的通道发送给APNs。


### 关于APNs的一点新的体会
这里主要谈谈这次完整了解APNs相关服务后，发现之前没有正确理解的问题。
APNs提供的服务包括QoS，存储和转发，合并通知。QoS不用说了，是保证通信安全的一个标准。而这里的存储和转发有一点细节的问题，在Provider已经将Notification发送给APNs时，如果APNs发现目标用户设备处于下线状态，则会将这条通知存储一段时间，在用户处于上线转台的时候立马推送给用户。这里的存储有一个特性，该服务只会存储最新的通知，这就导致了对一个处于下线状态的用户再次推送通知会导致之前的通知(下线状态收到的)会被丢弃掉。同时，如果超过一定的时间，APNs会把之前保存的通知全部丢弃。
APNs还提供了合并多调通知的功能。具体的操作方法是在发送HTTP请求的时候，有一个名为 _apns-collapse-id_ 的字段，APNs会自动将该字段取值相同的Notification合并成一条再推送给设备。

### APNs的安全措施
为了保证APNs服务的可靠性，APNs强制使用端到端服务，加密验证以及双层认证。
双层认证分别为：
* 连接认证
* 设备令牌认证

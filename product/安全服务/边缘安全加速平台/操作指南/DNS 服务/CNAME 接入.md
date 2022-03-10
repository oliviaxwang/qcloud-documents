在 CNAME 接入方式下，用户无需将 DNS 解析权转移给 EdgeOne，只需添加记录（子域名）并选定相应的代理模式，在 DNS 解析商处添加指定的 CNAME 记录，即可接入 EdgeOne 安全/加速服务。




### 添加记录（子域名接入）

在CNAME 接入方式下，通过添加记录来为该站点的子域名接入相应的服务。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/teo) ，在左侧菜单栏中，单击 **DNS 服务**。
2. 在 DNS 服务页面，选择所需站点，单击**切换为 CNAME 接入模式** > **确定**。
>?切换至 CNAME 接入需要验证站点所有权，如果您已 [验证过站点](https://cloud.tencent.com/document/product/1552/70789)，则会直接完成切换。
>
![](https://qcloudimg.tencent-cloud.cn/raw/5b7671cb8671c27369c2717cac53a7e3.png)

### 记录类型及记录值

在 CNAME 接入下，记录类型和记录值代表的意义和 [NS 接入](https://cloud.tencent.com/document/product/1552/70825)有所不同：

 - 记录类型：表示源站的类型。
 - 记录值：代表源站地址。
<table>
<thead>
<tr>
<th>记录类型</th>
<th>记录值示例</th>
<th>用途说明</th>
</tr>
</thead>
<tbody><tr>
<td>A</td>
<td>8.8.8.8</td>
<td>对应主机记录（子域名）将回源到一个 IPv4 源站，源站地址为 8.8.8.8</td>
</tr>
<tr>
<td>AAAA</td>
<td>2400:cb00:2049:1::a29f:f9</td>
<td>对应主机记录（子域名）将回源到一个 IPv6 源站，源站地址为 2400:cb00:2049:1::a29f:f9，EdgeOne 默认支持双栈回源</td>
</tr>
<tr>
<td>CNAME</td>
<td>www.origin.com</td>
<td>对应主机记录（子域名）将回源到一个域名源站，源站地址为 www.origin.com</td>
</tr>
</tbody></table>


#### 主机记录
主机记录相当于子域名的前缀，假设当前的站点为 `edgeone.com` ，则常见的主机记录有：

| 主机记录值 | 说明                                          |
| ---------- | --------------------------------------------- |
| @          | 直接解析根域名 edgeone.com                    |
| www        | 常见主机记录，解析域名为 www.edgeone.com      |
| mail       | 解析域名为 mail.edgeone.com，通常用于邮件服务 |
| *          | 泛解析，匹配其他所有域名 *.edgeone.com        |



#### 代理模式

CNAME 接入方式支持以下三种服务（代理）模式，更多详情请参见 [代理模式](https://cloud.tencent.com/document/product/1552/70786)。
- 关闭代理
- 代理加速
- 安全加速



#### CNAME

选中不同代理模式，系统将指定不同的 CNAME 后缀，用户需在 DNS 服务商处添加指定的 CNAME 记录。



#### HTTPS 证书

CNAME 接入方式下，系统不提供 EdgeOne 通用证书。需要手动为每个子域名关联证书，方可正常使用 HTTPS 服务。



#### 负载均衡联动

如果用户想要更复杂的回源配置，需要开启[负载均衡]()。开启负载均衡后，对应子域名的记录将置灰，所有源站配置都必须在负载均衡配置。

![](https://qcloudimg.tencent-cloud.cn/raw/ea889d3b90ff1765f474c0bc1b3d86cc.png)

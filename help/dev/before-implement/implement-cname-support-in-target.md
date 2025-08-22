---
keywords: 客户关怀， cname，证书计划，规范名称， cookie，证书， amc， adobe管理的证书， digicert，域控制器验证， dcv，客户关怀2
description: 使用[!UICONTROL Adobe Client Care]在 [!DNL Adobe Target] 中实施CNAME （规范名称）支持以处理广告阻止问题。
title: 如何在Target中使用CNAME？
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: f894122217529cb40369c003a3b4ed5419fb0505
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---

# CNAME和Target

有关使用[!DNL Adobe Client Care]在[!DNL Adobe Target]中实现CNAME （规范名称）支持的说明。 使用CNAME处理广告阻止问题或与ITP相关的（智能防跟踪）Cookie策略。 使用CNAME时，会调用客户拥有的域，而不是Adobe拥有的域。

## 请求Target中的CNAME支持

1. 确定您的SSL证书所需的主机名列表（请参阅下面的常见问题解答）。

1. 对于每个主机名，请在DNS中创建一个指向常规[!DNL Target]主机名`clientcode.tt.omtrdc.net`的CNAME记录。

   例如，如果您的客户端代码为“cnamecustomer”，而建议的主机名为`target.example.com`，则您的DNS CNAME记录将类似于：

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >在此步骤完成之前，Adobe的证书颁发机构DigiCert无法颁发证书。 因此，在此步骤完成之前，Adobe无法完成您对CNAME实施的请求。

1. [填写此表单](assets/FPC_Request_Form.xlsx)，并在您[打开请求CNAME支持的Adobe客户关怀票证](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=zh-Hans&#reference_ACA3391A00EF467B87930A450050077C)时包含此表单：

   * [!DNL Adobe Target]客户端代码：
   * SSL证书主机名（示例： `target.example.com target.example.org`）：
   * SSL证书购买者(强烈推荐Adobe，请参阅常见问题解答)：Adobe/客户
   * 如果客户正在购买证书(也称为“自带证书”(BYOC))，请填写以下其他详细信息：
      * 证书组织（示例：Example Company Inc）：
      * 证书组织单位（可选，例如：营销）：
      * 证书国家/地区（例如：美国）：
      * 证书所在州/地区（示例：加利福尼亚）：
      * 证书城市（示例：圣何塞）：

1. 如果Adobe正在购买证书，Adobe将与DigiCert合作以购买证书并将其部署到Adobe的生产服务器上。

   如果客户正在购买证书(BYOC)，Adobe客户关怀团队会向您发送证书签名请求(CSR)。 通过您选择的证书颁发机构购买证书时，请使用CSR 。 颁发证书后，将证书副本和任何中间证书发送到Adobe客户关怀团队以进行部署。

   Adobe客户关怀会在您的实施准备就绪时通知您。

1. 将`serverDomain` [文档](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain)更新为新的CNAME主机名，并在您的at.js配置中将`overrideMboxEdgeServer`设置为`false` [文档](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver)。

## 常见问题解答

以下信息回答了有关在Target中请求和实施CNAME支持的常见问题：

### 我可以提供我自己的证书（自带证书或BYOC）吗？

您可以提供自己的证书。 但是，Adobe不建议这样做。 如果Adobe购买并控制证书，则Adobe和您都更轻松地管理SSL证书生命周期。 SSL证书必须每年续订。 因此，Adobe客户关怀团队每年都必须与您联系，才能及时获取新证书。 有些客户可能难以及时生成续订的证书。 当证书过期时，由于浏览器拒绝连接，您的[!DNL Target]实施会受损。

>[!WARNING]
>
>如果您请求[!DNL Target]自带证书CNAME实施，则需每年向Adobe客户关怀团队提供续订证书。 在Adobe部署续订的证书之前，允许您的CNAME证书过期，会导致您的特定[!DNL Target]实施中断。

### 我的新SSL证书需要多久才能过期？

所有Adobe购买的证书有效期为一年。 有关详细信息，请参阅[DigiCert关于1年期证书](https://www.digicert.com/blog/position-on-1-year-certificates)的文章。

### 我应该选择哪些主机名？ 每个域应选择多少主机名？

Target CNAME实施仅要求SSL证书和客户的DNS中的每个域使用一个主机名。 Adobe建议每个域使用一个主机名。 某些客户出于其自身的用途（例如，在暂存环境中测试）需要每个域提供更多主机名，这是受支持的。

大多数客户都会选择类似`target.example.com`的主机名。 Adobe建议遵循此做法，但最终将由您来做出选择。 请勿请求现有DNS记录的主机名。 这样做会导致冲突并延迟解决[!DNL Target] CNAME请求的时间。

### 我已经有了Adobe Analytics的CNAME实施，我可以使用相同的证书或主机名吗？

否，[!DNL Target]需要单独的主机名和证书。

### 我当前的[!DNL Target]实施是否会受ITP 2.x影响？

Apple智能防跟踪(ITP) 2.3版引入了其CNAME遮蔽缓解功能，此功能能够检测[!DNL Target]个CNAME实现并将Cookie过期时间减少到7天。 当前[!DNL Target]没有ITP的CNAME遮蔽缓解解决方法。 有关ITP的更多信息，请参阅[Apple智能防跟踪(ITP) 2.x](../before-implement/privacy/apple-itp-2x.md)。

### 部署我的CNAME实施时，可能会出现哪种服务中断？

部署证书时没有服务中断（包括证书续订）。

但是，在将[!DNL Target]实施代码（ at.js中的`serverDomain`）中的主机名更改为新的CNAME主机名(`target.example.com`)后，Web浏览器会将回访访客视为新访客。 回访访客的配置文件数据丢失，因为旧主机名(`clientcode.tt.omtrdc.net`)下的上一个Cookie不可访问。 由于浏览器安全模型，无法访问上一个Cookie。 此中断仅在初次切换到新CNAME时发生。 证书续订的效果并不相同，因为主机名不会更改。

### 我的CNAME实施使用什么密钥类型和证书签名算法？

默认情况下，所有证书均为RSA SHA-256，密钥为RSA 2048位。 应通过[!UICONTROL Customer Care]显式请求大于2048位的密钥大小。

### 如何验证我的CNAME实施是否已准备好进行流量？

使用以下命令集(在macOS或Linux命令行终端中，使用bash和curl >=7.49)：

1. 将此bash函数复制并粘贴到您的终端中，或者将该函数粘贴到bash启动脚本文件（通常为`~/.bash_profile`或`~/.bashrc`）中，以便该函数在终端会话间可用：

   +++ 查看详细信息

   ```bash {line-numbers="true"}
    function adobeTargetCnameValidation {
   
     local hostname="$1"
   
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="41 42 44 45 46 47 48"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local poolDomain="pool.data.adobedc.net"
     local shards=5
     local shardsFoundCount=0
     local shardsFound=""
     local shardsFoundOutput=""
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2)"
     local curlVersionRequired=7.49
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local cnameExists=""
     local endToEndTestSucceeded=""
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local currShard="${region}-${poolDomain}"
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         shardsFound+=" $currShard"
   
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundCount=$((shardsFoundCount+1))
           shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
         else
           shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
         fi
   
         shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
   
         if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
         fi
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
   
     local dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
       fi
     fi
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
           if [ -n "$cnameExists" ]; then
             echo
           else
             echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
               "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
           fi
           endToEndTestSucceeded=true
         else
           echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
             "unexpected response from $url -- "
           if [ -n "$cnameExists" ]; then
             echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
           else
             echo "the required DNS CNAME record is missing, see above"
           fi
         fi
       else
         echo -n "$failure $hostname FAILED TLS validation for region $region -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
             "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
           echo ""
           echo "$horizontalRule"
           echo "$curlResult" | sed 's/^/    /g'
           echo "$horizontalRule"
           echo ""
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     done
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, see SSL Shopper:"
         echo ""
         echo "    $info  $sslShopperUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       echo ""
     fi
   
     echo
     echo "$horizontalRule"
     echo
   }
   ```

   +++

1. 粘贴以下命令（将`target.example.com`替换为您的主机名）：

   ```adobeTargetCnameValidation target.example.com```

如果实施已准备就绪，您将看到如下所示的输出。 重要部分是所有验证状态行都显示`✅`而不是`🚫`。 每个Target边缘CNAME分区都应显示`CN=target.example.com`，这与所请求证书上的主要主机名匹配（此输出中未打印证书上的其他SAN主机名）。

    +++查看详细信息
    
    &quot;&#39;bash {line-numbers=&quot;true&quot;}
    $ adobeTargetCnameValidation
    target.example.com=====================================Adobe Target CNAME实施验证主机名target.example.com：
    ✅ target.example.com通过DNS CNAME验证
    ✅ target.example.comtarget.example.com通过TLS和HTTP响应验证IRL1
    ✅区域IND1
    ✅的TLS和HTTP响应验证target.example.com通过区域SIN
    ✅的TLS和HTTP响应验证target.example.com通过区域OR
    ✅的TLS和HTTP响应验证target.example.com通过区域SYD
    ✅的TLS和HTTP响应验证target.example.com通过区域VA
    ✅的TLS和HTTP响应验证target.example.comtarget.example.com target.example.com target.example.com target.example.com target.example.com target.example.com target.example.com target.example.com通过区域TYO的分片验证：===== 
    ✅ [edge shard： IRL1-pool.data.adobedc.net] =====✅*过期日期： Feb 20 23
    59 2026 GMT:59:*颁发者： C=US； O=DigiCert Inc； CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *主题： C=US； ST=California； L=San Jose； O=Adobe Systems Incorporated； CN=target.example.com===== 
     [edge shard： IND1-pool.data.adobedc.net] =====✅*过期日期： Feb 20 23
    59 2026 GMT:59:*颁发者： C=US； O=DigiCert Inc； CN=DigiCert Global G2 TLS RSA SHA256 202202020 CA CN=target.example.com===== 
     [edge shard： SIN-pool.data.adobedc.net] =====
    *到期日期： Feb 20 23✅59 2026 GMT
    *颁发者： C=US； O=DigiCert Inc； CN=DigiCert Global Cert tls RSA SHA256 2020 CA1:59:*主题： C=US； ST=California； L=San Jose； O=Adobe Systems Incorporated； CN=target.example.com===== 
     [edge shard： OR-pool.data.adobedc.net] =====
    *到期日期： Feb 20 23✅59 2026 GMT
    *颁发者： C=US； O=US digiCert Inc； CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1:59:*主题： C=US； ST=California； L=San Jose； O=Adobe Systems Incorporated； CN=target.example.com===== 
     [edge shard： SYD-pool.data.adobedc.net] =====
    *过期日期： Feb0233&lbrace;359 2026 GMT✅*颁发者： C=US； O=DigiCert Inc； CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *主题： C=US； ST=California； L=San Jose； O=Adobe Systems Incorporated； CN=target.example.com===== :59: [edge shard： VA-pool.data.adobedc.net] =====
    *到期日期：Feb 20 23
    59 2026 GMT✅*发行者：C=US；O=DigiCert Inc；CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *主题：C=US；ST=California；L=San Jose；O=Adobe Systems Incorporated；CN TARGET=target.example.com===== :59: [edge shard： TYO-pool.data.adobedc.net] =====
    *过期日期： Feb 20 23
    59 2026 GMT✅*颁发者： C=US； O=DigiCert Inc； CN=DigiCert Global G2 TLS RSA SHA256 20 CA1
    *主体： C=US； ST l=San Jose； O=Adobe Systems Incorporated； CN=target.example.com==========================================================有关其他TLS/SSL验证，请参阅SSL购物者：    :59: https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com要检查全球的DNS传播，请参阅whatsmydns.net：    
     DNS A记录：     https://whatsmydns.net/#A/target.example.com
     +++DNS CNAME记录： https://whatsmydns.net/#CNAME/target.example.com🔎“🔎
    🔎
    
    
    

>[!NOTE]
>
>如果此验证命令在DNS验证时失败，但您已经进行了必要的DNS更改，则可能需要等待DNS更新完全传播。 DNS记录具有关联的[TTL （生存时间）](https://en.wikipedia.org/wiki/Time_to_live#DNS_records)，它规定这些记录的DNS回复的缓存过期时间。 因此，您可能需要至少等待与TTL一样长的时间。 您可以使用`dig target.example.com`命令或[G Suite Toolbox](https://toolbox.googleapps.com/apps/dig/#CNAME)查找您的特定TTL。 要检查全球范围内的DNS传播，请参阅[whatsmydns.net](https://whatsmydns.net/#CNAME)。

### 如何将选择退出链接与 CNAME 配合使用

如果您使用的是CNAME，则选择退出链接应包含“client=`clientcode`参数，例如：
`https://my.cname.domain/optout?client=clientcode`。

将`clientcode`替换为您的客户端代码，然后添加要链接到[选择退出URL](privacy/privacy.md)的文本或图像。

## 已知限制

* 当您具有CNAME和at.js 1.x时，QA模式无粘性，因为它基于第三方Cookie。 解决方法是将预览参数添加到您导航到的每个URL中。 当您具有CNAME和at.js 2.x时，QA模式具有粘滞性。
* 使用CNAME时，[!DNL Target]调用的Cookie标头大小更有可能增加。 Adobe建议将Cookie大小保持在8 KB以下。

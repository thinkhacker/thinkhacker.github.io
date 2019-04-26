---
layout: post
title: "聊天APP红包设计之Java实现"
category:
- Android
- Java
- 红包实现
- 聊天APP 
tags: ["红包","聊天APP"]
---


* content
{:toc}


<!-- more -->
<!-- TOC -->
# 数据格式
xml数据格式

```xml
<?xml version="1.0" encoding="utf-8"?>
<xml> 
  <sign><![CDATA[E1EE61A91C8E90F299DE6AE075D60A2D]]></sign>  
  <billno><![CDATA[0010010404201411170000046545]]></billno>  
  <send_id><![CDATA[888]]></send_id>  
  <send_name><![CDATA[send_name]]></send_name>  
  <send_time><![CDATA[10000097]]></send_time>
  <receiver_id><![CDATA[onqOjjmM1tad-3ROpncN-yUfa6uI]]></receiver_id>  
  <total_amount><![CDATA[200]]></total_amount>  
  <total_num><![CDATA[1]]></total_num>  
  <type><![CDATA[1]]></type>  
  <wishing><![CDATA[恭喜发财]]></wishing>  
  <client_ip><![CDATA[127.0.0.1]]></client_ip>  
  <act_name><![CDATA[新年红包]]></act_name>  
  <remark><![CDATA[新年红包]]></remark>  
  <scene_id><![CDATA[PRODUCT_2]]></scene_id>
  <nonce_str><![CDATA[50780e0cca98c8c8e814883e5caa672e]]></nonce_str>  
  <risk_info>posttime%3d123123412%26clientversion%3d234134%26mobile%3d122344545%26deviceid%3dIOS</risk_info> 
</xml>
```
JSON数据
```json
{
    "sign": "E1EE61A91C8E90F299DE6AE075D60A2D",
    "billno": "0010010404201411170000046545",
    "send_id": "888",
    "send_name": "send_name",
    "send_time": "10000097",
    "receiver_id": "onqOjjmM1tad-3ROpncN-yUfa6uI",
    "total_amount": "200",
    "total_num": "1",
    "type": "1",
    "wishing": "恭喜发财",
    "client_ip": "127.0.0.1",
    "act_name": "新年红包",
    "remark": "新年红包",
    "scene_id": "PRODUCT_2",
    "nonce_str": "50780e0cca98c8c8e814883e5caa672e",
    "risk_info": "posttime%3d123123412%26clientversion%3d234134%26mobile%3d122344545%26deviceid%3dIOS" 
}
```

# Java实现

## 红包实体

``` java
package xxx.xxx.xxx.entity;

import com.thoughtworks.xstream.annotations.XStreamAlias;

/**
 * <p>红包请求类/子商户模式<p/></br>
 *
 * @author LanChaoHui
 * @date 2018-07-01 20:20
 * @since 1.0
 */
public class RedPackEntity {
    /**
     * 随机字符串,不长于32位
     */
    @XStreamAlias("nonce_str")
    private String nonceStr;
    /**
     * 签名
     */
    @XStreamAlias("sign")
    private String sign;
    /**
     * 商户订单号
     */
    @XStreamAlias("mch_billno")
    private String mchBillNo;
    /**
     * 商户号
     */
    @XStreamAlias("mch_id")
    private String mchId;
    /**
     * 子商户号
     */
    @XStreamAlias("sub_mch_id")
    private String subMchId;
    /**
     * 服务商号微信公众号的APPID
     */
    @XStreamAlias("wxappid")
    private String wxAppid;
    /**
     * 子商号的公众号的APPID
     */
    @XStreamAlias("msgappid")
    private String msgAppid;
    /**
     * 红包发送者名称
     */
    @XStreamAlias("send_name")
    private String sendName;
    /**
     * 接收红包的用户
     */
    @XStreamAlias("re_openid")
    private String reOpenid;
    /**
     * 付款金额,单位分
     */
    @XStreamAlias("total_amount")
    private int totalAmount;
    /**
     * 红包发放总人数
     */
    @XStreamAlias("total_num")
    private int totalNum;
    /**
     * 红包祝福语
     */
    @XStreamAlias("wishing")
    private String wishing;
    /**
     * 调用接口的机器IP地址
     */
    @XStreamAlias("client_ip")
    private String clientIp;
    /**
     * 活动名称
     */
    @XStreamAlias("act_name")
    private String actName;
    /**
     * 备注名称
     */
    @XStreamAlias("remark")
    private String remark;

    public String getNonceStr() {
        return nonceStr;
    }

    public void setNonceStr(String nonceStr) {
        this.nonceStr = nonceStr;
    }

    public String getSign() {
        return sign;
    }

    public void setSign(String sign) {
        this.sign = sign;
    }

    public String getMchBillNo() {
        return mchBillNo;
    }

    public void setMchBillNo(String mchBillNo) {
        this.mchBillNo = mchBillNo;
    }

    public String getMchId() {
        return mchId;
    }

    public void setMchId(String mchId) {
        this.mchId = mchId;
    }

    public String getSubMchId() {
        return subMchId;
    }

    public void setSubMchId(String subMchId) {
        this.subMchId = subMchId;
    }

    public String getWxAppid() {
        return wxAppid;
    }

    public void setWxAppid(String wxAppid) {
        this.wxAppid = wxAppid;
    }

    public String getMsgAppid() {
        return msgAppid;
    }

    public void setMsgAppid(String msgAppid) {
        this.msgAppid = msgAppid;
    }

    public String getSendName() {
        return sendName;
    }

    public void setSendName(String sendName) {
        this.sendName = sendName;
    }

    public String getReOpenid() {
        return reOpenid;
    }

    public void setReOpenid(String reOpenid) {
        this.reOpenid = reOpenid;
    }

    public int getTotalAmount() {
        return totalAmount;
    }

    public void setTotalAmount(int totalAmount) {
        this.totalAmount = totalAmount;
    }

    public int getTotalNum() {
        return totalNum;
    }

    public void setTotalNum(int totalNum) {
        this.totalNum = totalNum;
    }

    public String getWishing() {
        return wishing;
    }

    public void setWishing(String wishing) {
        this.wishing = wishing;
    }

    public String getClientIp() {
        return clientIp;
    }

    public void setClientIp(String clientIp) {
        this.clientIp = clientIp;
    }

    public String getActName() {
        return actName;
    }

    public void setActName(String actName) {
        this.actName = actName;
    }

    public String getRemark() {
        return remark;
    }

    public void setRemark(String remark) {
        this.remark = remark;
    }

    /**
     * @param nonceStr    随机的字符串不能超过32位
     * @param mchBillNo   商户订单号
     * @param mchId       商户号
     * @param subMchId    子商户号
     * @param wxAppid     服务商号
     * @param msgAppid    子服务商号
     * @param sendName    红包发送者名称
     * @param reOpenid    接收红包的用户
     * @param totalAmount 付款金额,单位分
     * @param totalNum    红包发放总数
     * @param wishing     红包祝福语
     * @param clientIp    调用接口请求的IP
     * @param actName     活动名称
     * @param remark      备注
     */
    public RedPackEntity(String nonceStr, String mchBillNo, String mchId, String subMchId, String wxAppid, String msgAppid, String sendName, String reOpenid, int totalAmount, int totalNum, String wishing, String clientIp, String actName, String remark) {
        this.nonceStr = nonceStr;
        this.mchBillNo = mchBillNo;
        this.mchId = mchId;
        this.subMchId = subMchId;
        this.wxAppid = wxAppid;
        this.msgAppid = msgAppid;
        this.sendName = sendName;
        this.reOpenid = reOpenid;
        this.totalAmount = totalAmount;
        this.totalNum = totalNum;
        this.wishing = wishing;
        this.clientIp = clientIp;
        this.actName = actName;
        this.remark = remark;
    }

    public RedPackEntity() {
    }
}

```
## 红包工具类

```java
package xxx.xxx.xxx.util;

import xxx.xxx.xxx.entity.RedPackEntity;
import jersey.repackaged.com.google.common.collect.Maps;
import org.apache.commons.codec.digest.DigestUtils;
import org.apache.commons.lang.StringUtils;
import org.apache.http.HttpEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.conn.ssl.SSLConnectionSocketFactory;
import org.apache.http.conn.ssl.SSLContexts;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import javax.net.ssl.SSLContext;
import java.io.*;
import java.net.URLEncoder;
import java.nio.charset.StandardCharsets;
import java.security.KeyStore;
import java.util.*;

/**
 * <p>微信红包工具<p/></br>
 *
 * @author LanChaoHui
 * @date 2018-07-01 21:38
 * @since 1.0
 */
public class RedPackUtil {
    public static String sendRedPack(String data) {
        StringBuffer message = new StringBuffer();
        try {
            //服务商ID
            String mchId = WeiXinUtil.getValueBykey("sendRedPack.service.mchId");
            //获取KeyStore
            KeyStore keyStore = KeyStore.getInstance("PKCS12");
            String certFilePath = WeiXinUtil.getValueBykey("sendRedPack.cert.path");
            FileInputStream instream = new FileInputStream(new File(certFilePath));
            keyStore.load(instream, mchId.toCharArray());
            //创建SSL
            SSLContext sslcontext = SSLContexts.custom().loadKeyMaterial(keyStore, mchId.toCharArray()).build();
            SSLConnectionSocketFactory sslsf = new SSLConnectionSocketFactory(sslcontext, new String[]{"TLSv1"}, null, SSLConnectionSocketFactory.BROWSER_COMPATIBLE_HOSTNAME_VERIFIER);
            CloseableHttpClient httpclient = HttpClients.custom().setSSLSocketFactory(sslsf).build();
            HttpPost httpost = new HttpPost("https://api.mch.weixin.qq.com/mmpaymkttransfers/sendredpack");
            httpost.addHeader("Connection", "keep-alive");
            httpost.addHeader("Accept", "*/*");
            httpost.addHeader("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8");
            httpost.addHeader("Host", "api.mch.weixin.qq.com");
            httpost.addHeader("X-Requested-With", "XMLHttpRequest");
            httpost.addHeader("Cache-Control", "max-age=0");
            httpost.addHeader("User-Agent", "Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.0) ");
            httpost.setEntity(new StringEntity(data, "UTF-8"));
            System.out.println("executing request" + httpost.getRequestLine());
            CloseableHttpResponse response = httpclient.execute(httpost);
            HttpEntity entity = response.getEntity();
            System.out.println("----------------------------------------");
            System.out.println(response.getStatusLine());
            if (entity != null) {
                System.out.println("Response content length: " + entity.getContentLength());
                BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(entity.getContent(), "UTF-8"));
                String text;
                while ((text = bufferedReader.readLine()) != null) {
                    message.append(text);
                }
            }
            EntityUtils.consume(entity);
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println("红包返回结果:" + message);
        return message.toString();
    }

    /**
     * <p>创建红包签名<p/></br>
     *
     * @param redPack 红包实体
     * @return String MD5加密后的值
     * @author LanChaoHui
     * @date 2018-7-1 23:31:28
     * @since 1.0
     */
    public static String createRedPackOrderSign(RedPackEntity redPack) {
        Map<String, String> params = Maps.newHashMap();
        params.put("act_name", redPack.getActName());
        params.put("client_ip", redPack.getClientIp());
        params.put("mch_billno", redPack.getMchBillNo());
        params.put("mch_id", redPack.getMchId());
        params.put("msgappid", redPack.getMsgAppid());
        params.put("nonce_str", redPack.getNonceStr());
        params.put("re_openid", redPack.getReOpenid());
        params.put("remark", redPack.getRemark());
        params.put("send_name", redPack.getSendName());
        params.put("total_amount", String.valueOf(redPack.getTotalAmount()));
        params.put("total_num", String.valueOf(redPack.getTotalNum()));
        params.put("wishing", redPack.getWishing());
        params.put("wxappid", redPack.getWxAppid());
        params.put("sub_mch_id", redPack.getSubMchId());
        try {
            String url = makeUrlFormMap(params, false, false);
            url += "&key=" + WeiXinUtil.getValueBykey("sendRedPack.ApiKey");
            return DigestUtils.md5Hex(url).toUpperCase();
        } catch (UnsupportedEncodingException e) {
            e.printStackTrace();
            return null;
        }
    }

    /**
     * <p>对所有传入参数按照字段名的 ASCII 码从小到大排序（字典序），并且生成url参数串<p/></br>
     *
     * @param paraMap   要排序的Map对象
     * @param urlEncode 是否需要URLENCODE
     * @return keyToLower 是否需要将Key转换为全小写  true:key转化成小写，false:不转化
     * @throws UnsupportedEncodingException 未知字符集异常
     * @author LanChaoHui
     * @date 2018-7-1 23:33:43
     * @since 1.0
     */
    public static String makeUrlFormMap(Map<String, String> paraMap, boolean urlEncode, boolean keyToLower) throws UnsupportedEncodingException {
        StringBuffer stringBuffer = new StringBuffer();
        List<Map.Entry<String, String>> entryList = new ArrayList<>(paraMap.entrySet());
        Collections.sort(entryList, new Comparator<Map.Entry<String, String>>() {
            // 对所有传入参数按照字段名的 ASCII 码从小到大排序（字典序）
            @Override
            public int compare(Map.Entry<String, String> o1, Map.Entry<String, String> o2) {
                return o1.getKey().compareTo(o2.getKey());
            }
        });
        //构造URL
        for (Map.Entry<String, String> entry: entryList) {
            if (!StringUtils.isBlank(entry.getKey())) {
                String key = entry.getKey();
                String val = entry.getValue();
                if (urlEncode) {
                    val = URLEncoder.encode(val, StandardCharsets.UTF_8.name());
                }
                if (keyToLower) {
                    stringBuffer.append(key.toLowerCase()).append("=").append(val);
                } else {
                    stringBuffer.append(key).append("=").append(val);
                }
                stringBuffer.append("&");
            }
        }
        String url = stringBuffer.toString();
        if (!url.isEmpty()) {
            url = url.substring(0, url.length() - 1);
        }
        return url;
    }
}
```



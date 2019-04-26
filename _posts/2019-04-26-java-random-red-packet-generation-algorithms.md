---
layout: post
title: "拼手气红包，生成算法。（每个人最少0.01）"
category: 
- Java
- 红包实现
- 聊天APP 
- 算法研究
tags: ["红包","聊天APP","红包分配算法","红包实现"]
---

自行去校验amount与num的值是否有效。  

```java
/**
 * 红包生成算法
 * amount 单位为分
 */
protected function splitHongbao($amount,$num){
    $red = []; //金额
    $rate = [];// 占比
    $allRate = 0; // 总值
    $min = 0; //占比最小的索引
    $allRed = 0; //二次填充后的总金额
    //一次遍历
    for($i = 0;$i < $num; $i ++){
        $red[$i] = 1; //分配低保
        $rate[$i] = mt_rand(0,$num*1000); //生成随机占比
        $allRate = $rate[$i] + $allRate;//统计总占比
        if($rate[$i] < $rate[$min]){
            $min = $i;  //记录占比最小的索引
        }
    }

    //剩下的钱拿来随机分
    $rest = $amount - $num;

    if($rest < 0){
        throw new Exception('金额错误');
    }

    //二次遍历 填充金额
    for($i = 0;$i < $num; $i ++){
        $red[$i] = $red[$i] + floor($rest * ($rate[$i] / $allRate)); //不保留小数
        $allRed = $allRed + $red[$i];  //累计金额
    }

    $rest = $amount - $allRed; //剩下一点点 分配给刚才最小的
    $red[$min] = $red[$min] + $rest;

    //三次遍历 校验红包金额总和是否正确
    $count = 0;
    for($i = 0;$i < $num; $i ++){
        $count = $count + $red[$i];
    }
    //数组打乱
    shuffle($red);

    return $red;
}
```

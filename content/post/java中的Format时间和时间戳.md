---
title: Java中的Format时间和时间戳
tags: 
- java
date: 2021-03-07 09:50:40
categories:
- java
- 技巧
---

---

## 🧐format时间和时间戳

Timestamp就是所谓的时间戳。这个主要用在数据库上，你可以再java.sql这个包内找到这个类。

一般数据库里如果用Date这个类的话，那你取出来的时候只能到某一天，也就是日，但是Timestamp的话，就是到小时一直到纳秒，很精确的。

时间戳就是一种类型，只是精度很高，比datetime要精确的多，通常用来防止数据出现脏读现象 。

时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数

## 🔃java中format时间和时间戳的转换

```java
import java.text.SimpleDateFormat;
import java.util.Date;

/**
 * @author MengYingjie
 * @version 1.0
 * @date 2020/10/26 21:33
 */
public class Test2 {

    public static void main(String[] args) {
        Long SystemTimeStamp = System.currentTimeMillis();
        System.out.println("时间:" + SystemTimeStamp);
        String timeFormat = stampToDate(SystemTimeStamp);
        System.out.println("时间戳转换为时间:" + timeFormat);
        Long timeStamp = dateToStamp(timeFormat);
        System.out.println("时间转换为时间戳:" + timeStamp);
    }

    /**
     * 将时间转换为时间戳
     *
     * @param timeFormat format 时间格式
     * @return 时间戳时间格式
     */
    public static Long dateToStamp(String timeFormat) {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Long timeStamp = null;
        try {
            timeStamp = sdf.parse(timeFormat).getTime();
        } catch (Exception e) {
            System.out.println("传入了null值");
        }
        return timeStamp;
    }

    /**
     * 将时间戳转换为时间
     *
     * @param timeStamp 时间戳时间格式
     * @return format 时间格式
     */
    public static String stampToDate(Long timeStamp) {
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String timeFormat = format.format(new Date(timeStamp));
        return timeFormat;
    }
}
```
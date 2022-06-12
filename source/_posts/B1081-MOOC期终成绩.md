---
title: B1081-检查密码
date: 2019-12-2 0:34:15 
categories: PAT练习
cover: https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/id=54341472(なつ).mdg91a8wwtc.jpg
---

## 题目描述 <!--more-->

 本题要求你帮助某网站的用户注册模块写一个密码合法性检查的小功能。该网站要求用户设置的密码必须由不少于6个字符组成，并且只能有英文字母、数字和小数点 `.`，还必须既有字母也有数字。 

## 输入描述

>  输入第一行给出一个正整数 N（≤ 100），随后 N 行，每行给出一个用户设置的密码，为不超过 80 个字符的非空字符串，以回车结束。

## 输出描述

> 对每个用户的密码，在一行中输出系统反馈信息，分以下5种：
>
> - 如果密码合法，输出`Your password is wan mei.`；
> - 如果密码太短，不论合法与否，都输出`Your password is tai duan le.`；
> - 如果密码长度合法，但存在不合法字符，则输出`Your password is tai luan le.`；
> - 如果密码长度合法，但只有字母没有数字，则输出`Your password needs shu zi.`；
> - 如果密码长度合法，但只有数字没有字母，则输出`Your password needs zi mu.`。

## 示例

### 输入

> 5
> 123s
> zheshi.wodepw
> 1234.5678
> WanMei23333
> pass*word.6

### 输出

> 5
> 123s
> zheshi.wodepw
> 1234.5678
> WanMei23333
> pass*word.6

## 解题思路：

- 设置三个标记，一个记录是否有字母，一个是否有数字，一个是有除了字母和数字加上.之外的其他字符
- 有其他字符或者同时没有字母和数字输出太乱了。

---

---



```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class PAT_B1081 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        for (int i = 0; i <n ; i++) {
            char[] password = br.readLine().toCharArray();
            if (password.length <6){
                System.out.println("Your password is tai duan le.");
                continue;
            }
            boolean letter = false, number = false, other = true;
            for (int j = 0; j <password.length ; j++) {
                char c = password[j];
                if (c >='a' && c<='z' || c>='A' && c<='Z'){
                    letter = true;
                }else if(c >='0' && c<='9'){
                    number = true;
                }else if(c != '.'){
                    other = false;
                }
            }
            if (!other || letter==false && number==false){
                System.out.println("Your password is tai luan le.");
            }else if (!number && letter){
                System.out.println("Your password needs shu zi.");
            }else if (number && !letter){
                System.out.println("Your password needs zi mu.");
            }else {
                System.out.println("Your password is wan mei.");
            }
        }
    }
}
```


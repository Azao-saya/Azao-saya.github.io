---
title: B1043-输出PATest
date: 2019-11-2 3:34:12 
categories: PAT练习
tags:
- 字符串操作
cover: https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/id=69606244.rzhzf5abaxs.png
---

## 题目描述 <!--more-->

-      给定一个长度不超过 104 的、仅由英文字母构成的字符串。请将字符重新调整顺序，按 `PATestPATest....` 这样的顺序输出，并忽略其它字符。当然，六种字符的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按 PATest 的顺序打印，直到所有字符都被输出。 

## 输入描述

>输入在一行中给出一个长度不超过 104 的、仅由英文字母构成的非空字符串。 

## 输出描述:

>在一行中按题目要求输出排序后的字符串。题目保证输出非空。 

## 示例

### 输入

> redlesPayBestPATTopTeePHPereatitAPPT

### 输出

> PATestPATestPTetPTePePee

## 解题思路：

-  把PATest6个字符遇见的数量分别存入数组的0到5索引中
-  在按照升序遍历数组，值不为零时时输出对应字符，直到数组所有数为零
-  尝试了一下别的循环，运行时间还略有增加，还是直接用被注释的内容就行了

---

---



```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class PAT_B1043 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        br.close();
        int[] PATest = new int[6];
        for (int i = 0; i <str.length() ; i++) {
            if (str.charAt(i)=='P'){
                PATest[0]++;
            }else if (str.charAt(i)=='A'){
                PATest[1]++;
            }else if (str.charAt(i)=='T'){
                PATest[2]++;
            }else if (str.charAt(i)=='e'){
                PATest[3]++;
            }else if (str.charAt(i)=='s'){
                PATest[4]++;
            }else if (str.charAt(i)=='t'){
                PATest[5]++;
            }
        }
        StringBuilder sb = new StringBuilder();
        char[] temp = {'P','A','T','e','s','t'};
//        for (int w = 0; w <str.length(); w++) { //想写判断PATest[]0到6是否还有不为零的，想了下先暴力循环，运行时间还有很多余裕就不改了。
//            for (int i = 0; i <6 ; i++) {
//                if (PATest[i]!=0){
//                    sb.append(temp[i]);
//                    PATest[i]--;
//                }
//            }
//        }

        while(true){
            boolean flag = false;
            for (int i = 0; i <6 ; i++) {
                if (PATest[i]!=0){
                    sb.append(temp[i]);
                    PATest[i]--;
                    flag =true;
                }
            }
            if (!flag){
                break;
            }
        }
        System.out.println(sb);
    }
}
```


---
title: B1080-MOOC期终成绩
date: 2019-12-2 0:34:12 
categories: PAT练习
-tags:
- 祖传屎山代码
cover: https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/id=54341472(なつ).mdg91a8wwtc.jpg
---

## 题目描述 <!--more-->

对于在中国大学MOOC（http://www.icourse163.org/ ）学习“数据结构”课程的学生，想要获得一张合格证书，必须首先获得不少于200分的在线编程作业分，然后总评获得不少于60分（满分100）。总评成绩的计算公式为 *G*=(*G**m**i*d*−*t*e*r*m*×40%+*G**f**i**n**al*×60%)，如果 *G**m**i**d*−*t**e**r**m*>*G**f**i**n**a**l*；否则总评 *G* 就是 *G**f**i**n**a*l。这里 *G**m**i*d*−*t**e**r**m和G**f**i**n**a**l 分别为学生的期中和期末成绩。

现在的问题是，每次考试都产生一张独立的成绩单。本题就请你编写程序，把不同的成绩单合为一张。

## 输入描述

>  输入在第一行给出3个整数，分别是 P（做了在线编程作业的学生数）、M（参加了期中考试的学生数）、N（参加了期末考试的学生数）。每个数都不超过10000。
>
>  接下来有三块输入。第一块包含 P 个在线编程成绩 Gp；
>
>  第二块包含 M 个期中考试成绩 Gmid−term；
>
>  第三块包含 N 个期末考试成绩 Gfinal。
>
>  每个成绩占一行，格式为：学生学号 分数。其中学生学号为不超过20个字符的英文字母和数字；分数是非负整数（编程总分最高为900分，期中和期末的最高分为100分）。 

## 输出描述:

> 打印出获得合格证书的学生名单。每个学生占一行，格式为：
>
> `学生学号 Gp Gmid−term Gfinal G`
> 
> 如果有的成绩不存在（例如某人没参加期中考试），则在相应的位置输出“−1”。输出顺序为按照总评分数（四舍五入精确到整数）递减。若有并列，则按学号递增。题目保证学号没有重复，且至少存在1个合格的学生。

## 示例

### 输入

> 6 6 7
> 01234 880
> a1903 199
> ydjh2 200
> wehu8 300
> dx86w 220
> missing 400
> ydhfu77 99
> wehu8 55
> ydjh2 98
> dx86w 88
> a1903 86
> 01234 39
> ydhfu77 88
> a1903 66
> 01234 58
> wehu8 84
> ydjh2 82
> missing 99
> dx86w 81

### 输出

> missing 400 -1 99 99
> ydjh2 200 98 82 88
> dx86w 220 88 81 84
> wehu8 300 55 84 84

## 解题思路：

- 这题硬做的，没啥思路。

---

---



```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
/**
 * 最后一个测试点超时，又是我最喜欢的再做一题天亮环节。
 * 哎我的认知里必须要用构造体，但是到底要怎么样才能少传参数。
 * 我试过虽然传入参数但不用只对需要的参数使用this，但结果是别的全部初始化了
 * 结果就是大量的重复代码，不过超时应该不是因为这个
 * 听到每个数都不超过10000心里就有点逼数了
 */
public class PAT_B1080 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] temp = br.readLine().split(" ");
        int p = Integer.parseInt(temp[0]);
        int m = Integer.parseInt(temp[1]);
        int n = Integer.parseInt(temp[2]);
        Map<String,Score> map = new HashMap<String,Score>();
        for (int i = 0; i < p; i++) {
            String[] temp2 = br.readLine().split(" ");
            int grade = Integer.parseInt(temp2[1]);
            if (grade < 200){
                continue;
            }
            map.put(temp2[0],new Score(grade));
        }

        for (int i = 0; i <m ; i++) {
            String[] temp3 = br.readLine().split(" ");
            if (map.containsKey(temp3[0])){
                int grade2 = Integer.parseInt(temp3[1]);
                int temp3_1 = map.get(temp3[0]).p_score;
                map.put(temp3[0],new Score(temp3_1,grade2));
            }
        }

        for (int i = 0; i <n ; i++) {
            String[] temp4 = br.readLine().split(" ");
            if (map.containsKey(temp4[0])){
                int grade3 = Integer.parseInt(temp4[1]);
                int temp4_1 = map.get(temp4[0]).p_score;
                int temp4_2 = map.get(temp4[0]).m_score;
                map.put(temp4[0], new Score(temp4_1,temp4_2,grade3));
            }
        }

        for (Map.Entry<String, Score> entry : map.entrySet()) {
            int gp = entry.getValue().p_score;
            double gm = entry.getValue().m_score;
            double gf = entry.getValue().f_score;
            if (gm > gf){
                int total = (int)(gm*0.4+gf*0.6+0.5);
                map.put(entry.getKey(),new Score(gp,(int)gm,(int)gf,total));
                continue;
            }
            map.put(entry.getKey(),new Score(gp,(int)gm,(int)gf,(int)gf));
        }


        List<Map.Entry<String, Score>> list = new ArrayList<Map.Entry<String, Score>>(map.entrySet());
        Collections.sort(list, new Comparator<Map.Entry<String, Score>>() {
            @Override
            public int compare(Map.Entry<String, Score> o1, Map.Entry<String, Score> o2) {
                if (o2.getValue().t_score-o1.getValue().t_score ==0){
                    return o1.getKey().compareTo(o2.getKey());
                }
                return o2.getValue().t_score-o1.getValue().t_score;
            }
        });

        for(Map.Entry<String,Score> mapping:list){
            if (mapping.getValue().m_score==0 && mapping.getValue().t_score>=60){
                System.out.println(mapping.getKey()+" "+mapping.getValue().p_score+" -1 "+mapping.getValue().f_score+" "+mapping.getValue().t_score);
            }else if(mapping.getValue().f_score==0 &&mapping.getValue().t_score>=60){
                System.out.println(mapping.getKey()+" "+mapping.getValue().p_score+" "+mapping.getValue().m_score+" -1"+mapping.getValue().t_score);
            }else if (mapping.getValue().t_score>=60){
                System.out.println(mapping.getKey()+" "+mapping.getValue().p_score+" "+mapping.getValue().m_score+" "+mapping.getValue().f_score+" "+mapping.getValue().t_score);
            }
        }
    }
}
class Score{
    int p_score;
    int m_score ;
    int f_score ;
    int t_score ;
    public Score(int p){
        this.p_score = p;
    }

    public Score(int p, int m){
        this.p_score = p;
        this.m_score = m;
    }

    public Score(int p, int m, int f){
        this.p_score = p;
        this.m_score = m;
        this.f_score = f;
    }

    public Score(int p, int m, int f, int t){
        this.p_score = p;
        this.m_score = m;
        this.f_score = f;
        this.t_score = t;
    }
}
```


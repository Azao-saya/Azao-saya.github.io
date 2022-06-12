---
title: 1002-NowCoder数列
date: 2019-09-30 8:52:52
categories: PAT练习
---

## 题目描述 <!--more-->
>NowCoder最近在研究一个数列：<br/>
* F(0) = 7<br/>
* F(1) = 11<br/>
* F(n) = F(n-1) + F(n-2) (n≥2)<br/>
他称之为NowCoder数列。请你帮忙确认一下数列中第n个数是否是3的倍数。<br/>

## 输入描述:
>输入包含多组数据。<br/>
>每组数据包含一个整数n，(0≤n≤1000000)。<br/>
## 输出描述:
对应每一组输入有一行输出。<br/>
如果F(n)是3的倍数，则输出“Yes”；否则输出“No”。<br/>
## 示例
### 输入例子:
>0<br/>
1<br/>
2<br/>
3<br/>
4<br/>
5<br/>

### 输出例子:
>No<br/>
No<br/>
Yes<br/>
No<br/>
No<br/>
No<br/>

## 解题思路
> * F(n) = F(n-1) + F(n-2) (n≥2)
> * F(0) = 7  &#8195;&#8195;&#8195;&#8195;&#8195;&#8195;余1
> * F(1) = 11 &#8195;&#8195;&#8195;&#8195;&#8195;&ensp;余2
> * F(2) = F(1)+F(0) = 18 余0
> * F(3) = 29 &#8195;&#8195;&#8195;&#8195;&#8195;&ensp;余2
> * F(4) = 47 &#8195;&#8195;&#8195;&#8195;&#8195;&ensp;余2
> * F(5) = 76 &#8195;&#8195;&#8195;&#8195;&#8195;&ensp;余1
> * F(6) = 123 &#8195;&#8195;&#8195;&#8195;&ensp;&ensp;余0
> * F(7) = 199 &#8195;&#8195;&#8195;&#8195;&ensp;&ensp;余1
> * F(8) = 322 &#8195;&#8195;&#8195;&#8195;&ensp;&ensp;余1
> * F(9) = 521 &#8195;&#8195;&#8195;&#8195;&ensp;&ensp;余2
> * F(10)= 843&#8195;&#8195;&#8195;&#8195;&ensp;&ensp;余0
> &#8195;<br/>
> * 凑就完事了嗷 n =2,6,10,14....能被3整除
> * 即 n % 4 ==2 时
> * 然而这题是难在java使用超时，加了一条略过0,1判断使我勉强在6000ms的时间内，最后的用时是5787ms。
&#8195;
***
***

	import java.io.BufferedInputStream;
	import java.util.Scanner;

	public class second_1002 {
	    public static void main(String[] args) {
	        Scanner sc = new Scanner(new BufferedInputStream(System.in));
	        while(sc.hasNext()){
	            int input = sc.nextInt();
	            if( input == 0 || input == 1){
	                System.out.println("No");
	            }else{
	                if (input % 4 == 2){
	                    System.out.println("Yes");
	                }else {
	                    System.out.println("No");
	                }
	            }
	        }
	    }
	}




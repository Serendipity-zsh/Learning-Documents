> **题目描述：**
>
> 罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。
>
> 字符          数值
> I             1
> V             5
> X             10
> L             50
> C             100
> D             500
> M             1000
>
> 例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。
>
> 通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：
>
> ​    I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
> ​    X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。
> ​    C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
>
> 给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。
>
> 示例 1:
>
> 输入: 3
> 输出: "III"
>
> 示例 2:
>
> 输入: 4
> 输出: "IV"
>
> 示例 3:
>
> 输入: 9
> 输出: "IX"
>
> 示例 4:
>
> 输入: 58
> 输出: "LVIII"
> 解释: L = 50, V = 5, III = 3.
>
> 示例 5:
>
> 输入: 1994
> 输出: "MCMXCIV"
> 解释: M = 1000, CM = 900, XC = 90, IV = 4.

 1、极其暴力法

最简单直接的方法就是列出所有的情况，即：1000(M)，900(CM)，500(D)，400(CD)，100(C)，90(XC)，50(L)，40(XL)，10(X)，9(IX)，5(V)，4(IV)，1(I)

一共13种情况，就按照从大到小的顺序，用给定的整数num去分别除以他们，再取余数，继续相除，直至余数为0

用一个整型数组或者13个整型变量去表示对应13种情况的个数，输出对应罗马数字个数

Java代码如下：

```java
public String intToRoman(int num) {
        int a = num / 1000;         //M
        int b = (num % 1000) / 900;  //CM
        int c = ((num % 1000)%900) / 500;//D
        int d = ((num % 1000) % 900 % 500) / 400;//CD
        int e = ((num % 1000) % 900 % 500 % 400) / 100;//C
        int f = (((num % 1000) %900% 500) %400% 100) / 90;//XC
        int g = (((num % 1000) %900 % 500) %400% 100%90) / 50;//L
        int h = ((((num % 1000) %900% 500) %400 % 100%90) % 50) / 40;//XL
        int i = ((((num % 1000) %900% 500)%400 % 100%90) % 50%40) / 10;//X
        int j = (((((num % 1000)%900 % 500)%400 % 100%90) % 50%40) % 10) / 9;//IX
        int k = (((((num % 1000) %900% 500)%400 % 100%90) % 50%40) % 10%9) / 5;//V
        int l = ((((((num % 1000)%900 % 500)%400 % 100%90) % 50%40) % 10%9) % 5) / 4;//IV
        int m = ((((((num % 1000)%900 % 500)%400 % 100%90) % 50%40) % 10%9) % 5) % 4;//I
        String result = "";

        for(int x=0;x<a;x++){

            result = result + "M";
        }
        for(int x=0;x<b;x++){

            result = result + "CM";

        }
        for(int x=0;x<c;x++){

            result = result + "D";
        }
        for(int x=0;x<d;x++){

            result = result + "CD";
        }
        for(int x=0;x<e;x++){

            result = result + "C";
        }
        for(int x=0;x<f;x++){

            result = result + "XC";
        }
        for(int x=0;x<g;x++){

            result = result + "L";
        }
        for(int x=0;x<h;x++){

            result = result + "XL";
        }
        for(int x=0;x<i;x++){

            result = result + "X";
        }
        for(int x=0;x<j;x++){

            result = result + "IX";
        }
        for(int x=0;x<k;x++){

            result = result + "V";
        }
        for(int x=0;x<l;x++){

            result = result + "IV";
        }
        for(int x=0;x<m;x++){

            result = result + "I";
        }
        return result;
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2、暴力优化法

由于上面的方法过于暴力，就简单优化了一下

罗马数字的范围是1-3999，整数转换为罗马数字最长的也就15位，所以就用一个16位的数组result来表示转化后的罗马数字

这里用整除获得低位的方式完成，获得低位数字后，除4，5，9需要特殊处理以外，其它数字每输出一个该分位对应的单位（个位对应“I”，十位对应“X”），就自减1，一直重复循环，直到为0时跳出循环

Java代码如下：

```java
public String intToRoman(int num){
        char Roman[] = {'I', 'V', 'X', 'L', 'C', 'D', 'M'};
        int  i = 14, j = 0, m = 0;
        char result[] = new char[16];
        while(num>0) {
            m = num % 10;
            num /= 10;
            while (true) {
                if (m == 9) {result[i--] = Roman[j+2]; m = 1; }
                else if (m == 8) {result[i--] = Roman[j]; m--;}
                else if (m == 7) {result[i--] = Roman[j]; m--;}
                else if (m == 6) {result[i--] = Roman[j]; m--;}
                else if (m == 5) {result[i--] = Roman[j+1]; break;}
                else if (m == 4) {result[i--] = Roman[j+1]; m=1;}
                else if (m == 3) {result[i--] = Roman[j]; m--;}
                else if (m == 2) {result[i--] = Roman[j]; m--;}
                else if (m == 1) {result[i--] = Roman[j]; break;}
                else{ break;}
            }
            j += 2;
        }
        String stringResult = new String(result);
        return stringResult;

    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3、贪心算法

考虑到上面两种方法还是比较暴力，所以就考虑用贪心算法来解决下这个问题。

其实就是把阿拉伯数字和罗马数字可能出现的所有情况和其对应的情况放在两个数组种，并且按照阿拉伯数字的大小降序排列，判断给定的整数与数组nums中整数的大小，如果给定的整数大，就记下对应的罗马数字，并减去nums中比较的数字，一直循环，直到给定整数减到比nums数组中的整数小，再继续与后面的数字比较，直至所有比较完。（这个就是贪心最优选择的思想）

Java代码如下：

```java
public String intToRoman(int num) {
        int[] nums = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] luomas = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        String result = "";
        int index = 0;
        //一共13种选择
        while (index<13) {
            while (num >= nums[index]) {

                result += luomas[index];
                num -= nums[index];
            }
            index++;
        }
        return result;
    }
```


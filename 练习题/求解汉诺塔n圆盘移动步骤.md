
```
package cn.edu.tsinghua.javase.exercise;

import java.util.Scanner;

/**
 * @author mingfei.net@gmail.com
 * @link https://github.com/thu/JavaSE_20170902/
 * @since 16:20 23 Sep 2017
 */

// 求解汉诺塔 n 圆盘移动步骤
public class E52 {

    private static int counter = 0;

    static void hanoi(int n, char src, char with, char dest) {
        if (n == 1) {
            System.out.println(src + "\t->\t" + dest);
            counter++;
        } else {
            hanoi(n - 1, src, dest, with);
            System.out.println(src + "\t->\t" + dest);
            counter++;
            hanoi(n - 1, with, src, dest);
        }

    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("input n: ");
        int n = scanner.nextInt();

        hanoi(n, 'A', 'B', 'C');
        System.out.println("counter: " + counter);
    }
}

/*

 -
 --
____ ____ ____
 A    B     C

 n = 1
 A -> C

 n = 2
 A -> B
 A -> C
 B -> C

 n
 ?

 */


```
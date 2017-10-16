
```
package cn.edu.tsinghua.javase.exercise;

import java.util.Scanner;

/**
 * @author mingfei.net@gmail.com
 * @link https://github.com/thu/JavaSE_20170902/
 * @since 13:30 23 Sep 2017
 */

// 输入两个正整数m和n，求其最大公约数和最小公倍数
public class E6 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("input m: ");
        int m = scanner.nextInt();
        System.out.println("input n: ");
        int n = scanner.nextInt();

        int min = Math.min(m, n);
        for (int i = min; i > 0; i--) {
            if (m % i == 0 && n % i == 0) {
                System.out.println("Greatest Common Divisor: " + i);
                break;
            }
        }

        int max = Math.max(m, n);
        for (int i = max; i < m*n + 1; i++) {
            if (i % m == 0 && i % n == 0) {
                System.out.println("Lowest Common Multiple: " + i);
                break;
            }
        }
    }
}


```
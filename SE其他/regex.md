# 补1. 正则表达式 `Regular Expression`

> RegEx = Regular Expression

1. 括号 `Brackets`
    - [abc]	
    - [^abc]	
    - [0-9]	
    - [^0-9]	
    - (x|y)	 
    - `[a-d[m-p]]`	a 到 d 或 m 到 p：[a-dm-p]（并集）
    - `[a-z&&[def]]`	d、e 或 f（交集）
    - `[a-z&&[^bc]]`	a 到 z，除了 b 和 c：[ad-z]（减去）
    - `[a-z&&[^m-p]]`	a 到 z，而非 m 到 p：[a-lq-z]（减去）           
    
2. 元字符 `Metacharacters`    
    - .	
    - \w	
    - \W	
    - \d
    - \D
    - \s
    - \S
    - \b
    - \B
    - \0
    - \n
    - \f
    - \r
    - \t
    - \v
    - \xxx
    - \xdd
    - \uxxxx

3. POSIX 字符类（仅 US-ASCII）    
    - `\p{Lower}`	小写字母字符：[a-z]3. 量词 `Quantifiers`    
    - `\p{Upper}`	大写字母字符：[A-Z]    - n+	
    - `\p{ASCII}`	所有 ASCII：[\x00-\x7F]    - n*	
    - `\p{Alpha}`	字母字符：[\p{Lower}\p{Upper}]    - n?	
    - `\p{Digit}`	十进制数字：[0-9]    - n{X}	
    - `\p{Alnum}`	字母数字字符：[\p{Alpha}\p{Digit}]    - n{X,Y}	
    - `\p{Punct}`	标点符号：!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~    - n{X,}	
    - `\p{Graph}`	可见字符：[\p{Alnum}\p{Punct}]    - n$	
    - `\p{Print}`	可打印字符：[\p{Graph}\x20]    - ^n	
    - `\p{Blank}`	空格或制表符：[ \t]    - ?=n	
    - `\p{Cntrl}`	控制字符：[\x00-\x1F\x7F]    - ?!n	
    - `\p{XDigit}`	十六进制数字：[0-9a-fA-F]    
    - `\p{Space}`	空白字符：[ \t\n\x0B\f\r]

4. 量词 `Quantifiers`    
    - n+	
    - n*	
    - n?	
    - n{X}	
    - n{X,Y}	
    - n{X,}	
    - n$	
    - ^n	
    - ?=n	
    - ?!n	
    
5. `java.util.regex`

    - Pattern
        - compile
        - split
    - Matcher
        - find
        - group                    
    
    
- 匹配单个字符

```
System.out.println("\u0041\\\\");
输出
A\\
```
- 从大段的字符串中找到所有的电话号码

```
 public static void main(String[] args) {

        // 使用字符串模拟从网络上得到的网页源码
        String str = "我想求购一本《疯狂Java讲义》，尽快联系我13500006666"
                + "交朋友，电话号码是13611125565"
                + "出售二手电脑，联系方式15899903312";
        // 创建一个Pattern对象，并用它建立一个Matcher对象
        // 该正则表达式只抓取13X和15X段的手机号，
        // 实际要抓取哪些电话号码，只要修改正则表达式即可。\\d 匹配0到9的所有数字
        Matcher m = Pattern.compile("((13\\d)|(15\\d))\\d{8}")
                .matcher(str);
        // 将所有符合正则表达式的子串（电话号码）全部输出
        while(m.find())//依次查找字符串中匹配的子串
        {
            System.out.println(m.group());
        }
    }
```
-  匹配所有的非单词字符

```
  public static void main(String[] args)
    {
        // 创建一个Pattern对象，并用它建立一个Matcher对象
        String regStr = "Java is very easy!";
        System.out.println("目标字符串是：" + regStr);
//        匹配所有的非单词字符
        Matcher m = Pattern.compile("\\w+")
                .matcher(regStr);
        while(m.find())
        {
            System.out.println(m.group() + "子串的起始位置："
                    + m.start() + "，其结束位置：" + m.end());
        }
    }
    
    输出结果
    目标字符串是：Java is very easy!
    Java子串的起始位置：0，其结束位置：4
    is子串的起始位置：5，其结束位置：7
    very子串的起始位置：8，其结束位置：12
    easy子串的起始位置：13，其结束位置：17
```
- 判断一个字符串是不是一个有效的电子邮件地址

```

	public static void main(String[] args)
	{
		String[] mails =
		{
			"kongyeeku@163.com" ,
			"kongyeeku@gmail.com",
			"ligang@crazyit.org",
			"wawa@abc.xx"
		};
		String mailRegEx = "\\w{3,20}@\\w+\\.(com|org|cn|net|gov)";
		Pattern mailPattern = Pattern.compile(mailRegEx);
		Matcher matcher = null;
		for (String mail : mails)
		{
			if (matcher == null)
			{
				matcher = mailPattern.matcher(mail);
			}
			else
			{  //matcher应用到一个新的字符串系列
				matcher.reset(mail);
			}
			String result = mail + (matcher.matches() ? "是" : "不是")
				+ "一个有效的邮件地址！";
			System.out.println(result);
		}
	}
```
- 将所有匹配的字符串进行替换

```
 public static void main(String[] args)
    {
        String[] msgs =
                {
                        "Java has regular expressions in 1.4",
                        "regular expressions now expressing in Java",
                        "Java represses oracular expressions"
                };
        Pattern p = Pattern.compile(" re\\w*");
        Matcher matcher = null;
        for (int i = 0 ; i < msgs.length ; i++)
        {
            if (matcher == null)
            {
                matcher = p.matcher(msgs[i]);
            }
            else
            {
                matcher.reset(msgs[i]);
            }
            System.out.println(matcher.replaceAll("哈哈:)"));
        }
    }
```
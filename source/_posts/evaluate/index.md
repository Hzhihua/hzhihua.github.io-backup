---
title: evaluate
date: 2017-10-30 08:42:07
---

# Dijkatra的双栈算术表达式求值算法
> 算法第四版(java版)  P 80-81
```java
import java.util.Stack;

public class Evaluate {
	public static void main(String[] args) {
		Stack<String> ops = new Stack<String>();
		Stack<Double> vals = new Stack<Double>();
		while (!StdIn.isEmpty()) {
			String s = StdIn.readString();
			if      (s.equals("("))	              ;
			else if (s.equals("+"))	   ops.push(s);
			else if (s.equals('-'))    ops.push(s);
			else if (s.equals("*"))    ops.push(s);
			else if (s.equals("/"))    ops.push(s);
			else if (s.equals("sqrt")) ops.push(s);
			else if (s.equals(")")) {
				// pop stack
				String op = ops.pop();
				Double val = vals.pop();
				if (op.equals("+"))         val = vals.pop() + val;
				else if (op.equals("-"))    val = vals.pop() - val;
				else if (op.equals("*"))    val = vals.pop() * val;
				else if (op.equals("/"))    val = vals.pop() / val;
				else if (op.equals("sqrt")) val = Math.sqrt(val);
				vals.push(val);
			}
			else vals.push(Double.parseDouble(s));
		}
		System.out.println(vals.pop());
	}
}
```

> evaluate_data.txt

```data
( ( 1 + sqrt ( 5.0 ) ) / 2.0 )
```

> 运算结果

```ssh
$ javac Evaluate.java
$ java Evaluate < evaluate_data.txt
$ 1.618033988749895
```


## 分析

1. 将操作数压入操作数栈

2. 将运算符压入运算符栈

3. 忽略左括号

4. 在遇到有括号时，弹出一个运算符，以及所需数量的操作数，并将运算符和操作数的运算结果压入操作数栈

5. 例如：

   ( 1 + ( 2 + 3 ) * ( 4 * 5 ) )

   ( 1 + ( 5 ) * ( 4 * 5 ) )

   ( 1 + ( 5 ) * ( 20 ) )

   ( 1 + 100 )

   101

## 图解

![evaluate图解](images/evaluate/Dijkstra-evaluate.png)

## 源代码

[github](https://github.com/Hzhihua/hzhihua.github.io-backup/tree/master/source/evaluate) [download](evaluate.tar.gz) 
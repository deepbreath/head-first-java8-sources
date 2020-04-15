
## 概览
出镜率和基本类型一样高的核心数据结构，可以没有 boolean , 但是不能没有 String. 帝国基石。  

## 常见用法
[测试类](../tests/lang/StringTest.java)
```java
int length = "test".length();
assertEquals(4, length);

boolean bc = "test".contains("tes");
assertEquals(true, bc);

boolean bs = "test".startsWith("tes");
assertEquals(true, bs);

boolean be = "test".endsWith("st");
assertEquals(true, be);

char cc = "test".charAt(3);
assertEquals('t', cc);

int ii = "test".indexOf('e');
assertEquals(1, ii);

java.lang.StringTest trim = " test ".trim();
assertEquals("test", trim);

java.lang.StringTest[] es = "test".split("e");
assertEquals(2, es.length);
assertEquals("t", es[0]);
assertEquals("st", es[1]);

java.lang.StringTest substring = "test".substring(1, 2);
assertEquals("e", substring);

java.lang.StringTest uc = "test".toUpperCase();
assertEquals("TEST", uc);

java.lang.StringTest lc = "tEst".toLowerCase();
assertEquals("test", lc);

java.lang.StringTest replace = "test".replace("te", "T");
assertEquals("Tst", replace);

java.lang.StringTest ra = "stest".replaceAll(".{2}t", "T");
assertEquals("stT", ra);

java.lang.StringTest test = java.lang.StringTest.join(",", "x", "y", "z");
assertEquals("x,y,z", test);

java.lang.StringTest j2 = java.lang.StringTest.join(",", Arrays.asList("x", "y", "z"));
assertEquals("x,y,z", j2);

```

## 继承结构
![java.lang.String](java.lang.String.png)
## 主要属性
### 成员变量
```java
/** The value is used for character storage. */
private final char value[]; // 字符数组， 存储字符

/** Cache the hash code for the string */
private int hash; // Default to 0 // 性能优化， String 的实现是不可变的， 生命周期内 hash 也是不会变得， 不用每次计算。 
```
### 静态变量
```java
/** use serialVersionUID from JDK 1.0.2 for interoperability */
private static final long serialVersionUID = -6849794470754667710L;

/**
 * Class String is special cased within the Serialization Stream Protocol.
 *
 * A String instance is written into an ObjectOutputStream according to
 * <a href="{@docRoot}/../platform/serialization/spec/output.html">
 * Object Serialization Specification, Section 6.2, "Stream Elements"</a>
 */
private static final ObjectStreamField[] serialPersistentFields =
    new ObjectStreamField[0]; 与序列化有关， 后续分析序列化时再详细分析
```

## 主要方法
### 构造函数
```java
/**
 * Initializes a newly created {@code String} object so that it represents
 * an empty character sequence.  Note that use of this constructor is
 * unnecessary since Strings are immutable.
 */
public String() {
    this.value = "".value;
}

/**
 * Constructs a new {@code String} by decoding the specified subarray of
 * bytes using the specified {@linkplain java.nio.charset.Charset charset}.
 * The length of the new {@code String} is a function of the charset, and
 * hence may not be equal to the length of the subarray.
 *
 * <p> This method always replaces malformed-input and unmappable-character
 * sequences with this charset's default replacement string.  The {@link
 * java.nio.charset.CharsetDecoder} class should be used when more control
 * over the decoding process is required.
 *
 * @param  bytes
 *         The bytes to be decoded into characters
 *
 * @param  offset
 *         The index of the first byte to decode
 *
 * @param  length
 *         The number of bytes to decode
 *
 * @param  charset
 *         The {@linkplain java.nio.charset.Charset charset} to be used to
 *         decode the {@code bytes}
 *
 * @throws  IndexOutOfBoundsException
 *          If the {@code offset} and {@code length} arguments index
 *          characters outside the bounds of the {@code bytes} array
 *
 * @since  1.6
 */
public String(byte bytes[], int offset, int length, Charset charset) {
    if (charset == null)
        throw new NullPointerException("charset");
    checkBounds(bytes, offset, length);
    this.value =  StringCoding.decode(charset, bytes, offset, length);
}

```
### 实例方法


### 静态方法

## 常见问题
1. 平时开发都是直接 ```String x = "xxx"```，没有使用 ```String x = new String("xxx") ``` ， 这两种方式有啥区别，怎么选择？

2. ```"xxx" + "yyy"``` 是什么魔法？ 如果用过 C 语言，会发现字符串不能直接相加。

3. String 的不变性，不可变意味着什么， 为什么要设计为不可变， 怎么实现不可变。 

4. 关于 String intern 方法。  
建议不用深究， 意义不大，在几个主流代码库（spring, netty, dubbo) 搜索均没有该方法的使用。

5. switch 语句与 String .

## 补充

## 后记

## 参考
- [JDK 之 String 源码阅读笔记](https://emacsist.github.io/2017/07/01/jdk-%E4%B9%8B-string-%E6%BA%90%E7%A0%81%E9%98%85%E8%AF%BB%E7%AC%94%E8%AE%B0/)
- [String源码分析](https://juejin.im/post/59fffddc5188253d6816f9c1)
- [深入解析String#intern](https://tech.meituan.com/2014/03/06/in-depth-understanding-string-intern.html)
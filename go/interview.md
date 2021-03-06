# Go 面试要点
## goroutine的实现
## Go 内置函数
* close：主要用来关闭channel
* len：用来求长度，比如string,array,slice,map,channel
* new：用来分配内存，主要用来分配值类型，比如int,struct。返回的是指针
* make：用来分配内存，主要用来分配引用类型，比如chan,slice,map
* append：用来追加元素到数组、切片中，非线程安全
* panic和recover：用来做错误处理

## golang 中 new 和 make 的区别
* make 仅用来分配及初始化类型为 slice、map、chan 的数据。new 可分配任意类型的数据.
* new 分配返回的是指针，即类型 *Type。make 返回引用，即 Type.
* new 分配的空间被清零, make 分配空间后，会进行初始化.

## 高效拼接字符串
Go 语言中，字符串是只读的，也就意味着每次修改操作都会创建一个新的字符串。如果需要拼接多次，应使用 strings.Builder，最小化内存拷贝次数。
```go
var str strings.Builder
for i := 0; i < 1000; i++ {
    str.WriteString("a")
}
fmt.Println(str.String())
```
## 字节序
大小端问题主要涉及的是非单字节非字符串外的其余数据的表示和传递，如short型、int型等。大端和小端有其各自的优势。我们知道计算机正常的内存增长方式是从低到高(当然栈不是)，取数据方式是从基址根据偏移找到他们的位置，从他们的存储方式可以看出，大端存储因为第一个字节就是高位，从而很容易知道它是正数还是负数，对于一些数值判断会很迅速。而小端存储 第一个字节是它的低位，符号位在最后一个字节，这样在做数值四则运算时从低位每次取出相应字节运算，最后直到高位，并且最终把符号位刷新，这样的运算方式会更高效。

## rune 与 byte 类型
* 在unicode中，一个中文占两个字节，utf-8中一个中文占三个字节，golang默认的编码是utf-8编码，因此默认一个中文占三个字节
* rune类型的底层类型是int32类型，适合表达unicode字符
* byte类型的底层类型是int8类型，适合表达ascii编码的字符 
* rune能处理一切的字符，而byte仅仅局限在ascii

```go
fmt.Println(len("Go语言")) // 8
fmt.Println(len([]rune("Go语言"))) // 4
```

## Go 单引号、双引号与反引号
* 双引号用来创建可解析的字符串字面量(支持转义，但不能用来引用多行)
* 反引号用来创建原生的字符串字面量，这些字符串可能由多行组成(不支持任何转义序列)，原生的字符串字面量多用于书写多行消息、HTML以及正则表达式
* 单引号则用于表示Golang的一个特殊类型：rune，类似其他语言的byte但又不完全一样，是指：码点字面量（Unicode code point），不做任何转义的原始内容。
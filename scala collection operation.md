sacla 对集合的操作
===
scala中的集合有数组array，元组tuple，列表list以及用Map产生的映射。

list
--
list是列表，我们可以在集合中储存任何类型的值，而不只是数字或字符串，我们还可创建一个集合的集合。可以把一个列表分解为表头（head）和表尾（tail）,表头即列表的第一项，表尾即为列表的其余项。

    scala > val primes = List(2,3,5,7,11,13)
    primes: List[Int] = List(2,2,5,7,11,13)
    
    scala > val first = primes.head
    first: Int = 2
    
    scala > val remaining = primes.tail
    remaining: List[Int] = List(3,5,7,11,13)
    
List可以用来构建迭代器，确定何时到达列表末尾可以使用isEmpty方法，而无需遍历列表。

Cons操作符
可以使用cons操作符来构建列表，使用右结合的操作符::。所有列表都有一个Nil实例作为终结点。

    scala > val numbers = 1::2::3::Nil
    numbers： List[Int] = List(1,2,3)
集合方法
--

### map函数

`Map` 是一个不可变的键-值库。在Map中值按一个给定的唯一键值存储，可以使用这个键值来获取对应的值。键和值都可以类型参数化，像创建从整数到字符串的映射一样，也可以很容易地创建从字符串到整数的映射。`Map`可以用来创建一个键值库，通过键来索引对应的值。

map（）的用法：取一个函数，将一个列表元素转换成另一个值和/或类型。

### foreach函数

取一个函数（或者说是过程），遍历列表中的元素，并对每一项分别调用这个函数。

映射
--
### 构造映射 
    val scores = Map("Jim"->10, ("Tom",20), "Sam"->44) //key->value, (key,value)两种方式表示, 不可变映射，
    val s = scala.collection.mutable.Map("Jim"->10, ("Tom",20), "Sam"->44)//可变映射
    val s1 = new scala.collection.mutable.HashMap[String, Int] //空的Map

    //scores.+=(("Lily"->10))  //不可变映射，map中不能新增元素 
    s.+=(("Lily"->10))
    s1.+=(("Jim"->10))

    println(scores)
    println(s)
    println(s1)
### 获取映射的值
    val scores = Map("Jim"->10, ("Tom",20), "Sam"->44)
 
    val score1 = scores("Lily")  //直接通过()获取里面的值
    val score2 = if(scores.contains("Lily")) scores("Lily") else 0 //判断是否存在，然后再取值
    val score3 = scores.getOrElse("Lily",0) //通过getOrElse方法实现，不存在给默认值

    println(score1)//没有值，会报异常
    println(score2)
    println(score3)
### 更新映射的值


### flatmap操作符

`flatmap`对列表进行扁平化处理，并映射出新的列表。

### array操作符


### scala中的partition span splitAt groupBy

注：

    val (a,b) = List(1,2,3,4,5).partition(_%2==0)
    // (List(2,4), List(1,3,5))

    可把Collection分成：满足条件的一组，其他的另一组。

    和partition相似的是span，但有不同：

    List(1,9,2,4,5).span(_<3)       //
     (List(1),List(9, 2, 4, 5))，碰到不符合就结束

    List(1,9,2,4,5).partition(_<3) //
     (List(1, 2),List(9, 4, 5))，扫描所有

    List(1,3,5,7,9) splitAt 2 //
     (List(1, 3),List(5, 7, 9))

    List(1,3,5,7,9) groupBy (5<) //
     Map((true,List(7, 9)), (false,List(1, 3, 5)))

### zip函数

- zip函数合并两个列表

    scala> val list = "Hello.World".toCharArray
    list: Array[Char] = Array(H, e, l, l, o, ., W, o, r, l, d)
 
    scala> val list1 = 1 to 20 toList
    list1: List[Int] = List(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20)
 
    scala> list.zip(list1)
    res30: Array[(Char, Int)] = Array((H,1), (e,2), (l,3), (l,4), (o,5), (.,6), (W,7), (o,8), (r,9), (l,10), (d,11))
 
    scala> list1.zip(list)
    res31: List[(Int, Char)] = List((1,H), (2,e), (3,l), (4,l), (5,o), (6,.), (7,W), (8,o), (9,r), (10,l), (11,d))
 
 - zip函数返回的列表的长度与较短的列表相关，只要有一个列表到达末尾就结束
 我们还可使用zipall对剩余的元素进行处理
 
    scala> list.zipAll(list1,'a','1')
    res33: Array[(Char, AnyVal)] = Array((H,1), (e,2), (l,3), (l,4), (o,5), (.,6), (W,7), (o,8), (r,9), (l,10), (d,11), (a,12), (a,13)(a,14), (a,15), (a,16), (a,17), (a,18), (a,19), (a,20))
    
- 如果字母列表比较短就用a来补充，如果数字列表比较短就使用1来补充。
还有zipwithindex函数，使用元素在列表内的索引值构成新的元组列表

    scala> list.zipWithIndex
    res36: Array[(Char, Int)] = Array((H,0), (e,1), (l,2), (l,3), (o,4), (.,5), (W,6), (o,7), (r,8), (l,9), (d,10))
 
### reduce函数
reduce()取一个函数，将两个列表元素结合成一个元素。

使用reduce我们可以处理列表的每个元素并返回一个值。通过使用reduceLeft和reduceRight我们可以强制处理元素的方向。（使用reduce方向是不被保证的）
注：reduce和fold很像，但reduce返回的值的类型必须和列表的元素类型相关（类型本身或其父类），但fold没有这种限制（但与此同时fold必须给定一个初始值），可以说reduce是fold的一种特殊情况。reduce()取一个函数，将两个列表元素结合成一个元素。

    scala> list1
    res51: List[Int] = List(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20)
 
    scala> val sum = (x:Int, y:Int) => {println(x,y) ; x + y} 
    sum: (Int, Int) => Int = <function2>
 
    scala> list1.reduce(sum)
    (1,2)
    (3,3)
    (6,4)
    (10,5)
    (15,6)
    (21,7)
    (28,8)
    (36,9)
    (45,10)
    (55,11)
    (66,12)
    (78,13)
    (91,14)
    (105,15)
    (120,16)
    (136,17)
    (153,18)
    (171,19)
    (190,20)
    res52: Int = 210
 
    scala> list1.reduceLeft(sum)
    (1,2)
    (3,3)
    (6,4)
    (10,5)
    (15,6)
    (21,7)
    (28,8)
    (36,9)
    (45,10)
    (55,11)
    (66,12)
    (78,13)
    (91,14)
    (105,15)
    (120,16)
    (136,17)
    (153,18)
    (171,19)
    (190,20)
    res53: Int = 210
 
    scala> list1.reduceRight(sum)
    (19,20)
    (18,39)
    (17,57)
    (16,74)
    (15,90)
    (14,105)
    (13,119)
    (12,132)
    (11,144)
    (10,155)
    (9,165)
    (8,174)
    (7,182)
    (6,189)
    (5,195)
    (4,200)
    (3,204)
    (2,207)
    (1,209)
    res54: Int =210
### fold函数

### 列表的排序操作
使用sorted方法

    scala> val a = List(10, 5, 8, 1, 7).sorted
    a: List[Int] = List(1, 5, 7, 8, 10)

ordeing和ordered为traits

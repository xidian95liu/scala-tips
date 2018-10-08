sacla 对集合的操作
===
scala中的集合有数组array，元组tuple，列表list以及用Map产生的映射。

集合方法
--
### map操作符
`Map` 是一个不可变的键-值库。在Map中值按一个给定的唯一键值存储，可以使用这个键值来获取对应的值。键和值都可以类型参数化，像创建从整数到字符串的映射一样，也可以很容易地创建从字符串到整数的映射。
map（）的用法：取一个函数，将一个列表元素转换成另一个值和/或类型。
### foreach操作符
遍历集合中的元素，并对每一项执行指定的方法
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


flatmap操作符
--
`flatmap`



列表的操作方法
--
foreach（）：取一个函数，对列表中的每一项分别调用这个函数取一个函数。
reduce（）：取一个函数，将两个列表元素结合成一个元素。

array操作符
--

scala中的partition span splitAt groupBy
---

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

key symbol of scala
==

具体代码表现如下：
---


    object ScalaOperator {
    def main(args: Array[String]) {
        // ::: 三个冒号:2个集合合并
        println("------- [:::] ")
        val list1 = List(1, 2)
        val list2 = List(3, 4)

        val listCombine = list1 ::: list2
        listCombine.foreach(x => {
            println(x)
        })

        println("------- [::] ")
        // :: 2个 冒号 元素添加到集合中
        // 元素在前, 集合在后
        val d = 5 :: listCombine

        // => 方法体指标符
        d.foreach(x => {
            println(x)
        })

        // -> 构造一个二元的元组
        println("------- [->]")
        val one = 1
        val two = 2
        val c = one -> two
        println(c)

        // _N 用于访问元组中的数据元素,坐标从1开始
        println("------- [_N]")
        println("one = " + c._1)
        println("two = " + c._1)

        println("------- [<-] ")
        // <- 将集合中的元素 依次赋给临时变量
        for (v <- listCombine) {
            println(" v = " + v)
        }

        println("------- arrBuf1 [result1]")
        //
        val arrBuf1 = new ArrayBuffer[Int]()
        arrBuf1.+=(11) // 添加一个元素
        arrBuf1.+=(33, 44) //添加多个元素
        arrBuf1.insert(1, 22) //在index=1,位置插入22
        arrBuf1 += 55 //添加一个元素
        arrBuf1.append(66) // 追回一个元素
        arrBuf1.prepend(77) // 在头部追加一个元素
        arrBuf1.prepend(88) // 在头部追加一个元素
        arrBuf1.prepend(99) // 在头部追加一个元素
        for (elem <- arrBuf1) {
            println(elem)
        }
        println("------- arrBuf1 [result2] ")
        arrBuf1.remove(3, 2) // 从index=3开始,删除2个元素
        for (elem <- arrBuf1) {
            println(elem)
        }

        println("------- arrBuf1 [result3] ")
        arrBuf1.trimEnd(2) // 删除尾部2个元素
        for (elem <- arrBuf1) {
            println(elem)
        }

        val arrBuf3 = arrBuf1.+:(3) // 在首部增加一个元素,并返回一个新集合
        println("------- arrBuf3 [result] = ")
        arrBuf3.foreach(x => {
            println(x)
        })

        println("------- arrBuf2 [result]")
        // val arrBuf3 = 5 ++ arrBuf2
        val arrBuf2 = new ArrayBuffer[Int]()
        arrBuf2.+=(3)
        arrBuf2.+=(4)

        arrBuf2.foreach(x => {
            println(x)
        })

        println("------- arrBufCom [result]")
        // 将arrBuf2,arrBuf1所有元素都添加到新集合 arrBufCom 中,返回arrBufCom
        val arrBufCom = arrBuf1.++:(arrBuf2)
        arrBufCom.foreach(x => {
            println(x)
        })

        println("------- arrBuf1 [result4]")
        // 将arrBuf2中的所有元素,都增加到arrBuf1首部
        arrBuf1.++=:(arrBuf2)
        arrBuf1.foreach(x => {
            println(x)
        })

        // :_* 将集合元素当作 参数序列来处理,用在有变长参数列表的函数中
        println("------- seq:_* [result]")
        val seq = Seq(1, 2, 3, 4, 5)
        println(my_sum(seq: _*))
    }

    def my_sum(args: Int*): Int = {
        var result = 0
        for (a <- args) {
            result += a
        }
        return result
    }
    }
通配符用法

    1、作为“通配符”，类似Java中的*。如import scala.math._
    2、:_*作为一个整体，告诉编译器你希望将某个参数当作参数序列处理！例如val s = sum(1 to 5:_*)就是将1 to 5当作参数序列处理。
    3、指代一个集合中的每个元素。例如我们要在一个Array a中筛出偶数，并乘以2，可以用以下办法：a.filter(_%2==0).map(2*_)。又如要对缓冲数组ArrayBuffer b排序，可以这样：val bSorted = b.sorted(_
    4、在元组中，可以用方法_1, _2, _3访问组员。如a._2。其中句点可以用空格替代。5、使用模式匹配可以用来获取元组的组员，例如val (first, second, third) = t
    但如果不是所有的部件都需要，那么可以在不需要的部件位置上使用_。比如上一例中val (first, second, _) = t6、还有一点，下划线_代表的是某一类型的默认值。对于Int来说，它是0。对于Double来说，它是0.0对于引用类型，它是null。欢迎指正补充


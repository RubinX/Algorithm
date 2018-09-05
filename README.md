# Algorithm
#蓄水池抽样问题</br>
#可以类似的思路解决。先把读到的前k个对象放入“水库”，对于第k+1个对象开始，以k/(k+1)的概率选择该对象，以k/(k+2)的概率选择第k+2个对象，以此类推，以k/m的概率选择第m个对象（m>k）。如果m被选中，则随机替换水库中的一个对象。最终每个对象被选中的概率均为k/n，

#Fast-Slow-Pointer</br>
##快慢指针用来判断链表是否有环是十分有效的手段，如何来严格证明呢？ ###有人类比在操场上一快一慢两个人跑步 我认为这种类比是不恰当的。因为操场上跑步是连续的，快的越快则相遇的时间越短，但是链表是离散的，步长太大会直接越过满指针。
下面我给出快慢指针步长和环大小与相遇时间的关系。 ###数学证明 假设 进入环以后慢指针走了x步，m为步长，则快指已经走了mx步，L为环的长度。
假设相遇则 mx%L=x%L,（假设 nf为快指针走的圈数，ns为慢指针走的圈数）
nfL+x%L =mx 
x%L=mx-nfL
nsL+mx-nfL=x
(m-1)x=(nf-ns)L
当 m=2时，x=（nf-ns）L
当满指针走（nf-ns）L步时肯定相遇
x=((nf-ns)/(m-1))*L 必须保证x为整数。

##Java中如何实现BitSet? </br>
###常规做法是使用位操作，与或非异或 1.定义一个整型数组，大小为N 2.通过/,%获取数组上的操作数 3.使用与或非异或
###能不能Boolean型的数组呢？ The boolean data type has only two possible values: true and false. 
Use this data type for simple flags that track true/false conditions.
This data type represents one bit of information, but its "size" isn't something that's precisely defined
以上摘自官方文档，说它表示1bit信息，但是大小是不确定的
####观点一：
（1）在虚拟机里boolean在编译成字节码时会用int或byte来表示。false用整数0表示，true用非零整数表示。涉及boolean的操作是用int进行的。 boolean数据是当成byte数组进行访问的。
（2）JAVA虚拟机中，基本的数据单元是字（word）大小由虚拟机的设计而定。一般为32位。虚拟机的局部变量和操作数栈都是按照字来字义的。
####观点二： （1）编译器对boolean变量进行了优化，在一个boolean变量情况下，编译器会给此变量安排一个字节的内存，但在多个boolean的情况下时，编译器会将多个变量安排在一个字节里 ####实验 定义一个4万×4万的boolean[][]，JDK7的JVM内存上限设置1000MB，很快占满并java.lang.OutOfMemoryError: Java heap space
说明一个boolean变量实际占用1Byte
#因为java虚拟机的最小寻址单元是byte，所以即使Boolean型实际占用1bit,最终还是要归结到常规解法上。

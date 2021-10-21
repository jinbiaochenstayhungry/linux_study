参考
https://www.hhcycj.com/post/item/351.html
https://zhuanlan.zhihu.com/p/110402378

# gcc编译过程
如果假设有这么一个test.c文件内容为

#include<stdio.h>
#define NUM 1
int main(){
int i =NUM * 10;
printf("numb is %d",i);

}

Linux 是如何把他编译成可执行文件的呢.
1、第一步当然是文本基本的预处理
  * 出来#include命令,将对应的命令复制到main.c这个文件来,也就是负责stdio.h文件
  * cpp程序将NUM 替换成相关文本.
  * 处理条件编译,将不符合条件的代码删除
  * 
2、第二步就是把他编译成汇编代码了,这个过程使用的工具是cc1,这里面就要涉及到分词、语法分析生成语法树,构建作用域,语义分析,代码生成
  * cc1其实是本身也实现了cpp命令的

3、利用as编译成目标文件.o
  * 这个时候生成的就是elf格式的文件了
  * 创建链接时候的信息,包括符号表,重定位表
4、ld、collect
  * 安排好静态对象
  * 链接静态库时候,并不是将整个静态库中的所有文件都合并到目标文件中,而仅仅链接库中使用到的目标文件,当然,这个库中的目标文件有可能有个别函数用不到.
  * 链接动态库时候,无法在文件生成时候重定位符号,智能生成一份冲定位表,帮助加载器在文件运行时候重新定位符号
  
 5、点击运行
  * https://blog.csdn.net/gatieme/article/details/51628257
  * https://www.cxyzjd.com/article/fivedoumi/53262160

# 工具链的组成
  ## binutil的使用
  * as、objdump
  * https://zhuanlan.zhihu.com/p/110402378
gcc调用binutils中的各种工具来处理代码的过程中,gcc要依赖于c库如glibc、uclibc,但是c库本身的编译时由编译器来完成的,这就带来一个循环依赖的问题.
我们能想到的办法是让编译器不用依赖c库来编译程序,但是因为以下原因,编译器需要依赖于c库.
* 编译器需要根据c库的某些特性来决定自己支持哪些特性,因此c编译器要依赖c库的头文件.
* 


# gcc 和g++的关系

  

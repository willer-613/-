<!--
 * @Author: your name
 * @Date: 2019-12-04 23:05:00
 * @LastEditTime: 2019-12-04 23:26:26
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \informal-essay\front-end-deep\event-loop.MD
 -->
#  事件运行机制

### ![命令](https://img.shields.io/badge/EventLoop-深入理解EventLoop机制-green.svg  "深入理解EventLoop机制")

>看`代码`说话

    //主线程任务
    console.log(1);

    //宏任务
    setTimeout(() => {
      //宏任务里面的主线程任务
      console.log(2);
      //宏任务里面的微任务
      Promise.resolve().then(() => {
        console.log(3)
      });
    });
    
    //微任务
    new Promise((resolve, reject) => {
      console.log(4)
      resolve(5)
    }).then((data) => {
      console.log(data);
      //微任务
      Promise.resolve().then(() => {
        console.log(6)
      }).then(() => {
        console.log(7)
        //宏任务
        setTimeout(() => {
          console.log(8)
        }, 0);
      });
    })
   //宏任务
    setTimeout(() => {
      console.log(9);
    })
    //主线程任务
    console.log(10);

>输出结果

* 说明究竟什么流程？
>整个函数执行的顺序是 先执行主线程任务 我们看看
* `主线程任务`包含那些 console.log(1) Pormise 函数内部的console.log(4)、console.log(10)
* 然后在执行`主线程上的微任务` Promise函数的then函数里面的内容 console.log(data) data就是前面resolve传递过来的值5 所以执行console.log(5)、然后是promise里面的promise函数内部的console.log(6)然后是then里面的console.log(7) 
* 最后都剩下宏任务setTimeout函数了 第一个setTimeout函数内部是console.log(2)、然后执行微任务promise函数 console.log(3)、接着执行第二个setTimeout函数内部是console.log(9)，最后当然是执行最后一个setTimeout函数console.log(8)
* `其实主要实行顺序是先全局宏任务执行看看内部有没有其他宏任务遇到一个宏任务就把宏任务添加到eventloop栈里面等全局宏任务就内部的主线任务及微任务执行完了才去栈内读取下一个宏任务，按照第一步执行顺序一步一步执行，因为js是单线程的嘛！！`

     1  4  10 5 6 7 2 3 9 8
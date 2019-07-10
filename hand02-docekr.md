# day03日报
##  一、线程
#### 1.1 什么是线程？
```
    说线程就必须得将一下进程，线程、进程都是操作系统的概念，而我们java程序中的进程线程都是对操作系统中的线程和进程进行实现并加以封装，再暴露出相关的接口供我们java程序员使用。那什么是进程呢？进程是指运行的程序代码，操作系统会为他分配系统资源，包括内存，网络等资源。那线程又是什么呢？线程是轻量级的进程，是程序中的多条执行路径。每个进程包含一个或者多个线程。线程不占用系统资源。
 ```
#### 1.2 线程有哪几种状态
```
新建==>就绪==>运行==>阻塞==>销毁
```
#### 1.3 java中线程的创建
~~~
a.继承thread类
public class Demo {
	public static void main(String[] args) {
		TtestThread t=new TtestThread();
		t.run();
		t.start();
		System.out.println("456");
		gg();
	}
	static void gg() {
		System.out.println("123");
	}
}
 class TtestThread extends Thread{

	@Override
	public void run() {

		System.out.println("456");
	}	 
 }
 
 b.实现Runnable接口
public class StudyDemo {
	public static void main(String[] args) {
		Study s=new Study();
		new Thread(s).start();
		
		for(int i=0;i<10000;i++) {
			if(5000==i) {
				s.stop();
			}
			
			System.out.println("mian thread **********"+i);
		}
	}
}
class Study implements Runnable{
	private boolean flag=true;
	@Override
	public void run() {

		while(flag) {
			System.out.println("i am Studing");
		}
	}
	public void stop() {
		this.flag=false;
	}
}
~~~
#### 1.4 线程池
        虽然线程是个轻量级的东西， 但是对于互联网应用来说，如果每个用户的请求都创建一个线程，那会非常得多，服务器也是难于承受， 再说了，众多的线程去竞争CPU，不断切换，也会让CPU调度不堪重负，很多线程将不得不等待。所以前辈们的思路就是（1）用少量的线程 （2） 让线程保持忙碌
         当线程池的线程刚创建时，让他们进入阻塞状态：等待某个任务的到来。 如果任务来了，那就好办，唤醒其中一个线程，让它拿到任务去执行即可。
         BlockingQueue听说过没有？ 没听说过？ 其实很简单，就是一个线程调用它的take()方法取数据时， 如果这个Queue中没有数据，该线程会阻塞；同样，一个线程调用它的put方法放数据时，如果Queue满了， 也会阻塞。
  ![image](https://minio.choerodon.com.cn/knowledgebase-service/file_c37bf12b53d841e09cc6562f264dd650_blob.png)  ![image](https://minio.choerodon.com.cn/knowledgebase-service/file_714066fb0e2441828d93da5dc3c36dae_blob.png)
## 二、DockerFile
### 2.1自定义centos
>1.编写
> 2.构建
> 3.运行

>  centos容器不提供vim指令
>  centos容器不提供ifconfig
>  进入容器后进入根目录/
![image](https://minio.choerodon.com.cn/knowledgebase-service/file_6fab19cf99ea4646858b4a4958c7d353_blob.png)
* 编写dockerFile

~~~
from centos         //从centos镜像开始

ENV mypath /tmp         //设置环境变量
WORKDIR $mypath     //进入容器后的落脚点，即当前位置

RUN yum -y install vim      //执行Linux命令下载vim工具
RUN yum -y install net-tools        //下载net-tool

EXPOSE 80
CMD /bin/bash   //进入可执行命令行
~~~
* 构建自定义镜像
>  docker build -f /docker-01/Dockerfile -t mycetos:1.1 .

![image](https://minio.choerodon.com.cn/knowledgebase-service/file_ddc5eff129b749858ad9d05d5870bca4_blob.png)
* 查看镜像
发现本地镜像多出新创建的
*![image](https://minio.choerodon.com.cn/knowledgebase-service/file_64137fb3a2064b3192019adfdf6cec00_blob.png)
### 2.2 总结
最终我们在基于dockerhub上面的 centos上又重新编写构建我们1.1版本的mycentos，实现了原本没有的功能，完成对镜像的改造。
## 三、SQL
### 3.1sql概念
> sql是彼岸准的计算机语言，用来操作数据库  。
### 3.2sql弱点强化
#### sqllike子句
QL LIKE 子句通过通配符来将一个值同其他相似的值作比较。可以同 LIKE 运算符一起使用的通配符有两个：

百分号（%）
下划线（_）
~~~
WHERE SALARY LIKE '200%'	找出所有 200 打头的值
WHERE SALARY LIKE '%200%'	找出所有含有 200 的值
WHERE SALARY LIKE '%2'	找出所有以 2 结尾的值
~~~
#### sql limit子句
在mysql中用limit来分页，
~~~
SELECT * FROM `student` limit 0,3 ; #查询1-3行学生记录
SELECT * FROM `student` limit 2,1 ; #查询第三条学生记录
~~~

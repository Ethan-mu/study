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
## 1.1 PRD输出环境

| 文档状态 | 产品版本 | 文档编号 | 撰写人 | 撰写日期 |
| ---- | :---: | :---: | --- | ---- |
| 编辑中 | V1.0 | 2019-12-31 | 某某某 | 2019-12-31 |
| 修改中 |  |  |  |  |
| 已完成 |  |  |  |  |
<br>
## 1.2 修订记录
<br>
| 版本号 | 修订日期 | 修订内容 | 修订人 |
| :---: | :---: | :---: | :---: |
| V1.0 | 2017-04-05 | 新增【工作台】、【分享】功能 | 某某某 |
| V1.0 | 2018-02-28 | 修复样式BUG | 某某某 |
| V1.0 | 2019-04-10 | 新增【游客访问】功能 | 某某某 |
| V1.0 | 2019-10-11 | 删除【工作台展示模式设置】功能 | 某某某 |
|  |  |  |  |
<br>
## 1.3名词解释

| 专业名词 | 描述 |
| ---- | --- |
| 工作台 | <span class="highlight" style="background-color:rgb(255, 255, 255)"><span style="color:#505050"><span class="font" style="font-family:&quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, 微软雅黑, &quot;Microsoft JhengHei&quot;, 黑体, arial, STHeiti, 宋体"><span class="size" style="font-size:14px">个人用户登录后展示个人创建、协同的项目。</span></span></span></span> |
| 游客访问 | <span class="highlight" style="background-color:rgb(255, 255, 255)"><span style="color:#505050"><span class="font" style="font-family:&quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, 微软雅黑, &quot;Microsoft JhengHei&quot;, 黑体, arial, STHeiti, 宋体"><span class="size" style="font-size:14px">不需要注册登录即可访问猪齿鱼的部分功能（比如知识库分享）。在使用需要登录的功能时，引导用户前往注册登录。</span></span></span></span> |
| <span class="highlight" style="background-color:rgb(255, 255, 255)"><span style="color:#505050"><span class="font" style="font-family:&quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, 微软雅黑, &quot;Microsoft JhengHei&quot;, 黑体, arial, STHeiti, 宋体"><span class="size" style="font-size:14px">公开可下载</span></span></span></span> | <span class="highlight" style="background-color:rgb(255, 255, 255)"><span style="color:#505050"><span class="font" style="font-family:&quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, 微软雅黑, &quot;Microsoft JhengHei&quot;, 黑体, arial, STHeiti, 宋体"><span class="size" style="font-size:14px">他人可在用户的工作台或用户给出的链接内访问、下载项目。</span></span></span></span> |
| <span class="highlight" style="background-color:rgb(255, 255, 255)"><span style="color:#505050"><span class="font" style="font-family:&quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, 微软雅黑, &quot;Microsoft JhengHei&quot;, 黑体, arial, STHeiti, 宋体"><span class="size" style="font-size:14px">私有</span></span></span></span> | <span class="highlight" style="background-color:rgb(255, 255, 255)"><span style="color:#505050"><span class="font" style="font-family:&quot;PingFang SC&quot;, &quot;Microsoft YaHei&quot;, 微软雅黑, &quot;Microsoft JhengHei&quot;, 黑体, arial, STHeiti, 宋体"><span class="size" style="font-size:14px">设置为私有的项目在他人访问用户个人主页时不会显示，只能通过用户分享的链接预览查看。</span></span></span></span> |
|  |  |
<br>
<br>
## 2.1 产品介绍

Choerodon 猪齿鱼是开源多云技术平台，是基于 Kubernetes 的容器编排和管理能力，整合 DevOps 工具链、微服务和移动应用框架，来帮助企业实现敏捷化的应用交付和自动化的运营管理，并提供 IoT、支付、数据、智能洞察、企业应用市场等业务组件，来帮助企业聚焦于业务，加速数字化转型。
<br>
## 2.2 用户群体

中小型及大型企业。
<br>
## 2.3 需求清单

| 序号 | 需求名称 | 需求描述 | 需求来源 | 状态 | 优先级 |
| :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | 文档分享 | 将文档分享某人 | 产品部 | 已完成 | 高 |
| 2 | 找回密码 | 对忘记登录密码的用户，发送重置密码邮件 | 产品部 | 待处理 | 中 |
| 3 | 游客模式 | 未注册登录情况下仅能查看被分享的内容 | 产品部 | 处理中 | 低 |
| 4 | 权限设置 | 对工作台中的项目进行权限设置 | 产品部 | 已完成 | 高 |
|  |  |  |  |  |  |
<br>
## 2.4 需求变更记录

| 修改时间 | 版本 | 属性 | 描述 | 修改人 |
| ---- | --- | --- | --- | --- |
| 2018-04-05 | V1.0 | 新增 | 1.新增游客模式<br>2.新增权限管理 | 某某某 |
| 2018-06-07 | V1.0 | 删除 | 修改项目名称功能 | 某某某 |
| 2018-08-19 | V1.0 | 修改 | 修改知识库项目权限设置 | 某某某 |
|  |  |  |  |  |
<br>
## 2.5 功能列表

| 功能模块 | 功能点 | 功能描述 | 优先级 |
| ---- | --- | ---- | :---: |
| @rows=4:登录/注册 | 邮箱登录/注册 | 用户可通过邮箱登录，系统自动监测邮箱账号是否正确，并跳转到对应的登录/注册页面 | 中 |
| 找回密码 | 帮助用户找回邮箱登录密码 | 中 |  |
| 工号登录 | 用户可快速通过工号登录 | 中 |  |
| 游客访问 | 用户未注册登录时，仅可访问被分享的内容 | 低 |  |
| @rows=3:个人信息 | 接收设置 | 对项目通知和平台通知的设置 | 高 |
| 权限信息 | 权限信息的展示 | 中 |  |
| 退出登录 | 退出当前登录账号，回到登录/注册页面 | 中 |  |
<br>
## 3.1 信息结构图

3.2 功能结构图
3.3 交互原型

<br>
## 4.1 功能权限

#### 登录前
<br>
以游客的身份进行使用，只能查看分享的文档内容。

![image](https://minio.choerodon.com.cn/knowledgebase-service/file_382c09bd7a404b60bae5569f46f17207_blob.png)
<br>
#### 登录后
<br>
可使用所有功能

![image](https://minio.choerodon.com.cn/knowledgebase-service/file_2ba1001e2b94471098ff019df2ebc677_blob.png)
<br>
## 4.2 异常提示

交互触发：输入账号/密码不正确时，出现异常提示

![image](https://minio.choerodon.com.cn/knowledgebase-service/file_34d520f0441042e28e2c7cdd457b25fd_blob.png)
<br>
## 4.3 页面交互

#### hover
<br>
交互触发：鼠标移入或移出触发区域，触发对应反馈，展示或隐藏信息。

![image](https://minio.choerodon.com.cn/knowledgebase-service/file_41519c998a2440549c0e68d37b473b3c_blob.png)
<br>
## 4.4  弹层交互

#### toast
<br>
交互触发：操作相应的功能后，在页面左下角出现，2s后自动消失。

弹层交互：渐隐渐现
<br>
#### 对话框
<br>
交互触发：操作相应的功能后，在页面中心出现，用户对其进行操作后消失。

弹层交互：渐隐渐现
<br>
## 4.5 机制与规则

#### 排序规则
<br>
1.最近更新：内容列表按照更新的时间进行倒序排列

2.工作列表：列表内容按照用户创建时间的先后进行倒序排列

<br>
#### 搜索规则
<br>
1.知识库中的搜索功能，搜索范围为所有已创建的知识库和文档的项目。

2.支持模糊搜索。

3.搜索逻辑为点击搜索，输入关键词后，点击键盘上的“确认”/“回车键”进行搜索。

<br>
#### 加载机制
<br>
1.打开知识库时，系统自动加载项目内容。

2.加载过程中，toast提示错误信息，加载内容将不被展示。

<br>
<br>
## 页面说明（示例一）

![image](https://minio.choerodon.com.cn/knowledgebase-service/file_36393c4d192948e8ad801c789f257e3f_blob.png)

##### 1.格式验证：
<br>
当登录名/邮箱格式输入错误时，会有弹窗提示【邮箱格式不正确】
<br>
##### 产品逻辑：
<br>
1.当【邮箱账号】被检测【已注册】，则进入【登录页】

2.当【邮箱账号】被检测【未注册】，则进入【注册页】
<br>
##### 2.
<br>
点击输入框，出现输入光标；
未输入密码或者密码错误时，出现错误提示
<br>
##### 3.
<br>
注册
<br>
##### 4.
<br>
点击进入【重置密码】页面
<br>
##### 5.
<br>
登录

<br>
## 页面说明（示例二）

![image](https://minio.choerodon.com.cn/knowledgebase-service/file_acbc3948400a43a592e94e3874e9428b_blob.png)

| 控件名称 | 交互 | 文案 | 异常态/操作 | 异常反馈 |
| ---- | --- | --- | ------ | ---- |
| 登录名/邮箱输入框 | 点击输入框，输入框变亮，出现输入光标 | 登录名/邮箱 | 输入登录名/邮箱不正确 | 登录名/密码错误 |
| 登录按钮 | 点击按钮，按钮变为选中态，跳转到系统页 | 登录 | 输入登录名/邮箱不正确 | 登录名/密码错误 |
|  |  |  |  |  |
<br>
## 页面说明（示例三）
<br>
![image](https://minio.choerodon.com.cn/knowledgebase-service/file_acbc3948400a43a592e94e3874e9428b_blob.png)
<br>
##### 使用场景：
<br>
登录、注册、忘记密码。
<br>
##### 交互说明：
<br>
* 点击输入框，输入框边框边亮，出现输入光标。
* 点击登录按钮，按钮变为选中态，跳转到系统页。

<br>
##### 异常态反馈
<br>
* 输入登录名/邮箱名不正确，弹窗提示“登录名或密码错误”

<br>
<br>
## 5.1 数据需求

#### 性能需求

| 模块 | 响应时间 | 并发数 |
| --- | ---- | --- |
| 登录授权 | < 3s | 10000 |
| 搜索 | < 3s | 5000 |
| 加载/刷新 | < 3s | 5000 |
| 预览项目 | < 2s | 5000 |
<br>
#### 数据埋点
<br>
| 事件编号 | 统计事件埋点路径 |
| ---- | -------- |
| 1 | 进入登录/注册页-游客访问 |
| 2 | 进入登录/注册页---忘记密码---重置邮件---登陆成功 |
| 3 | 进入个人信息页---查看权限信息、接收设置 |
<br>
<br>
## 5.2 其它非功能性需求

#### 服务需求

| 服务事件 | 服务频率 | 场景描述 | 协助类型 | 解决方案 | 需要协助方 | 服务成本 |
| ---- | ---- | ---- | ---- | ---- | ----- | ---- |
| 客户投诉 | 10次/周 | 无法登陆 | 客服 | 查看操作手册 | 技术人员 | 0.5个工作日 |
| 注册协议 | 1次 | 用户注册前阅读并同意的协议规定 | 法务 |  | 运营、产品 | 2个工作日 |
| 活动费用 | 1次 | 财务报销活动费用 | 财务 | 提交支出明细 | 运营 | 0.5个工作日 |
|  |  |  |  |  |  |  |
<br>
##### 风险描述
<br>
| 服务事件 | 服务频率 | 场景描述 | 协助类型 | 解决方案 | 需要协助方 | 服务成本 |
| ---- | ---- | ---- | ---- | ---- | ----- | ---- |
| 客户投诉 | 10次/周 | 无法登陆 | 客服 | 查看操作手册 | 技术人员 | 0.5个工作日 |
| 注册协议 | 1次 | 用户注册前阅读并同意的协议规定 | 法务 |  | 运营、产品 | 2个工作日 |
| 活动费用 | 1次 | 财务报销活动费用 | 财务 | 提交支出明细 | 运营 | 0.5个工作日 |
|  |  |  |  |  |  |  |


# MQ

## ActiveMQ

## RocketMQ



RocketMQ必问，把上课讲的准备点就可以应付了，其实这块也可介绍一些其他的消息中间件

rocketmq怎么配置的？

### **消息队列都有哪些**

**答：**Kafka、ActiveMQ、RabbitMQ、RocketMQ（在用）

秒杀怎么做的 mq订阅方事务失败了怎么办

1.10RocketMQ用的哪种？全局排序还是分区排序？（真的不知道），如何分区的？

 rocketMQ事务

订阅消息模式

RocketMQ消息队列的流程

为何用RocketMQ？和其他MQ相比，它的优点是什么？

分布式事务是通过MQ实现的？说一下RocketMQ事务流程**

### 是否了解rabbitMQ，是否了解MongoDB

6.用的是消息队列是什么？哪里用到了异步消息队列？

\10. 消息队列的原理？

12.rocketmq有哪些优势



14.rocketmq如何实现分布式事务？







参考：https://www.jianshu.com/p/824066d70da8





## Kafka











## RabbitMQ 然后画xmind图

 学习这个MQ的时候，有个小细节，有时候需要先启动Recv1，Recv2，然后再用Send发送消息。

个人感觉这里其实是Recv在监听Listener生产者，如果生产者生产出来消息，消费者就会根据某种约定的规则来消费。

### 1.消息队列解决了什么问题

#### 异步处理

![1594020269426](../media/pictures/MQ.assets/1594020269426.png)

如果串行的话，显然很浪费时间，因为发短信和邮件这些并不是和主业务有关。

如果并行，就像交易所项目，将这些非业务相关放到线程池里面。

异步就是放到MQ里面啦。

#### 应用解耦

![1594020460950](../media/pictures/MQ.assets/1594020460950.png)

微服务秒杀系统，订单完成以后，要减库存，假如这时候减库存这个服务挂了怎么办？

这时候引入MQ，订单完成以后，放入MQ，即使是减库存服务挂掉，等它上线，去MQ拿取还是可以减库存的，这时候订单模块和减库存模块是完全解耦的。

#### 流量削峰

![1594021283046](../media/pictures/MQ.assets/1594021283046.png)

当时学秒杀的时候，用过这个，异步削峰。 req指的是请求。

#### 日志处理



### 2.Rabbit安装与配置

可以正常的安装下载linux或者wins版本。这里试试docker版本。

#### Docker下安装RabbitMQ





  我们还是采用老规矩，在docker上安装最新版本

 

##### 1.拉取镜像

```
docker pull rabbitmq:3-management
```

![img](../media/pictures/MQ.assets/869262-20190617144708629-1279840356.png)

 

##### 2.查看镜像

```
docker images;
```

![img](../media/pictures/MQ.assets/869262-20190617144817128-740364497.png)

 

##### 3.启动镜像 生成docker容器 ，**默认用户名是guest ，密码是guest**

```shell
docker run --name rabbitmq -p 15672:15672 -p 5672:5672 1482b87815ec
```

![img](../media/pictures/MQ.assets/869262-20190617145436225-1650718155.png)

 

##### 4.如果在生成容器的时候设置用户名和密码的命令如下

```
docker run --name rabbitmq -e RABBITMQ_DEFAULT_USER=root -e RABBITMQ_DEFAULT_PASS=123 -p 15672:15672 -p 5672:5672 rabbitmq:3-management
```

 

##### 5.查看所有的docker容器

```
[root@holly ~]# docker ps -a
```

![img](../media/pictures/MQ.assets/869262-20190617150022232-206618987.png)

 

##### 6.启动rabbitmq容器

```
[root@holly ~]# docker start rabbitmq
```

![img](../media/pictures/MQ.assets/869262-20190617153408239-2136144192.png)

 

##### 7.查看已经启动的容器

![img](../media/pictures/MQ.assets/869262-20190617153458316-820400943.png)

 

##### 8.浏览器访问

![img](../media/pictures/MQ.assets/869262-20190617153542795-1948356413.png)

![img](../media/pictures/MQ.assets/869262-20190617153641500-765220633.png)

 

参考：https://www.cnblogs.com/holly8/p/11040009.html



##### ERROR：

在阿里云Docker安装RabbitMQ以后，阿里云安全组也都打开，但是外面访问不了主页。这时候需要：

```shell
#开启插件：首先使用命令进入容器  
docker exec -it myrabbitmq bash

#开启插件命令：
rabbitmq-plugins enable rabbitmq_management
```

![1594026000747](../media/pictures/MQ.assets/1594026000747.png)

然后就可以访问了：

![1594026017460](../media/pictures/MQ.assets/1594026017460.png)



参考：https://www.cnblogs.com/hellohero55/p/11953882.html



#### 用户管理

##### 新建一个用户 用于开发 

![1594026721078](../media/pictures/MQ.assets/1594026721078.png)

##### virtual hosts 管理

就相当于mysql 或者其他数据库 db

![1594026967549](../media/pictures/MQ.assets/1594026967549.png) 

![1594027064737](../media/pictures/MQ.assets/1594027064737.png)

一般以/开头

![1594027621965](../media/pictures/MQ.assets/1594027621965.png)

给刚才添加的user赋予新的权限。



然后试试user_steve  123 是否可以登录、

![1594027760001](../media/pictures/MQ.assets/1594027760001.png)

登录成功。



看一些其他的信息。

![1594027971304](../media/pictures/MQ.assets/1594027971304.png)

其实用docker部署的时候是可以看到这些的。





### 3.Java操作rabbitmq

#### 1.simple   简单队列

##### 模型

![1594037378049](../media/pictures/MQ.assets/1594037378049.png)

P：消息的生产者

红色的队列

C：消息的消费者



##### 获取MQ连接

```java
package com.jdrx.rabbitmq.utils;

import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 获取MQ的连接
 *
 * @author Steve
 * @date 2020/7/6-21:30
 */
public class ConnectionUtils {
	public static Connection getConnection() throws IOException, TimeoutException {

		//定义一个连接工厂
		ConnectionFactory factory = new ConnectionFactory();
		
		//设置服务地址
		factory.setHost("47.92.208.93");
		
		//AMQP 5672
		factory.setPort(5672);
		
		//vhost
		factory.setVirtualHost("/vhost_steve");
		
		//用户名
		factory.setUsername("user_steve");
		
		//密码
		factory.setPassword("123");
		
		return factory.newConnection();
	}
}
```

这里有一个注意的点，如果在浏览器访问阿里云上面的RabbitMQ，则15672端口是可以访问的。

如果是，在代码中作为客户端使用，15672用不了，只能用5672。

猜测估计是，15672是server，5672是client。



服务5672启动以后，就可以

![1594082996051](../media/pictures/MQ.assets/1594082996051.png)

在服务器上，就可以看到。

![1594083019988](../media/pictures/MQ.assets/1594083019988.png)

##### 消息生产者

```java
package com.jdrx.rabbitmq.simple;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * @author Steve
 * @date 2020/7/6-21:42
 */
public class Send {

	private static final String QUEUE_NAME = "test_simple_queue";

	public static void main(String[] args) throws IOException, TimeoutException {
		
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();
		
		channel.queueDeclare(QUEUE_NAME,false,false,false,null);
		
		String msg = "hello simple !";
		
		channel.basicPublish("",QUEUE_NAME,null,msg.getBytes());

		System.out.println("--send msg" + msg);
		
		channel.close();
		connection.close();
	}
}

```



##### 消息消费者

```java
package com.jdrx.rabbitmq.simple;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 消费消息
 *
 * @author Steve
 * @date 2020/7/7-8:54
 */
public class Recv {

	private static final String QUEUE_NAME = "test_simple_queue";
	
	public static void main(String[] args) throws IOException, TimeoutException, InterruptedException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		Channel channel = connection.createChannel();
		
		//队列声明
		channel.queueDeclare(QUEUE_NAME,false,false,false,null);
		
		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel){
			//获取到达的消息
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, 
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body,"utf-8");
				System.out.println("new Api msg" + msg);
			}
		};
		
		//监听队列
		channel.basicConsume(QUEUE_NAME,true,consumer); 
	}

	/**
	 * 旧的API 这里面的方法比较旧 有些已经废除啦
	 * @throws IOException
	 * @throws TimeoutException
	 * @throws InterruptedException
	 */
	public static void oldAPI() throws IOException, TimeoutException, InterruptedException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		Channel channel = connection.createChannel();

		//定义队列的消费者
		QueueingConsumer consumer = new QueueingConsumer(channel);

		//监听队列
		channel.basicConsume(QUEUE_NAME,true,consumer);
		while (true){
			QueueingConsumer.Delivery delivery = consumer.nextDelivery();

			String msgString = new String(delivery.getBody());
			System.out.println("[recv] msg:" + msgString);
		}
		
	}
}

```

##### 简单队列的不足

耦合性高，生产者一一对应消费者，如果想有多个消费者消费队列中的消息，这时候就不行啦

队列名变更，这时候得同时变更。



#### 2.work queues 工作多队列 

##### 轮询分发

这个就是一个生产者对应多个消息消费者。



###### 模型

![1594087159028](../media/pictures/MQ.assets/1594087159028.png)

###### 为什么会出现工作队列？

Simple队列时一一对应的，而且我们实际开发，生产者发送消息是毫不费力的，而消费者一般是要跟业务相结合的，小份这接受到消息之后就需要处理，可能需要花费时间，这时候队列就会积压很多消息。



###### 生产者

```java
package com.jdrx.rabbitmq.work;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * |----C1
 * P-------|
 * |----C2
 *
 * @author Steve
 * @date 2020/7/7-10:05
 */
public class Send {

	private static final String QUEUE_NAME = "test_work_queue";

	public static void main(String[] args) throws IOException, TimeoutException, InterruptedException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		for (int i = 0; i < 50; i++) {
			String msg = "hello " + i;

			System.out.println("[WQ] send:" +msg);

			channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());
			Thread.sleep(i * 20);
		}

		channel.close();
		connection.close();
	}
}

```



###### 消费者1 停两秒

```java
package com.jdrx.rabbitmq.work;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv1 {

	private static final String QUEUE_NAME = "test_work_queue";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME,false,false,false,null);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel){
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body,"utf-8");
				System.out.println("[1] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}finally {
					System.out.println("[1] Recv done");
				}
			}
		};

		//监听队列
		channel.basicConsume(QUEUE_NAME,true,consumer);
	}
}

```



###### 消费者2  停一秒

```java
package com.jdrx.rabbitmq.work;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv2 {

	private static final String QUEUE_NAME = "test_work_queue";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME,false,false,false,null);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel){
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body,"utf-8");
				System.out.println("[2] Recv msg" + msg);

				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}finally {
					System.out.println("[2] Recv done");
				}
			}
		};

		//监听队列
		channel.basicConsume(QUEUE_NAME,true,consumer);
	}
}
```



###### 现象

消费者1和消费者2处理的数据时一样的，均分的。

```java
//消费者1
[1] Recv msghello 0
[1] Recv done
[1] Recv msghello 2
[1] Recv done
[1] Recv msghello 4
[1] Recv done
[1] Recv msghello 6
[1] Recv done
[1] Recv msghello 8
[1] Recv done
[1] Recv msghello 10
[1] Recv done
[1] Recv msghello 12
[1] Recv done
[1] Recv msghello 14
[1] Recv done
[1] Recv msghello 16
[1] Recv done
[1] Recv msghello 18
[1] Recv done
[1] Recv msghello 20
[1] Recv done
[1] Recv msghello 22
[1] Recv done
[1] Recv msghello 24
[1] Recv done
[1] Recv msghello 26
[1] Recv done
[1] Recv msghello 28
[1] Recv done
[1] Recv msghello 30
[1] Recv done
[1] Recv msghello 32
[1] Recv done
[1] Recv msghello 34
[1] Recv done
[1] Recv msghello 36
[1] Recv done
[1] Recv msghello 38
[1] Recv done
[1] Recv msghello 40
[1] Recv done
[1] Recv msghello 42
[1] Recv done
[1] Recv msghello 44
[1] Recv done
[1] Recv msghello 46
[1] Recv done
[1] Recv msghello 48
[1] Recv done


//消费者2
[2] Recv msghello 1
[2] Recv done
[2] Recv msghello 3
[2] Recv done
[2] Recv msghello 5
[2] Recv done
[2] Recv msghello 7
[2] Recv done
[2] Recv msghello 9
[2] Recv done
[2] Recv msghello 11
[2] Recv done
[2] Recv msghello 13
[2] Recv done
[2] Recv msghello 15
[2] Recv done
[2] Recv msghello 17
[2] Recv done
[2] Recv msghello 19
[2] Recv done
[2] Recv msghello 21
[2] Recv done
[2] Recv msghello 23
[2] Recv done
[2] Recv msghello 25
[2] Recv done
[2] Recv msghello 27
[2] Recv done
[2] Recv msghello 29
[2] Recv done
[2] Recv msghello 31
[2] Recv done
[2] Recv msghello 33
[2] Recv done
[2] Recv msghello 35
[2] Recv done
[2] Recv msghello 37
[2] Recv done
[2] Recv msghello 39
[2] Recv done
[2] Recv msghello 41
[2] Recv done
[2] Recv msghello 43
[2] Recv done
[2] Recv msghello 45
[2] Recv done
[2] Recv msghello 47
[2] Recv done
[2] Recv msghello 49
[2] Recv done

```



消费者1 偶数

消费者2 奇数

这种方式叫轮询分类（round-robin）结果就是不管谁忙活着谁清闲，都不会多给活着少给一个消息。任务消息总是你一个，我一个。



##### 公平分发 fair dipatch

![1594089901073](../media/pictures/MQ.assets/1594089901073.png)

使用公平分发 必须关闭自动应答 ack 改成手动



###### 生产者

```java
package com.jdrx.rabbitmq.workfair;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * |----C1
 * P-------|
 * |----C2
 *
 * @author Steve
 * @date 2020/7/7-10:05
 */
public class Send {

	private static final String QUEUE_NAME = "test_work_queue";

	public static void main(String[] args) throws IOException, TimeoutException, InterruptedException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		//声明队列
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//每个消费者 发送确认消息之前，消息队列不发送下一个下次到消费者，一次只能处理一个消息
		//限制发送给同一个消费者不得超过一条消息
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);
		
		for (int i = 0; i < 50; i++) {
			String msg = "hello " + i;

			System.out.println("[WQ] send:" +msg);

			channel.basicPublish("", QUEUE_NAME, null, msg.getBytes());
			Thread.sleep(i * 20);
		}

		channel.close();
		connection.close();
	}
}

```



###### 消费者1

```java
package com.jdrx.rabbitmq.workfair;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv1 {

	private static final String QUEUE_NAME = "test_work_queue";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[1] Recv done");
					//手动回执
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};

		//自动应答
		boolean autoAck = false;
		
		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}

```



###### 消费者2

```java
package com.jdrx.rabbitmq.workfair;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv2 {

	private static final String QUEUE_NAME = "test_work_queue";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);  //新加

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] Recv msg" + msg);

				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[2] Recv done");
					channel.basicAck(envelope.getDeliveryTag(), false);  //新加
				}
			}
		};
		//自动应答
		boolean autoAck = false;  //新加

		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}


```



###### 现象

```java
//消费者1
[1] Recv msghello 0
[1] Recv done
[1] Recv msghello 3
[1] Recv done
[1] Recv msghello 6
[1] Recv done
[1] Recv msghello 9
[1] Recv done
[1] Recv msghello 12
[1] Recv done
[1] Recv msghello 15
[1] Recv done
[1] Recv msghello 18
[1] Recv done
[1] Recv msghello 21
[1] Recv done
[1] Recv msghello 23
[1] Recv done
[1] Recv msghello 26
[1] Recv done
[1] Recv msghello 29
[1] Recv done
[1] Recv msghello 32
[1] Recv done
[1] Recv msghello 35
[1] Recv done
[1] Recv msghello 38
[1] Recv done
[1] Recv msghello 41
[1] Recv done
[1] Recv msghello 44
[1] Recv done
[1] Recv msghello 46
[1] Recv done
[1] Recv msghello 49
[1] Recv done


//消费者2
[2] Recv msghello 1
[2] Recv done
[2] Recv msghello 2
[2] Recv done
[2] Recv msghello 4
[2] Recv done
[2] Recv msghello 5
[2] Recv done
[2] Recv msghello 7
[2] Recv done
[2] Recv msghello 8
[2] Recv done
[2] Recv msghello 10
[2] Recv done
[2] Recv msghello 11
[2] Recv done
[2] Recv msghello 13
[2] Recv done
[2] Recv msghello 14
[2] Recv done
[2] Recv msghello 16
[2] Recv done
[2] Recv msghello 17
[2] Recv done
[2] Recv msghello 19
[2] Recv done
[2] Recv msghello 20
[2] Recv done
[2] Recv msghello 22
[2] Recv done
[2] Recv msghello 24
[2] Recv done
[2] Recv msghello 25
[2] Recv done
[2] Recv msghello 27
[2] Recv done
[2] Recv msghello 28
[2] Recv done
[2] Recv msghello 30
[2] Recv done
[2] Recv msghello 31
[2] Recv done
[2] Recv msghello 33
[2] Recv done
[2] Recv msghello 34
[2] Recv done
[2] Recv msghello 36
[2] Recv done
[2] Recv msghello 37
[2] Recv done
[2] Recv msghello 39
[2] Recv done
[2] Recv msghello 40
[2] Recv done
[2] Recv msghello 42
[2] Recv done
[2] Recv msghello 43
[2] Recv done
[2] Recv msghello 45
[2] Recv done
[2] Recv msghello 47
[2] Recv done
[2] Recv msghello 48
[2] Recv done


```



消费者2处理的消息要比消费者1处理的多。能者多劳。



#### 3.消息应答 手动确认消息

```java
boolean autoAck = false;

//监听队列
channel.basicConsume(QUEUE_NAME, autoAck, consumer);

```



- boolean autoAck = true; (自动确认模式)  一旦rabbitmq将消息分发给消费者，就会从内存中删除。

  这种情况下，如果杀死正在执行的消费者，就会丢失正在处理的消息。

  

- boolean autoAck = false;（手动模式）

  如果有一个消费者挂掉，就会交给其他消费者。RabbitMQ支持消息应答，消费者发送一个消息应答，告诉RabbitMQ这个消息我已经处理完成，你可以删除啦，然后RabbitMQ就删除**内存**中的消息。 

  

消息应答默认是打开的，是false。

Message acknowledgment。

- 如果RabbitMQ挂了，我们的消息仍然会丢失。



#### 4.消息的持久化 和非持久化

```java
//声明队列
boolean durable = false； //持久化
channel.queueDeclare(QUEUE_NAME, durable, false, false, null);

```

如果将**运行中的**上述代码中的durable中的false改为ture，那么是不可以的。虽然代码没啥错误，但是运行会报错。

![1594100039023](../media/pictures/MQ.assets/1594100039023.png)

因为我们已经定义了一个test_work_queue这个queue是未持久化的。

**Rabbit不允许使用不同的参数重新定义已经存在的队列。**



如果想改参数，将原来的queue删除掉，或者换个名字，分配新参数就可以持久化啦。



#### 5.publish/subscribe  发布订阅

##### 模型

![1594100598377](../media/pictures/MQ.assets/1594100598377.png)

上面的是一个队列多个消费者，这个是一个队列一个消费者。



##### 解读

- 一个生产者，多个消费者
- 每个消费者都有自己的队列
- 生产者没有直接把消息发送到队列，而是发送给了交换机，转换机 exchange
- 每个队列都要绑定到交换机上
- 生产者发送的消息，经过交换机，到达队列就能实现一个消息被多个消费者消费



注册->邮件->短信



##### 生产者

```java

```



发送成功以后，在这里可以看到

![1594101544682](../media/pictures/MQ.assets/1594101544682.png)



消息哪里去啦？？丢失啦！！因为交换机没有存储能力，在RabbitMQ里面只有队列有存储能力，因为这时候还没有队列绑定到这个交换机，所以数据丢失啦。



![1594102182228](../media/pictures/MQ.assets/1594102182228.png)

下面两个表示这个交换机绑定的两个队列。 右边的Unbind可以手动解除绑定。

##### 消费者1

```java
package com.jdrx.rabbitmq.pb;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 订阅者模式消费者
 *
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv1 {

	private static final String QUEUE_NAME = "test_queue_fanout_email";

	private static final String EXCHANGE_NAME = "test_exchange_fanout";  //fangout 分发的意思

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//绑定队列到交换机 转发器
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "");

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[1] Recv done");
					//手动回执
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};

		//自动应答
		boolean autoAck = false;

		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}


```



##### 消费者2

```java
package com.jdrx.rabbitmq.pb;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 订阅者模式消费者
 *
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv2 {

	private static final String QUEUE_NAME = "test_queue_fanout_sms";

	private static final String EXCHANGE_NAME = "test_exchange_fanout";  //fangout 分发的意思

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//绑定队列到交换机 转发器
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "");

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[2] Recv done");
					//手动回执
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};

		//自动应答
		boolean autoAck = false;

		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}


```



#### 6.交换机 转发器Exchange

一方面是接收生产者的消息，一方面是向队列推送消息。



匿名转发



Fanout（不处理路由键）

![1594102635879](../media/pictures/MQ.assets/1594102635879.png)

Direct (处理路由键)

![1594102772762](../media/pictures/MQ.assets/1594102772762.png)



#### 7.routing  路由模式 路由选择  通配符模式 

##### 模型

![1594102863551](../media/pictures/MQ.assets/1594102863551.png)

##### 生产者

```java
package com.jdrx.rabbitmq.Routing;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.BuiltinExchangeType;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 路由模式
 * @author Steve
 * @date 2020/7/7-10:05
 */
public class Send {

	private static final String EXCHANGE_NAME = "test_exchange_direct";  

	public static void main(String[] args) throws IOException, TimeoutException, InterruptedException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		//声明交换机
		channel.exchangeDeclare(EXCHANGE_NAME, BuiltinExchangeType.DIRECT.getType());   //"direct" 这里有枚举 自己写字符串也行

		//发送消息
		String msg = "hello direct";
		
		//String routingKey = "error";
		String routingKey = "info";       //如果发这个的话，只有消费者2可以收到
		//String routingKey = "warning";  //如果发这个的话，只有消费者2可以收到
		channel.basicPublish(EXCHANGE_NAME,routingKey,null,msg.getBytes());

		System.out.println("Send :" + msg);
		

		channel.close();
		connection.close();
	}
}


```



##### 消费者1

```java
package com.jdrx.rabbitmq.Routing;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 路由模式消费者
 *
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv1 {

	private static final String QUEUE_NAME = "test_queue_direct_1";

	private static final String EXCHANGE_NAME = "test_exchange_direct";  

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//绑定队列到交换机 转发器
		String routingKey = "error";
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, routingKey);

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[1] Recv done");
					//手动回执
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};

		//自动应答
		boolean autoAck = false;

		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}


```



##### 消费者2

```java
package com.jdrx.rabbitmq.Routing;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 路由模式消费者
 *
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv2 {

	private static final String QUEUE_NAME = "test_queue_direct_2";

	private static final String EXCHANGE_NAME = "test_exchange_direct"; 

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//绑定队列到交换机 转发器
		
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "error");
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "info");
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "warning");

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[2] Recv done");
					//手动回执
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};

		//自动应答
		boolean autoAck = false;

		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}


```



#### 8.Topic  Exchange 主题

将路由键和某模式匹配

#匹配一个或者多个

*匹配一个

![1594105326736](../media/pictures/MQ.assets/1594105326736.png)

下面有一些通配符，可以匹配很多。



##### 模型

![1594105524507](../media/pictures/MQ.assets/1594105524507.png)

商品 ： 发布，删除，修改，查询  ... 

##### 生产者

```java
package com.jdrx.rabbitmq.topic;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.BuiltinExchangeType;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * Topic 模式
 *
 * @author Steve
 * @date 2020/7/7-10:05
 */
public class Send {

	private static final String EXCHANGE_NAME = "test_exchange_topic";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		//声明交换机
		channel.exchangeDeclare(EXCHANGE_NAME, BuiltinExchangeType.TOPIC.getType());   //"topic 这里有枚举 自己写字符串也行

		//发送消息
		String msg = "商品...";
		
		String routingKey = "goods.delete"; //商品发布
		channel.basicPublish(EXCHANGE_NAME, routingKey, null, msg.getBytes());

		System.out.println("Send :" + msg);

		channel.close();
		connection.close();
	}
}


```



##### 消费者1

```java
package com.jdrx.rabbitmq.topic;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * Topic模式消费者
 *
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv1 {

	private static final String QUEUE_NAME = "test_queue_topic_1";

	private static final String EXCHANGE_NAME = "test_exchange_topic";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//绑定队列到交换机 转发器
		String routingKey = "goods.add";
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, routingKey);

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[1] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[1] Recv done");
					//手动回执
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};

		//自动应答
		boolean autoAck = false;

		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}


```



##### 消费者2

```java
package com.jdrx.rabbitmq.topic;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * Topic模式消费者
 *
 * @author Steve
 * @date 2020/7/7-10:13
 */
public class Recv2 {

	private static final String QUEUE_NAME = "test_queue_topic_2";

	private static final String EXCHANGE_NAME = "test_exchange_topic";  

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		//绑定队列到交换机 转发器
		String routingKey = "goods.#";  //这里写成通配符
		channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, routingKey);

		//保证一次只有一条
		int prefetchCount = 1;
		channel.basicQos(prefetchCount);

		//定义消费者
		DefaultConsumer consumer = new DefaultConsumer(channel) {
			//消息到达 触发这个方法
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope,
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				String msg = new String(body, "utf-8");
				System.out.println("[2] Recv msg" + msg);

				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				} finally {
					System.out.println("[2] Recv done");
					//手动回执
					channel.basicAck(envelope.getDeliveryTag(), false);
				}
			}
		};

		//自动应答
		boolean autoAck = false;

		//监听队列
		channel.basicConsume(QUEUE_NAME, autoAck, consumer);
	}
}


```



#### 9.rabbitmq 的延时队列



#### 10.Rabbitmq 的消息确认机制（事务+confirm）

在Rabbitmq中，我们可以通过持久化数据，解决rabbitmq服务器异常的数据丢失问题

问题：生产者将消息发送出去之后，消息到底有没有到达rabbitmq服务器



两种方式：

- AMQP 实现了事务机制
- Confirm模式



##### 事务机制

txSelect    txCommit   txRollBack

- txSelect ：用于将当前的channel设置成transation模式
- txCommit：用于提交事务
- txRollBack：回滚事务



###### 生产者 

```java
package com.jdrx.rabbitmq.tx;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.BuiltinExchangeType;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * 事务
 *
 * @author Steve
 * @date 2020/7/7-10:05
 */
public class TxSend {

	private static final String QUEUE_NAME = "test_queue_tx";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		channel.queueDeclare(QUEUE_NAME,false,false,false,null);
		
		String msgString = "hello tx message!";
		
		try {
			channel.txSelect();  //将当前channel设置成事务模式
			channel.basicPublish("", QUEUE_NAME, null, msgString.getBytes());
			
			int i = 1/0;  //模拟出错
			
			System.out.println("send :" + msgString);
			channel.txCommit();  //事务提交
		}catch (Exception e){
			channel.txRollback();  //事务回滚
			System.out.println("send message rollBack");
		}
		
		channel.close();
		connection.close();
	}
}


```



###### 消费者

```java
package com.jdrx.rabbitmq.tx;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * @author Steve
 * @date 2020/7/7-16:15
 */
public class TxRecv {

	private static final String QUEUE_NAME = "test_queue_tx";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取连接
		Connection connection = ConnectionUtils.getConnection();

		//创建信道
		final Channel channel = connection.createChannel();

		//队列声明
		channel.queueDeclare(QUEUE_NAME, false, false, false, null);
		
		channel.basicConsume(QUEUE_NAME,true,new DefaultConsumer(channel){
			@Override
			public void handleDelivery(String consumerTag, Envelope envelope, 
									   AMQP.BasicProperties properties, byte[] body) throws IOException {
				System.out.println("recv[tx] msg: "+ new String(body,"utf-8"));
			}
		});
	}
}


```



此种模式还是很耗时的，采用这种方式，降低了RabbitMQ的消息吞吐量。



##### Confirm 模式

###### 生产者模式confirm的实现原理

![1594110611103](../media/pictures/MQ.assets/1594110611103.png)



Confirm最大的好处就是，他是异步的。

Nack



开启confirm模式



channel.confirmSelect()

编程模式:

- 普通  发一条  waitForConfirms（）
- 批量的  发一批   waitForConfirms （）
- 异步confirm模式：提供一个回调方法



###### confirm 单条消息 

```java
package com.jdrx.rabbitmq.confirm;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * confirm模式  普通模式
 *
 * @author Steve
 * @date 2020/7/7-16:36
 */
public class Send1 {

	private static final String QUEUE_NAME = "test_queue_confirm1";

	public static void main(String[] args) throws IOException, TimeoutException, InterruptedException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		channel.confirmSelect();
		String msgString = "hello confirm message";
		channel.basicPublish("", QUEUE_NAME, null, msgString.getBytes());
		
		if (!channel.waitForConfirms()){
			System.out.println("message send faild");
		}else {
			System.out.println("message send ok");
		}
		
		channel.close();
		connection.close();
	}
}


```



###### confirm 批量发

就加了个for循环

```java
package com.jdrx.rabbitmq.confirm;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

/**
 * confirm模式  批量模式
 *
 * @author Steve
 * @date 2020/7/7-16:36
 */
public class Send2 {

	private static final String QUEUE_NAME = "test_queue_confirm1";

	public static void main(String[] args) throws IOException, TimeoutException, InterruptedException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		channel.confirmSelect();
		String msgString = "hello confirm message batch";

		//批量发  只是加了个for循环
		for (int i = 0; i < 20; i++) {
			channel.basicPublish("", QUEUE_NAME, null, msgString.getBytes());
		}

		//确认
		if (!channel.waitForConfirms()) {
			System.out.println("message send faild");
		} else {
			System.out.println("message send ok");
		}

		channel.close();
		connection.close();
	}
}


```



###### 异步模式

Channel对象提供的ConfirmListerer() 回调方法只包含deliceryTag（当前Channel发出的消息序列），我们需要自己为每一个Channel维护一个unconfirm的消息序列集合，每一个publish一条数据，集合中元素加1，每回调一次HandleAck方法，unconfirm集合删掉相应的一条（multiple=false）或者多条（multile=true）记录。

从程序运行效率上看，这个unconfirm集合孔采用有序集合SortedSet存储结构。





```java
package com.jdrx.rabbitmq.confirm;

import com.jdrx.rabbitmq.utils.ConnectionUtils;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.ConfirmListener;
import com.rabbitmq.client.Connection;

import java.io.IOException;
import java.util.Collections;
import java.util.SortedSet;
import java.util.TreeSet;
import java.util.concurrent.TimeoutException;

/**
 * confirm模式  异步模式
 *
 * @author Steve
 * @date 2020/7/7-16:36
 */
public class Send3 {

	private static final String QUEUE_NAME = "test_queue_confirm1";

	public static void main(String[] args) throws IOException, TimeoutException {
		//获取一个连接
		Connection connection = ConnectionUtils.getConnection();

		//从连接中获取一个通道
		Channel channel = connection.createChannel();

		channel.queueDeclare(QUEUE_NAME, false, false, false, null);

		channel.confirmSelect();

		//未确认的消息标识
		final SortedSet<Long> confirmSet = Collections.synchronizedSortedSet(new TreeSet<Long>());

		//通道添加监听
		channel.addConfirmListener(new ConfirmListener() {

			//没有问题的handleAck
			public void handleAck(long deliveryTag, boolean multiple) throws IOException {
				if (multiple) {
					System.out.println("-----handleAck-----multiple");
					//headSet 返回的是指定元素之前的
					confirmSet.headSet(deliveryTag + 1).clear();
				} else {
					System.out.println("-----handleAck-----multiple false");
					confirmSet.headSet(deliveryTag);
				}
			}

			//handleNack
			public void handleNack(long deliveryTag, boolean multiple) throws IOException {
				if (multiple) {
					System.out.println("-----handleNack-----multiple");
					confirmSet.headSet(deliveryTag + 1).clear();
				} else {
					System.out.println("-----handleNack-----multiple false");
					confirmSet.headSet(deliveryTag);
				}
			}
		});

		String msgString = "sssssss";

		while (true) {
			long seqNo = channel.getNextPublishSeqNo();
			channel.basicPublish("", QUEUE_NAME, null, msgString.getBytes());
			confirmSet.add(seqNo);
		}
	}
}


```



### 4.Spring AMQP Spring-Rabbit

这一部分自己看吧，视频水啦。

参考Spring官网：https://docs.spring.io/spring-amqp/docs/2.3.0-SNAPSHOT/reference/html/









## 














































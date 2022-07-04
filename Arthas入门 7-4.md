arthas简单入门



## Arthas官网

![image-20220704093611532](Arthas 7-4.assets/image-20220704093611532.png)

## 进入quick Start



这里用windows

![image-20220704094221302](Arthas 7-4.assets/image-20220704094221302.png)

这个是用来实验的一个jar包

![image-20220704094300543](Arthas 7-4.assets/image-20220704094300543.png)



### 按tab键可以提示



### 1.先启动math-game.jar

```
java -jar arthas-boot.jar
```

![image-20220704094351311](Arthas 7-4.assets/image-20220704094351311.png)

### 2.启动arthas

```
java -jar arthas-boot.jar
```

### 3.选择线程

我们看到 math-game.jar 

线程1

**输入1敲回车**

![image-20220704094628451](Arthas 7-4.assets/image-20220704094628451.png)



## 仪表盘

```
dashboard
```

![image-20220704094943274](Arthas 7-4.assets/image-20220704094943274.png)

main方法的线程一般为1

![image-20220704095049271](Arthas 7-4.assets/image-20220704095049271.png)

## 线程

```
thread
```

查看1线程

```
thread 1
```

![image-20220704095327636](Arthas 7-4.assets/image-20220704095327636.png)

查看main方法的位置

```
thread 1 | grep  'main('
```

![image-20220704095452313](Arthas 7-4.assets/image-20220704095452313.png)

## 反编译

(将在跑的程序反编译看看)

```
jad demo.MathGame
```

![image-20220704095658764](Arthas 7-4.assets/image-20220704095658764.png)

## 监视

```
watch demo.MathGame primeFactors returnObj
```

![image-20220704100038351](Arthas 7-4.assets/image-20220704100038351.png)

## 离开

```
stop
```

![image-20220704100137750](Arthas 7-4.assets/image-20220704100137750.png)
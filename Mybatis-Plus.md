Mybatis-plus是对mybatis增强的框架



以下是一些基本API



## **QueryWrapper** 条件构造器

创建

```
QueryWrapper<Student> wrapper = new QueryWrapper<>();
```



eq()和allEq,用来构建=,一般用eq()即可

```
wrapper.eq("id","1");
```

```
       HashMap<String, String> map = new HashMap<>();
       map.put("id","1");
       map.put("name","张三");
       wrapper.allEq(map,true);
```



ne(),不等于

```
wrapper.ne("id","1");
```



gt大于,ge大于等于,lt小于,le小于等于

```
wrapper.le("age",18);
```



between, notBetween

```
wrapper.between("id","1","3");
```

```
wrapper.notBetween("id",1.1,"2");
```



模糊查询 like,notLike,likeLeft,likeRight

```
wrapper.like("name","张");
//SELECT id,country,name,age,likes FROM student WHERE (name LIKE ?) ,Parameters: %张%(String)

wrapper.notLike("name","张");
//SELECT id,country,name,age,likes FROM student WHERE (name NOT LIKE ?) ,Parameters: %张%(String)

wrapper.likeRight("name","张");
//SELECT id,country,name,age,likes FROM student WHERE (name LIKE ?) ,张%(String)

wrapper.likeLeft("name","三");
//SELECT id,country,name,age,likes FROM student WHERE (name LIKE ?) ,%三(String)
```



isNull 为空 isNotNull不为空

```
wrapper.isNotNull("UPDATE_TIME");
```



in,notin ,orderByDesc降序 orderByAsc升序

```
String[] arr = {"1","2","3","5"};
List<String> list = Arrays.asList(arr);
wrapper.in("id", list);
wrapper.orderByDesc("id");
wrapper.orderByAsc("id");
```



having

```
wrapper.in("id","1","2","3","5");
wrapper.gt("age","12");
wrapper.having("sum(id) > 3");
```



or & and

```
wrapper.eq("id","2")
		.and(i->i.eq("name","lisi"))
        .or().eq("id","1")
        .or().eq("id","3");
```



nested

```
wrapper.nested(i->i.eq("id","1").eq("name","张三"))
       .or().eq("id","2");   
       
       //SELECT * FROM student WHERE (( (id = ? AND name = ?) ) OR id = ?)
```



apply 这个好用,写固定格式

```
wrapper.apply("id = '1' AND name ='张三' OR id='3'"); 

//SELECT * FROM student WHERE (id = '1' AND name ='张三' OR id='3')
```



last 相当于在后边拼接一个String字符串,多个.last()的话以最后一个为准

```
wrapper.apply("id = '1' AND name ='张三' OR id='3'");
wrapper.last("OR id = '4'");
//SELECT * FROM student WHERE (id = '1' AND name ='张三' OR id='3') OR id = '4'
wrapper.last("limit 1");
```



notExists,exists

```
wrapper.exists("select * from sorces  where student.id= sorces.student_id");
```



select 选择要查询的字段

```
wrapper.select("id","name");
wrapper.nested(i->i.eq("id","1"))
       .or().eq("id","2");
wrapper.orderByDesc("age");
wrapper.last("limit 1");
```



## UpdateWrapper


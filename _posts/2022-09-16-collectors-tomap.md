---
id: 473
title: Collectors.toMap
date: '2022-09-16T10:08:34+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=473'
permalink: /index.php/2022/09/16/collectors-tomap/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Java
---

<div>### **1.使用规则：**

toMap(Function, Function) 返回一个 Collector，它将元素累积到一个 Map中，其键和值是将提供的映射函数应用于输入元素的结果。

如果映射的键包含重复项，则在执行收集操作时会抛出IllegalStateException。如果映射的键可能有重复项，请改用 toMap(Function, Function, BinaryOperator)。

### **2.我们测试一下，首先新建一个Sdudent 类，三个属性分别是id，name，group**

然后构造一个List

List<Student> list = new ArrayList<>();

for (int i = 1; i < 4; i++) {

list.add(new Student(i+"","学生"+i));

}

**1. 将list转成以id为key的map，value是id对应的Sudent对象：**

Map<String, Student> map = list.stream().collect(Collectors.toMap(Student::getId, Function.identity()));

**2.假如id存在重复值，则会报错Duplicate key xxx, 解决方案是：**

只取后一个key及value：

Map<String, Student> map = list.stream().collect(Collectors.toMap(Student::getId,Function.identity(),(oldValue,newValue) -> newValue))

只取前一个key及value：

Map<String, Student> map = list.stream().collect(Collectors.toMap(Student::getId,Function.identity(),(oldValue,newValue) -> oldValue))

**3.想获得一个id和name对应的Map<String, String> ：**

Map<String, String> map = list.stream().collect(Collectors.toMap(Student::getId,Student::getName));

***注意：name可以为空字符串但不能为null，否则会报空指针，解决方案：***

Map<String, String> map = list.stream().collect(Collectors.toMap(Student::getId, e->e.getName()==null?"":e.getName()));

***假如存在id重复，两个vaue可以这样映射到同一个id：***

Map<String, String> map = list.stream().collect(Collectors.toMap(Student::getId,Student::getName,(e1,e2)->e1+","+e2));

**4.把Student集合按照group分组到map中**

Map<String, List<Student>> map = list.stream().collect(Collectors.groupingBy(Student::getGroup));

**5.过滤去重，两个List<Student>**

List<Student> list1 = new ArrayList<>();

List<Student> list2= new ArrayList<>();

HashMap<String, String> hashMap = new HashMap<>();

for (int i = 1; i < 4; i++) {

list1.add(new Student(i+"","学生"+i));

}

for (int i = 2; i < 5; i++) {

list2.add(new Student(i+"","学生"+i));

}

Map<String, Student> map2 = list2.stream().collect(Collectors.toMap(Student::getId,Function.identity()));

**//把List1和List2中id重复的Student对象的name取出来：**

List<String> strings = list1.stream().map(Student::getId).filter(map2::containsKey).map(map2::get).map(Student::getName).collect(Collectors.toList());

System.out.println(strings);// 输出 \[学生2, 学生3\]

</div>
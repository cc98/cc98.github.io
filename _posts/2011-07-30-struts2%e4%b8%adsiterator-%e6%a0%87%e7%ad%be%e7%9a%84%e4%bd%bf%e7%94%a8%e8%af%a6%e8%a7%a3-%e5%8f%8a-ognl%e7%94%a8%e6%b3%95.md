---
layout: post
title: struts2中s:iterator 标签的使用详解 及 OGNL用法
date: 2011-07-30 12:33:44.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Labrary
tags: []
meta:
  views: '5484'
  _edit_last: '1'
  bot_views: '3'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/324.html"
---
简单的demo：  
s:iterator&nbsp;标签有3个属性：  
value：被迭代的集合  
id&nbsp;&nbsp;&nbsp;：指定集合里面的元素的id  
status&nbsp;迭代元素的索引  
1:jsp页面定义元素写法&nbsp;数组或list

\<s:iterator value="{'1','2','3','4','5'}" \>  
\<s:property value='number'/\>A  
\</s:iterator\>  
打印结果为: 1A2A3A4A5A  
2:索引的用法  
如果指定了status，每次的迭代数据都有IteratorStatus的实例，它有以下几个方法  
int getCount()返回当前迭代了几个元素  
int getIndex()返回当前元素索引  
boolean isEven()当然的索引是否偶数  
boolean isFirst()当前是否第一个元素  
boolean isLast()  
boolean isOdd()当前元素索引是否奇数  
\<s:iterator value="{'a','b','c'}" status='st'\>  
\<s:if test="#st.Even"\>  
现在的索引是奇数为:\<s:property value='#st.index'/\>  
\</s:if\>  
当前元素值：\<s:property value='char'/\>  
\</s:iterator\>  
3：遍历map  
value可以直接定义为：  
value="#{"1":"a","2":"b"}"  
每个元素以都好隔开。元素之间的key和value&nbsp;冒号隔开  
value也可以是数据栈里面的java.util.Map对象  
遍历写法如下：  
\<s:iterator value="map" status="st"\>  
key : \<s:property value='key'/\>  
value:\<s:property vlaue='value'/\>  
\</s:iterator\>  
当然key&nbsp;和value&nbsp;都可以使java&nbsp;的&nbsp;Object  
3：遍历数据栈.简单的List类，  
List\<Attr\>  
class Attr{String attrName;String getAttrName(){return "123";}}  
\<s:iterator value="label" \>  
\<s:property value="#id.attrName" /\>  
\</s:iterator\>  
当然value&nbsp;还可以写成&nbsp;value="%{label}" label可以有.操作  
label的属性List&nbsp;可以写成value="%{label.list}"&nbsp;相当于：getLabel().getList();  
4：遍历2个list；  
List\<AttrName\> attrN {color,size,style}  
List\<AttrValue\> attrV {red,20,gay}  
这2个list的元素是一一对应的，一个attrN对应一个attrV  
\<s:iterator value="%{attrN }" &nbsp;&nbsp; status="status"\>  
index&nbsp;&nbsp;&nbsp; is : \<s:property value='status.index'/\>  
attrName is : \<s:property value='id'/\> or \<s:property value='%{id}'/\>  
attrName is : \<s:property value='%{attrV[#status.index]}'/\>  
\</s:iterator\>

\<s:bean \>  
\<s:param value="5" /\>  
\<s:param value="10" /\>  
\<s:iterator\>  
counter:\<s:property/\>  
\</s:iterator\>  
\</s:bean\>

<!--more-->

这个标签主要的的作用就是迭代出集合。。  
value属性表示需要跌代显示出来的值。  
status属性，又来保存迭代时的一些状态值。

注：  
1.如果需要引用valueStack中的值，需要使用这样的形式。  
\<s:iterator value="#userList" /\> //userList在action部分被保存在Request中，所以使用#加属性名来引用值。  
2.如果集合的值是通过action的方法，假设我们的action中有一个getListMenu方法，返回一个List集合。  
我们可以使用如下的形式来引用这个集合，并用s:iterator来输出。  
\<s:iterator value="listMenu" /\>  
3.iterator的value使用定义好的方式，如：  
\<s:iterator value="{1,2,3,4}" /\>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //这样跌代输出的值就是1.2.3.4这四个值。

二、iterator中输出具体值，如果，在上面我们的list中的对象，有两个属性，都是String类型，一个是name,一个是url。  
我们可以这样来引用。  
1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<s:property value="name" /\>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //这样我们将可以输出跌代对象的name属性值。  
2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果我们希望使用\<s:url /\>来将跳转过后的url进行处理，该如何来做？  
\<s:url value="%{url}"/\>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //%{}ognl的表达式，这样的值能够将url的值进行\<s:url/\>的处理  
实际上就是转为绝对路径。这样，我们就可以对付一些因跳转换产生的路径问题。  
原因：因为\<s:iteratotr /\>以后，当前的对象应该就在ValueStack顶部了，这样当然的url实际上就是对象的url&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;属性了

三、使用ognl输出对应的值。  
\<s:textfield value="%{#request.loginNames}"/\>

使用此表达式，会生成一个文本框，并且，如果request.attribute中有loginNames属性，将会做为些文本框的默认值。  
如果只使用#request.loginNames在struts2的标签内部，是不会显示任何值的，注意外面加上的%{}附号，才会被正常的使用。  
如果希望如EL语言一样直接输出文件，如在一个\<a\>\</a\>之间的innerHTML文本为#request.loginNames的值，我们只要使用：\<s:property value="#request.loginNames" /\>使可以正常使用！

注：  
1.${}是EL语言的&nbsp;%{}这样的形式是ognl表过式语言的，在struts2的标签内部，使用%{}这样的形式，在标签外部可以使用${}EL语言的方式。如果在struts2的标签内部使用${}这样的方式，会出现以下的错误提示：  
According to TLD or attribute directive in tag file, attribute value does not accept any expressions  
2.很多时候，我们使用struts2的一些标签，属性是需要接受集合的，如果集合是保存在request,session，或者是值栈(非根对象的栈顶)，可以使用#变量名的方式，如果获取的值是在Action中通过特定的方法来获取，就需要使用如&nbsp;value="userList"这样的方式，只是去掉了前面的#。

&nbsp;

[struts2中的OGNL用法](http://www.cnblogs.com/macooma/articles/1662607.html)

User对象属性获取  
如User中有username和password字段  
获取username属性\<s:property value="user.username" /\>  
获取password属性\<s:property value="user.password" /\>

若User中又包含定义了address对象，address对象中包含有addr属性，则可以这样访问  
获取addr属性\<s:property value="user.address.addr" /\>

若User中还包含一个get()的普通方法，可以这样调用  
\<s:property value="user.get()" /\>  
以上是调用值栈中对象的普通方法，user为值栈中的对象

调用action中的静态方法get()，普通方法不能直接调用  
\<s:property value="@com.netshuai.action.ManagerAction@get()" /\>  
以上为调用非值栈中的静态方法

调用JDK中类的静态方法\<s:property value="@java.lang.Math@floor(32.56)" /\>  
上例也可写成\<s:property value="@@floor(32.56)" /\>，省略前面的类则默认使用java.lang.Math类，其他类不可省略

调用普通类中的静态属性\<s:property value="@com.netshuai.model.Address@city" /\>  
address中的city静态属性要用public声明

调用普通类的构造方法，如构造方法为  
public User(String username)  
{  
this.username=username;  
}  
调用方法为\<s:property value="new com.netshuai.model.User('hello').username" /\>，则返回username值为hello

获取List\<s:property value="list" /\>  
获取List中的某一个元素\<s:property value="list[0]" /\>  
获取List的大小\<s:property value="list.size" /\>  
获取Set\<s:property value="set" /\>  
无法获取Set中的某一个元素，因为Set没有顺序  
获取Map\<s:property value="map" /\>  
获取Map中所有key的值\<s:property value="map.keys" /\>  
获取Map中所有value的值\<s:property value="map.values" /\>  
获取Map中的某一个元素\<s:property value="map['k1']" /\>

获取List所有对象\<s:property value="listObject" /\>，需要重写toString()方法才能正常显示对象的值  
利用投影获取List中所有对象的username属性\<s:property value="listObject.{username}" /\>  
利用投影获取List中第一个对象的username属性\<s:property value="listObject.{username}[0]" /\>  
利用选择获取List中年龄大于30的对象\<s:property value="listObject.{?#this.age\>30}" /\>  
利用选择获取List中年龄大于30的对象的username\<s:property value="listObject.{?#this.age\>30}.{username}" /\>  
利&nbsp;用选择获取List中年龄大于30的第一个对象的username\<s:property value="listObject.{?#this.age\>30}.{username}[0]" /\>或\<s:property value="listObject.{^#this.age\>30}.{username}" /\>  
利用选择获取List中年龄大于30的最后一个对象的username\<s:property value="listObject.{$#this.age\>30}.{username}" /\>

获取parameters中的属性\<s:property value="#parameters.name" /\>  
获取request中的属性\<s:property value="#request.name" /\>  
获取session中的属性\<s:property value="#session.name" /\>  
获取application中的属性\<s:property value="#application.name" /\>  
\<s:property value="#attr.name" /\>按顺序遍历上面四个对象，然后返回首先找到的值

%{}可以取出存在值堆栈中的Action对象，直接调用它的方法，如%{getText('key')}可以取出国际化信息

${}可以用在国际化资源文件中和struts2配置文件中

使用top获取值栈中第二个对象\<s:property value="[1].top.user"/\>  
使用top获取值栈中第二个对象的属性\<s:property value="[1].user"/\>

调用值栈中action的静态方法get()\<s:property value="@vs@get()"/\>，vs也可写做vs1  
调用值栈中第二个action的静态方法get()\<s:property value="@vs2@get()"/\>

将一个对象放入值栈  
ActionContext.getContext().getValueStack().push(user);

&nbsp;


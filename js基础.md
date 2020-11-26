##数组
1. 创建一个数组：
```
常规模式:
var myCars=new Array();
myCars[0]="Saab";      
myCars[1]="Volvo";
myCars[2]="BMW";
简洁模式：
var myCars=new Array("Saab","Volvo","BMW");
字面：
var myCars=["Saab","Volvo","BMW"];

```

*常规模式和简洁的区别是：常规模式将数组的声明和初始化分别完成*
*字面量是根据等号后面的数据类型来确定变量的数据类型*

2. 数组的访问

根据变量名和数据下标可以找到数组中任意元素
```
myArray[0]=Date.now;
myArray[1]=myFunction;
myArray[2]=myCars;
```

3. 数组的属性和方法
**数组的属性：**

|属性|描述|
|---|---|
|constructor|返回创建数组对象的原型函数。|
|length|设置或返回数组元素的个数。|
|prototype|允许你向数组对象添加属性或方法。|

constructor:返回数组对象原型创建的函数：

```
fruits.constructor; //返回：function Array() { [native code] }
```
length:返回数组长度
prototype: 
>prototype属性使您有能力向对象添加属性和方法。

>当构建一个属性，所有的数组将被设置属性，它是默认值。

>在构建一个方法时，所有的数组都可以使用该方法。

>注意： Array.prototype 单独不能引用数组, Array() 对象可以。

>注意： 在JavaScript对象中，Prototype是一个全局属性。
实例：
```
设置方法：
一个新的数组的方法，将数组值转为大写：

Array.prototype.myUcase=function()
{
    for (i=0;i<this.length;i++)
    {
        this[i]=this[i].toUpperCase();
    }
}
创建一个数组，然后调用 myUcase 方法：

var fruits=["Banana","Orange","Apple","Mango"];
fruits.myUcase();
fruits 数组现在的值为：

BANANA,ORANGE,APPLE,MANGO

设置属性：
Array.prototype.name=value

```

**数组的方法：**
	
	
	
  
 
|方法|描述|用法|
|---|---|---|
|concat()|连接两个或更多的数组，并返回结果。|array1.concat(array2,array3,...,arrayX)|
|copyWithin()|从数组的指定位置拷贝元素到数组的另一个指定位置中。|copyWithin() 方法用于从数组的指定位置拷贝元素到数组的另一个指定位置中。array.copyWithin(target, start, end)|
|entries()|返回数组的可迭代对象。|见下方|
|every()|检测数值元素的每个元素是否都符合条件。|[every][1]|
|fill()	      |使用一个固定值来填充数组。 |fill() 方法用于将一个固定值替换数组的元素。arr.fill(value[, start[, end]])|
|filter()	  | 检测数值元素，并返回符合条件所有元素的数组。 |[filter][2]|
|find()	      | 返回符合传入测试（函数）条件的数组元素。||
|findIndex()  | 返回符合传入测试（函数）条件的数组元素索引。 ||
|forEach()	  | 数组每个元素都执行一次回调函数。 ||
|from()	      | 通过给定的对象中创建一个数组。 ||
|includes()	  | 判断一个数组是否包含一个指定的值。 ||
|indexOf()	  | 搜索数组中的元素，并返回它所在的位置。 ||
|isArray()	  | 判断对象是否为数组。 ||
|join()	      | 把数组的所有元素放入一个字符串。 ||
|keys()	      | 返回数组的可迭代对象，包含原始数组的键(key)。 ||
|lastIndexOf()| 搜索数组中的元素，并返回它最后出现的位置。 ||
|map()	      | 通过指定函数处理数组的每个元素，并返回处理后的数组。 ||
|pop()	      | 删除数组的最后一个元素并返回删除的元素。 ||
|push()    	  | 向数组的末尾添加一个或更多元素，并返回新的长度。 ||
|reduce()	  | 将数组元素计算为一个值（从左到右）。 ||
|reduceRight()| 将数组元素计算为一个值（从右到左）。 ||
|reverse()    | 反转数组的元素顺序。 ||
|shift()	  | 删除并返回数组的第一个元素。 ||
|slice()	  | 选取数组的一部分，并返回一个新数组。 ||
|some()       | 检测数组元素中是否有元素符合指定条件。 ||
|sort()	      | 对数组的元素进行排序。 ||
|splice()	  | 从数组中添加或删除元素。 ||
|toString()   | 把数组转换为字符串，并返回结果。 ||
|unshift()	  | 向数组的开头添加一个或更多元素，并返回新的长度。 ||
|valueOf()    | 返回数组对象的原始值。||
entries的使用方法:
```
var arr = ["a", "b", "c"];
var iter = arr.entries();
var a = [];

// for(var i=0; i< arr.length; i++){   // 实际使用的是这个 
for(var i=0; i< arr.length+1; i++){    // 注意，是length+1，比数组的长度大
    var tem = iter.next();             // 每次迭代时更新next
    console.log(tem.done);             // 这里可以看到更新后的done都是false
    if(tem.done !== true){             // 遍历迭代器结束done才是true
        console.log(tem.value);
        a[i]=tem.value;
    }
}
    
console.log(a);
```


##日期方法	      

|方法|描述||
|---|---|---|
|getDate()	      |从 Date 对象返回一个月中的某一天 (1 ~ 31)。||
|getDay()	      |从 Date 对象返回一周中的某一天 (0 ~ 6)。||
|getFullYear()    |从 Date 对象以四位数字返回年份。||
|getHours()	      |返回 Date 对象的小时 (0 ~ 23)。||
|getMilliseconds()|返回 Date 对象的毫秒(0 ~ 999)。||
|getMinutes()	  |返回 Date 对象的分钟 (0 ~ 59)。||
|getMonth()       |从 Date 对象返回月份 (0 ~ 11)。||
|getSeconds()	  |返回 Date 对象的秒数 (0 ~ 59)。||
|getTime()	      |返回 1970 年 1 月 1 日至今的毫秒数。||


##Math 对象
	         
|方法|描述||
|---|---|---|
|abs(x)	         |返回 x 的绝对值。||
|acos(x)	     |返回 x 的反余弦值。||
|asin(x)	     |返回 x 的反正弦值。||
|atan(x)	     |以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。||
|atan2(y,x)	     |返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。||
|ceil(x)	     |对数进行上舍入。||
|cos(x)	         |返回数的余弦。||
|exp(x)	         |返回 Ex 的指数。||
|floor(x)	     |对 x 进行下舍入。||
|log(x)	         |返回数的自然对数（底为e）。||
|max(x,y,z,...,n)|返回 x,y,z,...,n 中的最高值。||
|min(x,y,z,...,n)|返回 x,y,z,...,n中的最低值。||
|pow(x,y)	     |返回 x 的 y 次幂。||
|random()	     |返回 0 ~ 1 之间的随机数。||
|round(x)	     |四舍五入。||
|sin(x)	         |返回数的正弦。||
|sqrt(x)   	     |返回数的平方根。||
|tan(x)	         |返回角的正切。||

##Number 对象方法

	
  

|方法|描述|用法|
|---|---|---|
|isFinite	     |检测指定参数是否为无穷大。||
|toExponential(x)|  把对象的值转换为指数计数法。||
|toFixed(x)      |  把数字转换为字符串，结果的小数点后有指定位数的数字。||
|toPrecision(x)	 |  把数字格式化为指定的长度。||
|toString()	     |  把数字转换为字符串，使用指定的基数。||
|valueOf()	     |  返回一个 Number 对象的基本数字值。||

##String 对象属性

方法	描述
	        

||||
|---|---|---|
|charAt()	        | 返回在指定位置的字符。||
|charCodeAt()	    | 返回在指定的位置的字符的 Unicode 编码。||
|concat()	        | 连接两个或更多字符串，并返回新的字符串。||
|fromCharCode()	    | 将 Unicode 编码转为字符。||
|indexOf()	        | 返回某个指定的字符串值在字符串中首次出现的位置。||
|includes()	        | 查找字符串中是否包含指定的子字符串。||
|lastIndexOf()	    | 从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置。||
|match()	            | 查找找到一个或多个正则表达式的匹配。||
|repeat()	        | 复制字符串指定次数，并将它们连接在一起返回。||
|replace()	        | 在字符串中查找匹配的子串， 并替换与正则表达式匹配的子串。||
|search()	        | 查找与正则表达式相匹配的值。||
|slice()	            | 提取字符串的片断，并在新的字符串中返回被提取的部分。||
|split()	            | 把字符串分割为字符串数组。||
|startsWith()	    | 查看字符串是否以指定的子字符串开头。||
|substr()	        | 从起始索引号提取字符串中指定数目的字符。||
|substring()	        | 提取字符串中两个指定的索引号之间的字符。||
|toLowerCase()	    | 把字符串转换为小写。||
|toUpperCase()	    | 把字符串转换为大写。||
|trim()	            | 去除字符串两边的空白||
|toLocaleLowerCase()	| 根据本地主机的语言环境把字符串转换为小写。||
|toLocaleUpperCase()	| 根据本地主机的语言环境把字符串转换为大写。||
|valueOf()	        | 返回某个字符串对象的原始值。||
|toString()| 返回一个字符串。||


















[1]:every() 方法用于检测数组所有元素是否都符合指定条件（通过函数提供）。
every() 方法使用指定函数检测数组中的所有元素：
如果数组中检测到有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测。如果所有元素都满足条件，则返回 true。
注意： every() 不会对空数组进行检测。
注意： every() 不会改变原始数组

[2]:filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。
注意： filter() 不会对空数组进行检测。
注意： filter() 不会改变原始数组。
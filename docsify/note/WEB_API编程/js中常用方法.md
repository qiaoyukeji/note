###  1、 JavaScript 的三种弹出框（alert，confirm，prompt）

JavaScript 有三种类型的弹出框：警告框、确认框和提示框。

#### 1. 警告框（alert）

如果要确保信息传递给用户，通常会使用警告框。

当警告框弹出时，用户将需要单击“确定”来继续。

```js
alert("hello world");
alert("hello\nworld"); // \n 会使弹出框换行
```

![image-20200506180023706](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200506180025.png)

#### 2. 确认框（confirm）

如果您希望用户验证或接受某个东西，则通常使用“确认”框。

当确认框弹出时，用户将不得不单击“确定”或“取消”来继续进行。

如果用户单击==“确定”，该框返回 true==。如果用户单击==“取消”，该框返回 false==。

```js
var i = confirm('hello world')
console.log(i);//当点击确定时，打印true，点击取消时，打印false
```

![image-20200506175358717](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200506175400.png)

#### 3. 提示框（prompt）

如果您希望用户在进入页面前输入值，通常会使用提示框。

当提示框弹出时，用户将不得不输入值后单击“确定”或点击“取消”来继续进行。

###### 如果用户单击==“确定”，该框返回输入值==。如果用户单击==“取消”，该框返回 NULL==。

```js
var j = prompt('hello world')
console.log(j);
```

![image-20200506175729747](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200506175731.png)

![image-20200506175815454](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200506175816.png)

### 2、JavaScript 中一些预定义方法

#### 1. Array 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [concat()](https://www.w3school.com.cn/jsref/jsref_concat_array.asp) | 连接两个或更多的数组，并返回结果。                           |
| [join()](https://www.w3school.com.cn/jsref/jsref_join.asp)   | 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。 |
| [pop()](https://www.w3school.com.cn/jsref/jsref_pop.asp)     | 删除并返回数组的最后一个元素                                 |
| [push()](https://www.w3school.com.cn/jsref/jsref_push.asp)   | 向数组的末尾添加一个或更多元素，并返回新的长度。             |
| [reverse()](https://www.w3school.com.cn/jsref/jsref_reverse.asp) | 颠倒数组中元素的顺序。                                       |
| [shift()](https://www.w3school.com.cn/jsref/jsref_shift.asp) | 删除并返回数组的第一个元素                                   |
| [slice()](https://www.w3school.com.cn/jsref/jsref_slice_array.asp) | 从某个已有的数组返回选定的元素                               |
| [sort()](https://www.w3school.com.cn/jsref/jsref_sort.asp)   | 对数组的元素进行排序                                         |
| [splice()](https://www.w3school.com.cn/jsref/jsref_splice.asp) | 删除元素，并向数组添加新元素。                               |
| [toSource()](https://www.w3school.com.cn/jsref/jsref_tosource_array.asp) | 返回该对象的源代码。                                         |
| [toString()](https://www.w3school.com.cn/jsref/jsref_toString_array.asp) | 把数组转换为字符串，并返回结果。                             |
| [toLocaleString()](https://www.w3school.com.cn/jsref/jsref_toLocaleString_array.asp) | 把数组转换为本地数组，并返回结果。                           |
| [unshift()](https://www.w3school.com.cn/jsref/jsref_unshift.asp) | 向数组的开头添加一个或更多元素，并返回新的长度。             |
| [valueOf()](https://www.w3school.com.cn/jsref/jsref_valueof_array.asp) | 返回数组对象的原始值                                         |



#### 2. Date 对象方法

| 方法                                                         | 描述                                                   |
| :----------------------------------------------------------- | :----------------------------------------------------- |
| [Date()](https://www.w3school.com.cn/jsref/jsref_Date.asp)   | 返回当日的日期和时间。                                 |
| [getDate()](https://www.w3school.com.cn/jsref/jsref_getDate.asp) | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。            |
| [getDay()](https://www.w3school.com.cn/jsref/jsref_getDay.asp) | 从 Date 对象返回一周中的某一天 (0 ~ 6)。               |
| [getMonth()](https://www.w3school.com.cn/jsref/jsref_getMonth.asp) | 从 Date 对象返回月份 (0 ~ 11)。                        |
| [getFullYear()](https://www.w3school.com.cn/jsref/jsref_getFullYear.asp) | 从 Date 对象以四位数字返回年份。                       |
| [getYear()](https://www.w3school.com.cn/jsref/jsref_getYear.asp) | 请使用 getFullYear() 方法代替。                        |
| [getHours()](https://www.w3school.com.cn/jsref/jsref_getHours.asp) | 返回 Date 对象的小时 (0 ~ 23)。                        |
| [getMinutes()](https://www.w3school.com.cn/jsref/jsref_getMinutes.asp) | 返回 Date 对象的分钟 (0 ~ 59)。                        |
| [getSeconds()](https://www.w3school.com.cn/jsref/jsref_getSeconds.asp) | 返回 Date 对象的秒数 (0 ~ 59)。                        |
| [getMilliseconds()](https://www.w3school.com.cn/jsref/jsref_getMilliseconds.asp) | 返回 Date 对象的毫秒(0 ~ 999)。                        |
| [getTime()](https://www.w3school.com.cn/jsref/jsref_getTime.asp) | 返回 1970 年 1 月 1 日至今的毫秒数。                   |
| [getTimezoneOffset()](https://www.w3school.com.cn/jsref/jsref_getTimezoneOffset.asp) | 返回本地时间与格林威治标准时间 (GMT) 的分钟差。        |
| [getUTCDate()](https://www.w3school.com.cn/jsref/jsref_getUTCDate.asp) | 根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。        |
| [getUTCDay()](https://www.w3school.com.cn/jsref/jsref_getUTCDay.asp) | 根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。         |
| [getUTCMonth()](https://www.w3school.com.cn/jsref/jsref_getUTCMonth.asp) | 根据世界时从 Date 对象返回月份 (0 ~ 11)。              |
| [getUTCFullYear()](https://www.w3school.com.cn/jsref/jsref_getUTCFullYear.asp) | 根据世界时从 Date 对象返回四位数的年份。               |
| [getUTCHours()](https://www.w3school.com.cn/jsref/jsref_getUTCHours.asp) | 根据世界时返回 Date 对象的小时 (0 ~ 23)。              |
| [getUTCMinutes()](https://www.w3school.com.cn/jsref/jsref_getUTCMinutes.asp) | 根据世界时返回 Date 对象的分钟 (0 ~ 59)。              |
| [getUTCSeconds()](https://www.w3school.com.cn/jsref/jsref_getUTCSeconds.asp) | 根据世界时返回 Date 对象的秒钟 (0 ~ 59)。              |
| [getUTCMilliseconds()](https://www.w3school.com.cn/jsref/jsref_getUTCMilliseconds.asp) | 根据世界时返回 Date 对象的毫秒(0 ~ 999)。              |
| [parse()](https://www.w3school.com.cn/jsref/jsref_parse.asp) | 返回1970年1月1日午夜到指定日期（字符串）的毫秒数。     |
| [setDate()](https://www.w3school.com.cn/jsref/jsref_setDate.asp) | 设置 Date 对象中月的某一天 (1 ~ 31)。                  |
| [setMonth()](https://www.w3school.com.cn/jsref/jsref_setMonth.asp) | 设置 Date 对象中月份 (0 ~ 11)。                        |
| [setFullYear()](https://www.w3school.com.cn/jsref/jsref_setFullYear.asp) | 设置 Date 对象中的年份（四位数字）。                   |
| [setYear()](https://www.w3school.com.cn/jsref/jsref_setYear.asp) | 请使用 setFullYear() 方法代替。                        |
| [setHours()](https://www.w3school.com.cn/jsref/jsref_setHours.asp) | 设置 Date 对象中的小时 (0 ~ 23)。                      |
| [setMinutes()](https://www.w3school.com.cn/jsref/jsref_setMinutes.asp) | 设置 Date 对象中的分钟 (0 ~ 59)。                      |
| [setSeconds()](https://www.w3school.com.cn/jsref/jsref_setSeconds.asp) | 设置 Date 对象中的秒钟 (0 ~ 59)。                      |
| [setMilliseconds()](https://www.w3school.com.cn/jsref/jsref_setMilliseconds.asp) | 设置 Date 对象中的毫秒 (0 ~ 999)。                     |
| [setTime()](https://www.w3school.com.cn/jsref/jsref_setTime.asp) | 以毫秒设置 Date 对象。                                 |
| [setUTCDate()](https://www.w3school.com.cn/jsref/jsref_setUTCDate.asp) | 根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。        |
| [setUTCMonth()](https://www.w3school.com.cn/jsref/jsref_setUTCMonth.asp) | 根据世界时设置 Date 对象中的月份 (0 ~ 11)。            |
| [setUTCFullYear()](https://www.w3school.com.cn/jsref/jsref_setUTCFullYear.asp) | 根据世界时设置 Date 对象中的年份（四位数字）。         |
| [setUTCHours()](https://www.w3school.com.cn/jsref/jsref_setutchours.asp) | 根据世界时设置 Date 对象中的小时 (0 ~ 23)。            |
| [setUTCMinutes()](https://www.w3school.com.cn/jsref/jsref_setUTCMinutes.asp) | 根据世界时设置 Date 对象中的分钟 (0 ~ 59)。            |
| [setUTCSeconds()](https://www.w3school.com.cn/jsref/jsref_setUTCSeconds.asp) | 根据世界时设置 Date 对象中的秒钟 (0 ~ 59)。            |
| [setUTCMilliseconds()](https://www.w3school.com.cn/jsref/jsref_setUTCMilliseconds.asp) | 根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。           |
| [toSource()](https://www.w3school.com.cn/jsref/jsref_tosource_boolean.asp) | 返回该对象的源代码。                                   |
| [toString()](https://www.w3school.com.cn/jsref/jsref_toString_date.asp) | 把 Date 对象转换为字符串。                             |
| [toTimeString()](https://www.w3school.com.cn/jsref/jsref_toTimeString.asp) | 把 Date 对象的时间部分转换为字符串。                   |
| [toDateString()](https://www.w3school.com.cn/jsref/jsref_toDateString.asp) | 把 Date 对象的日期部分转换为字符串。                   |
| [toGMTString()](https://www.w3school.com.cn/jsref/jsref_toGMTString.asp) | 请使用 toUTCString() 方法代替。                        |
| [toUTCString()](https://www.w3school.com.cn/jsref/jsref_toUTCString.asp) | 根据世界时，把 Date 对象转换为字符串。                 |
| [toLocaleString()](https://www.w3school.com.cn/jsref/jsref_toLocaleString.asp) | 根据本地时间格式，把 Date 对象转换为字符串。           |
| [toLocaleTimeString()](https://www.w3school.com.cn/jsref/jsref_toLocaleTimeString.asp) | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。 |
| [toLocaleDateString()](https://www.w3school.com.cn/jsref/jsref_toLocaleDateString.asp) | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。 |
| [UTC()](https://www.w3school.com.cn/jsref/jsref_utc.asp)     | 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。  |
| [valueOf()](https://www.w3school.com.cn/jsref/jsref_valueOf_date.asp) | 返回 Date 对象的原始值。                               |

#### 3. Math 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [abs(x)](https://www.w3school.com.cn/jsref/jsref_abs.asp)    | 返回数的绝对值。                                             |
| [acos(x)](https://www.w3school.com.cn/jsref/jsref_acos.asp)  | 返回数的反余弦值。                                           |
| [asin(x)](https://www.w3school.com.cn/jsref/jsref_asin.asp)  | 返回数的反正弦值。                                           |
| [atan(x)](https://www.w3school.com.cn/jsref/jsref_atan.asp)  | 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。     |
| [atan2(y,x)](https://www.w3school.com.cn/jsref/jsref_atan2.asp) | 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。 |
| [ceil(x)](https://www.w3school.com.cn/jsref/jsref_ceil.asp)  | 对数进行上舍入。                                             |
| [cos(x)](https://www.w3school.com.cn/jsref/jsref_cos.asp)    | 返回数的余弦。                                               |
| [exp(x)](https://www.w3school.com.cn/jsref/jsref_exp.asp)    | 返回 e 的指数。                                              |
| [floor(x)](https://www.w3school.com.cn/jsref/jsref_floor.asp) | 对数进行下舍入。                                             |
| [log(x)](https://www.w3school.com.cn/jsref/jsref_log.asp)    | 返回数的自然对数（底为e）。                                  |
| [max(x,y)](https://www.w3school.com.cn/jsref/jsref_max.asp)  | 返回 x 和 y 中的最高值。                                     |
| [min(x,y)](https://www.w3school.com.cn/jsref/jsref_min.asp)  | 返回 x 和 y 中的最低值。                                     |
| [pow(x,y)](https://www.w3school.com.cn/jsref/jsref_pow.asp)  | 返回 x 的 y 次幂。                                           |
| [random()](https://www.w3school.com.cn/jsref/jsref_random.asp) | 返回 0 ~ 1 之间的随机数。                                    |
| [round(x)](https://www.w3school.com.cn/jsref/jsref_round.asp) | 把数四舍五入为最接近的整数。                                 |
| [sin(x)](https://www.w3school.com.cn/jsref/jsref_sin.asp)    | 返回数的正弦。                                               |
| [sqrt(x)](https://www.w3school.com.cn/jsref/jsref_sqrt.asp)  | 返回数的平方根。                                             |
| [tan(x)](https://www.w3school.com.cn/jsref/jsref_tan.asp)    | 返回角的正切。                                               |
| [toSource()](https://www.w3school.com.cn/jsref/jsref_tosource_math.asp) | 返回该对象的源代码。                                         |
| [valueOf()](https://www.w3school.com.cn/jsref/jsref_valueof_math.asp) | 返回 Math 对象的原始值。                                     |

#### 4. String 对象方法

| 方法                                                         | 描述                                                 |
| :----------------------------------------------------------- | :--------------------------------------------------- |
| [anchor()](https://www.w3school.com.cn/jsref/jsref_anchor.asp) | 创建 HTML 锚。                                       |
| [big()](https://www.w3school.com.cn/jsref/jsref_big.asp)     | 用大号字体显示字符串。                               |
| [blink()](https://www.w3school.com.cn/jsref/jsref_blink.asp) | 显示闪动字符串。                                     |
| [bold()](https://www.w3school.com.cn/jsref/jsref_bold.asp)   | 使用粗体显示字符串。                                 |
| [charAt()](https://www.w3school.com.cn/jsref/jsref_charAt.asp) | 返回在指定位置的字符。                               |
| [charCodeAt()](https://www.w3school.com.cn/jsref/jsref_charCodeAt.asp) | 返回在指定的位置的字符的 Unicode 编码。              |
| [concat()](https://www.w3school.com.cn/jsref/jsref_concat_string.asp) | 连接字符串。                                         |
| [fixed()](https://www.w3school.com.cn/jsref/jsref_fixed.asp) | 以打字机文本显示字符串。                             |
| [fontcolor()](https://www.w3school.com.cn/jsref/jsref_fontcolor.asp) | 使用指定的颜色来显示字符串。                         |
| [fontsize()](https://www.w3school.com.cn/jsref/jsref_fontsize.asp) | 使用指定的尺寸来显示字符串。                         |
| [fromCharCode()](https://www.w3school.com.cn/jsref/jsref_fromCharCode.asp) | 从字符编码创建一个字符串。                           |
| [indexOf()](https://www.w3school.com.cn/jsref/jsref_indexOf.asp) | 检索字符串。                                         |
| [italics()](https://www.w3school.com.cn/jsref/jsref_italics.asp) | 使用斜体显示字符串。                                 |
| [lastIndexOf()](https://www.w3school.com.cn/jsref/jsref_lastIndexOf.asp) | 从后向前搜索字符串。                                 |
| [link()](https://www.w3school.com.cn/jsref/jsref_link.asp)   | 将字符串显示为链接。                                 |
| [localeCompare()](https://www.w3school.com.cn/jsref/jsref_localeCompare.asp) | 用本地特定的顺序来比较两个字符串。                   |
| [match()](https://www.w3school.com.cn/jsref/jsref_match.asp) | 找到一个或多个正则表达式的匹配。                     |
| [replace()](https://www.w3school.com.cn/jsref/jsref_replace.asp) | 替换与正则表达式匹配的子串。                         |
| [search()](https://www.w3school.com.cn/jsref/jsref_search.asp) | 检索与正则表达式相匹配的值。                         |
| [slice()](https://www.w3school.com.cn/jsref/jsref_slice_string.asp) | 提取字符串的片断，并在新的字符串中返回被提取的部分。 |
| [small()](https://www.w3school.com.cn/jsref/jsref_small.asp) | 使用小字号来显示字符串。                             |
| [split()](https://www.w3school.com.cn/jsref/jsref_split.asp) | 把字符串分割为字符串数组。                           |
| [strike()](https://www.w3school.com.cn/jsref/jsref_strike.asp) | 使用删除线来显示字符串。                             |
| [sub()](https://www.w3school.com.cn/jsref/jsref_sub.asp)     | 把字符串显示为下标。                                 |
| [substr()](https://www.w3school.com.cn/jsref/jsref_substr.asp) | 从起始索引号提取字符串中指定数目的字符。             |
| [substring()](https://www.w3school.com.cn/jsref/jsref_substring.asp) | 提取字符串中两个指定的索引号之间的字符。             |
| [sup()](https://www.w3school.com.cn/jsref/jsref_sup.asp)     | 把字符串显示为上标。                                 |
| [toLocaleLowerCase()](https://www.w3school.com.cn/jsref/jsref_toLocaleLowerCase.asp) | 把字符串转换为小写。                                 |
| [toLocaleUpperCase()](https://www.w3school.com.cn/jsref/jsref_toLocaleUpperCase.asp) | 把字符串转换为大写。                                 |
| [toLowerCase()](https://www.w3school.com.cn/jsref/jsref_toLowerCase.asp) | 把字符串转换为小写。                                 |
| [toUpperCase()](https://www.w3school.com.cn/jsref/jsref_toUpperCase.asp) | 把字符串转换为大写。                                 |
| toSource()                                                   | 代表对象的源代码。                                   |
| [toString()](https://www.w3school.com.cn/jsref/jsref_toString_string.asp) | 返回字符串。                                         |
| [valueOf()](https://www.w3school.com.cn/jsref/jsref_valueOf_string.asp) | 返回某个字符串对象的原始值。                         |

#### 5. Event 时间属性方法

| 属性        | 当以下情况发生时，出现此事件   |
| :---------- | :----------------------------- |
| onabort     | 图像加载被中断                 |
| onblur      | 元素失去焦点                   |
| onchange    | 用户改变域的内容               |
| onclick     | 鼠标点击某个对象               |
| ondblclick  | 鼠标双击某个对象               |
| onerror     | 当加载文档或图像时发生某个错误 |
| onfocus     | 元素获得焦点                   |
| onkeydown   | 某个键盘的键被按下             |
| onkeypress  | 某个键盘的键被按下或按住       |
| onkeyup     | 某个键盘的键被松开             |
| onload      | 某个页面或图像被完成加载       |
| onmousedown | 某个鼠标按键被按下             |
| onmousemove | 鼠标被移动                     |
| onmouseout  | 鼠标从某元素移开               |
| onmouseover | 鼠标被移到某元素之上           |
| onmouseup   | 某个鼠标按键被松开             |
| onreset     | 重置按钮被点击                 |
| onresize    | 窗口或框架被调整尺寸           |
| onselect    | 文本被选定                     |
| onsubmit    | 提交按钮被点击                 |
| onunload    | 用户退出页面                   |
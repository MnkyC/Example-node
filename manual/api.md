# 数学
Math，JS的原生对象，提供数学功能

* Math.PI, 圆周率
* Math.abs(value), 绝对值
* Math.ceil(value), 向上取整
* Math.floor(value), 向下取整
* Math.round(value), 四舍五入，等同于Math.floor(value + 0.5)

		// 主要注意0.5的处理
		Math.round(0.5); // 1
		Math.round(-1.5); // -1
* Math.pow(i, j), i为底数，j为幂的指数，等同于 i ** j
* Math.random(), [0, 1)区间的**伪随机数**

		// 任意范围随机数
		min + Math.random() * (max - min);
		// 任意范围随机整数
		min + Math.floor(Math.random() * (max - min));
		// 任意长度随机字符
		let str = "ABCDEFG...XYZabc...xyz01..789-_...";
		for (let i = 0; i < length; i++) {
			const rand = Math.floor(Math.random() * str.length);
			str = str.slice(rand, rand + 1);
		}
* Math.sin(value),  正弦，value为弧度值
* Math.cos(value), 余弦
* Math.tan(value) , 正切，
* Math.asin(value), 反正弦，返回弧度值
* Math.acos(value), 反余弦
* Math.atan(value), 反正切

# 数值
* Number.isInteger(), ES6, 判断是否为整数，精度要求高的不建议使用，因为超过精度后就会误判

		JavaScript中整数和浮点数都是一样的存储方式，所以10和10.0是同一个值，都是整数

# 字符串
* str.length属性获取长度
* str.indexOf(searchvalue, fromindex), 确定一个字符串在另一个字符串中第一次出现的位置，返回匹配开始的位置，不匹配返回-1

		fromindex可选，表示从该位置开始向后匹配
		'JavaScript'.indexOf('a'); // 1
		'JavaScript'.indexOf('a', 2); // 3
* strs.includes(str, startindex), ES6，确定是否在strs中找到str，startindex可选，表示开始搜索的位置，从startindex到尾部
* strs.startsWith(str, startindex), ES6，str是否在strs头部，startindex可选，表示开始搜索的位置，从startindex到尾部
* strs.endsWith(str, n), ES6，str是否在strs尾部，n可选，针对前n个字符
* str.lastIndexOf(searchvalue, fromindex), 和indexOf类似，不过是从尾部开始匹配

		fromindex可选，表示从该位置开始向前匹配
		'JavaScript'.lastIndexOf('a'); // 3
		'JavaScript'. lastIndexOf('a', 2); // 1
* str.slice(startindex, endindex), 截取并返回子字符串，不改变原字符串，区间[startindex, endindex)

		endindex没有的话，默认是到字符串尾部
		'JavaScript'.slice(0, 4); // "Java"
		'JavaScript'.slice(4); // "Script"
		参数是负数，就从尾部开始倒数计算，负数加上字符串长度
		'JavaScript'.slice(-6); // "Script"
		'JavaScript'.slice(0, -6); // "Java"
		'JavaScript'.slice(-2, -1); // "p"
		startindex > endindex时，返回空字符串
* str.substring(startindex, endindex), 截取并返回子字符串，不改变原字符串，区间[startindex, endindex)

		endindex没有的话，默认是到字符串尾部
		'JavaScript'.substring(0, 4); // "Java"
		'JavaScript'.substring(4); // "Script"
		和slice不同的点:
			tartindex > endindex时，自动交换两个参数的位置
			'JavaScript'. substring(10, 4); // "Script"
			参数是负数，自动将其转为0
			'JavaScript'.substring(-3); // "JavaScript"
			'JavaScript'.substring(4, -3); // "Java"
			
**不建议使用substring，优先使用slice**

* str.substr(startindex, size), 截取并返回子字符串，不改变原字符串，size是子字符串的长度

		size没有的话，默认是到字符串尾部
		'JavaScript'.substr(4, 6); // "Script"
		'JavaScript'.substr(4); // "Script"
		第一个参数是负数，就从尾部开始倒数计算，第二个参数是负数自动转为0，因此返回空字符串
		'JavaScript'.substr(-6); // "Script"
		'JavaScript'.substr(4, -1); // ""
* str.split(delimiter, size), 按照指定规则分隔字符串，返回分割后的子字符串组成的数组，参数都可选

		'a|b|c'.split('|'); // ["a", "b", "c"]
		'a|b|c'.split(''); // ["a", "|", "b", "|", "c"]
		'a|b|c'.split(); // ["a|b|c"]
		'a||c'.split('|'); // ["a", "", "c"]
		'|b|c'.split('|'); // ["", "b", "c"]
		'a|b|'.split('|'); // ["a", "b", ""]
		size限定返回数组的最大成员数
		'a|b|c'.split('|', 0); // []
		'a|b|c'.split('|', 1); // ["a"]
		'a|b|c'.split('|', 4); // ["a", "b", "c"]
* str.concat(), 连接字符串，返回一个新字符串，不改变原字符串

		s1.concat(s2, s3, ..., sn)
		与加法运算符的区别是，都会将参数转为字符串再连接
		而加法运算时当前两个运算子都是数值时，不会转换类型，而是进行数学计算(1 + 2 + ‘3’; // 33)
* str.toUpperCase()/toLowerCase(), 转大写/转小写，返回新字符串，不改变原字符串

		'JavaScript'.toUpperCase();
		'JavaScript'.toLowerCase();
	
* str.trim(), 去掉两端的空格，返回新字符串，不改变原字符串

		' JavaScript \t'.trim(); // "JavaScript"
* str.repeat(n), ES6, 返回新字符串，表示将原字符串重复n次

		n是浮点数就取整
		负数或者Infinity就报错
		-1到0间的小数除外，因为会先向下取整，(-1, 0)取整后是0
		NaN等同于0，不能转为数字的字符串也等同于0
		'x'.repeat(0); // ""
		'x'.repeat('cc'); // ""
		'x'.repeat(NaN); // ""

# 数组
*  length属性获取元素数量
* Array.isArray(arr), 静态方法，判断是否为数组
* arr.valueOf(), 返回数组本身
* arr.toString(), 数组的字符串形式

		let arr = [1, 2, 3];
		arr.toString(); // "1, 2, 3"
		let arr = [1, 2, 3, [4, 5]];
		arr.toString(); // "1, 2, 3, 4, 5"
* arr.push(...), 尾部添加一个或多个元素并返回新的数组长度，改变原数组，可以用扩展运算符...，直接添加一个数组

		arr.push(1);
		arr.push('2', true, {}); // [1, '2', true, {}]
		arr.push(...[3, 4]); // [1, '2', true, {}, 3, 4]
* arr.pop(), 删除最后一个元素并返回该元素，改变原数组

		[].pop(); // 返回undefined, 不会报错
* arr.unshift(...), 头部添加一个或多个元素并返回新的数组长度，改变原数组

		let arr = [1, 2, 3];
		arr.unshift(4, 5); // [4, 5, 1, 2, 3]
* arr.shift(), 删除第一个元素并返回该元素，改变原数组
* arr.join(', '), 将数组按照指定的分隔符拼接成字符串返回，默认逗号

		数组中有undefined或null或空位，会转成空字符串
		[undefined, null].join('#'); // "#"
		['a', , 'b'].join('-'); // "a--b"
* arr.concat(...), 合并多个数组，返回新数组，不改变原数组

		['Java'].concat(['Script']); // ["Java", "Script"]
		['Java'].concat(['Script'], ['!']); // ["Java", "Script", "!"]
		除了数组，也可以合并其他类型的值
		[].concat({a: 1}, {b: 2}); // [{a: 1}, {b: 2}]
		[1].concat(2, 3); // [1, 2, 3]
		参数都省略就是返回原数组的拷贝，不影响原数组
		[1, 2, 3].concat(); // [1, 2, 3]
* arr.reverse(), 颠倒排序，返回改变后的数组，改变原数组
* arr.slice(startindex, endindex), 截取并返回数组的一部分，不改变原数组，区间[startindex, endindex)

		省略endindex或者超过数组长度就是截取到数组尾部
		let arr = [1, 2, 3];
		arr.slice(0); // [1, 2, 3]
		arr.slice(2, 6); // [3]
		参数都省略就是返回原数组的拷贝，不影响原数组
		arr.slice(); // [1, 2, 3]
		参数是负数，就从尾部开始倒数计算
		arr.slice(-2); // [2, 3]
		arr.slice(-2, -1); // 2
		startindex > endindex或者startindex > 数组长度, 返回空数组
* arr.splice(startindex, size, item1, item2, ...), 删除数组的一部分，可以在删除的位置添加新的元素，返回被删除的元素，改变原数组

		let arr = ['a', 'b', 'c', 'd'];
		size，被删除的元素个数
		arr.splice(2, 2); //  ['c', 'd']
		arr // ['a', 'b']
		size后面是要添加的元素
		arr.splice(2, 2, 1, 2); // ['c' , 'd']
		arr // ['a', 'b', 1, 2]
		startindex是负数，就从尾部倒数位置开始删除
		arr.splice(-2, 2); // ['a', 'b']
		size=0表示单纯插入
		arr.splice(1, 0, 2); // []
		arr // ['a', 2, 'b', 'c', 'd']
		只有startindex一个参数，就是分割数组
		arr.splice(2); // ['c', 'd']
		arr / ['a', 'b']
* arr.sort() 可以自定义排序函数，内置默认的是按照字典顺序升序，改变原数组

		不按大小而是按照字典顺序排序，数值会先转为字符串
		[11, 101].sort(); // [101, 11]
		[10111, 1101, 111].sort(); // [10111, 1101, 111]
		自定义排序，传入一个函数
		[10111, 1101, 111].sort(functin (a, b) { return a - b; }); // [111, 1101, 10111]
* arr.map(function, arr), 将数组所有元素依次传入参数函数，每次结果组成新数组返回，不改变原数组

		let arr = [1, 2, 3];
		arr.map(fucntion (item) { return item + 1; }); // [2, 3, 4]
		第二个参数指向回调函数内部的this
		let arr = ['a', 'b', 'c'];
		[1, 2].map(fucntion (item) { return this[item]; }, arr); // ["b","c"]
		参数函数可以接受三个参数，当前元素，当前索引和整个数组
		对于数组中的空位，map中的函数会跳过，不跳过undefined和null
		[1, , 2].map(function (item) { return 'a';}) // ["a", , "a"]
* arr.forEach(function (value) {}), 不返回值，只用来操作数据，将数组所有元素依次执行参数函数，无法中断执行

	**注意！若要操作第二个参数，必须用fucntion形式，不能用箭头函数**

		arr.forEach(element => { console.log(element + 2)});
		第二个参数指向回调函数内部的this
		let arr = [];
		[1, 2].forEach(fucntion (item) { this.push(item * item); }, arr); // [1, 2]
		参数函数可以接受三个参数，当前元素，当前索引和整个数组
		对于数组中的空位，forEach的函数也会跳过，不跳过undefined和null
* arr.filter(function), 过滤数组成员，满足条件的成员组成新数组返回，不改变原数组

		所有元素都执行参数函数，结果为true才返回
		[1, 2, 3, 4].filter(element => { return element > 3; });// [4]
		[0, 1, 'a', false].filter(Boolean); // [1, 'a']
		第二个参数指向回调函数内部的this
		参数函数可以接受三个参数，当前元素，当前索引和整个数组
		arr.filter(function (element, index, arr) {});
* arr.indexOf(item, startindex), 返回元素在数组中第一次出现的位置，没有则返回-1

		startindex 可选，默认是开始位置
		不能用于搜索NaN
		底层用严格相等运算符===进行比较
* arr.lastIndexOf(), 返回元素在数组中最后一次出现的位置，没有则返回-1

		不能用于搜索NaN
		底层用严格相等运算符===进行比较

## ES6数组扩展
* Array.from(obj), 将类似数组的对象和可遍历对象(如ES6新增的数据结构Set和Map)转为真正的数组
* arr.keys(), 对键名的遍历
* arr.values(), 对键值的遍历
* arr.entries(), 对键值对的遍历
* arr.includes(item, startindex), 返回布尔值，数组是否包含给定的元素

		startindex可选，表示开始搜索的位置
		startindex为负数表示倒数的位置，大于数组长度就从0开始

# JSON
## 规定
**JSON对值的类型和格式有严格规定**

1. 复合类型的值只能是数组或对象
2. 原始类型的值只有四种(字符串，十进制的数值，布尔值，null)，不能使用NaN, Infinity, -Infinity和undefined
3. 字符串必须用双引号表示，单引号不行
4. 对象的键名必须在双引号中
5. 数组或对象最后一个成员后不能加逗号
6. 空数组和空对象是合法的JSON值

## API
* JSON.stringify(obj, arr或function), 转JSON字符串

	对象属性是undefined，函数或xml对象，会被过滤
	数组属性是undefined，函数或xml对象，会转为null
	对象中的属性若定义了enumerable: false，会被忽略

		第二个参数可选，是指定需要转成JSON字符串的对象属性，类似白名单，数组形式传入，只对对象属性有效，数组无效
		let obj = {"p1": "1", "p2": "2", "p3": "3"};
		let keys = ['p1', "p2"];
		JSON.stringify(obj, keys); // "{"p1": "1", "p2": "2"}"
		第二个参数也可以是函数，可以更改stringify的返回值
		function func(key, value) { if (typeof value == "number") { value += 10; } return value; }
		JSON.stringify({a: 1, b: 2}, func); // {"a": 11, "b": 12}
		若参数对象有自定义的toJSON方法，就是用该函数的返回值作为参数
* JSON.parse(string, function), JSON字符串转对象

		JSON.parse('null'/'{}'/'true'/'"foo"'); // null {} true "foo"
		JSON.parse('[1, 5, "foo"]'); // [1 ,5, "foo"]
		let o = JSON.parse('{"name": "foo"}');
		o.name; // foo
		字符串是不合法的JSON格式，会报错
		JSON.parse("'string'"); // 报错
		为了防止报错，可以写在try...catch中
		try { JSON.parse(); } catch(e) { }
		第二个参数是参数函数
		function func(key, value) { if (key == "a") { return value + 10; } return value; }
		JSON.parse('{"a": 1, "b": 2}', func); // {a: 11, b: 12}

	
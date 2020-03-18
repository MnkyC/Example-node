# 字符串
* length属性获取长度
* indexOf(searchvalue, fromindex), 确定一个字符串在另一个字符串中第一次出现的位置，返回匹配开始的位置，不匹配返回-1

		fromindex可选，表示从该位置开始向后匹配
		'JavaScript'.indexOf('a'); // 1
		'JavaScript'.indexOf('a', 2); // 3
* lastIndexOf(searchvalue, fromindex), 和indexOf类似，不过是从尾部开始匹配

		fromindex可选，表示从该位置开始向前匹配
		'JavaScript'.lastIndexOf('a'); // 3
		'JavaScript'. lastIndexOf('a', 2); // 1
* slice(startindex, endindex), 截取并返回子字符串，不改变原字符串，区间[startindex, endindex)

		endindex没有的话，默认是到字符串尾部
		'JavaScript'.slice(0, 4); // "Java"
		'JavaScript'.slice(4); // "Script"
		参数是负数，就从尾部开始倒数计算，负数加上字符串长度
		'JavaScript'.slice(-6); // "Script"
		'JavaScript'.slice(0, -6); // "Java"
		'JavaScript'.slice(-2, -1); // "p"
		startindex > endindex时，返回空字符串
* substring(startindex, endindex), 截取并返回子字符串，不改变原字符串，区间[startindex, endindex)

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

* substr(startindex, size), 截取并返回子字符串，不改变原字符串，size是子字符串的长度

		size没有的话，默认是到字符串尾部
		'JavaScript'.substr(4, 6); // "Script"
		'JavaScript'.substr(4); // "Script"
		第一个参数是负数，就从尾部开始倒数计算，第二个参数是负数自动转为0，因此返回空字符串
		'JavaScript'.substr(-6); // "Script"
		'JavaScript'.substr(4, -1); // ""
* split(delimiter, size), 按照指定规则分隔字符串，返回分割后的子字符串组成的数组，参数都可选

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
* concat(), 连接字符串，返回一个新字符串，不改变原字符串

		s1.concat(s2, s3, ..., sn)
		与加法运算符的区别是，都会将参数转为字符串再连接
		而加法运算时当前两个运算子都是数值时，不会转换类型，而是进行数学计算(1 + 2 + ‘3’; // 33)
* toUpperCase()/toLowerCase(), 转大写/转小写，返回新字符串，不改变原字符串

		'JavaScript'.toUpperCase();
		'JavaScript'.toLowerCase();
	
* trim(), 去掉两端的空格，返回新字符串，不改变原字符串

		' JavaScript \t'.trim(); // "JavaScript"
# 数组
*  length属性获取元素数量
* Array.isArray(arr), 静态方法，判断是否为数组
* arr.valueOf(), 返回数组本身
* arr.toString(), 数组的字符串形式

		let arr = [1, 2, 3];
		arr.toString(); // "1, 2, 3"
		let arr = [1, 2, 3, [4, 5]];
		arr.toString(); // "1, 2, 3, 4, 5"
* arr.push(...), 尾部添加一个或多个元素并返回新的数组长度，改变原数组

		arr.push(1);
		arr.push('2', true, {}); // [1, '2', true, {}]
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
* arr.reverse(), 颠倒排序，返回改变后的数组，改变原数组
* arr.slice(startindex, endindex), 截取并返回数组的一部分，不改变原数组，区间[startindex, endindex)

		省略endindex或者超过数组长度就是截取到数组尾部
		let arr = [1, 2, 3];
		arr.slice(0); // [1, 2, 3]
		arr.slice(2, 6); // [3]
		参数都省略就是返回原数组的拷贝
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
* arr.map(), 将数组所有元素依次传入参数函数，每次结果组成新数组返回，不改变原数组

		let arr = [1, 2, 3];
		arr.map(fucntion (item) { return item + 1; }); // [2, 3, 4]
* arr.forEach(function (value) {}), 不返回值，只用来操作数据，将数组所有元素依次执行参数函数

		arr.forEach(element => { console.log(element + 2)});

# JSON
* JSON.parse(), JSON字符串转对象

	
* JSON.stringify(), 对象转JSON字符串
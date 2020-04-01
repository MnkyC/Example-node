# 遍历
## 对象
ES6新增，返回数组

	Object.keys(obj).forEach(key => {});
	Object.values(obj).forEach(value => {});
	Object.entries(obj).forEach((key, value) => {});
	
**注意！！！Object.keys不保证属性的顺序**

	首先遍历所有数值键，按照升序排列
	其次遍历所有字符串键，按照加入时间升序排列
	最后遍历所有Symbol键，按照加入时间升序排列
	
**建议！用数组存储Object.keys中的属性，然后用自定义的排序算法对数组进行sort，最后遍历数组来获取对应的对象属性进行处理**
## 数组
forEach，缺点: 不能中断

	arr.forEach(element => {});
	arr.forEach((element, index) => {})
	arr.forEach((element, index, arr) => {})
ES6新增

	arr.keys(), 键名遍历
		for (let index of arr.keys())
	arr.values(), 键值遍历
		for (let item of arr.values())
	arr.entries(), 键值对遍历
		for (let [index, item] of arr.entries())
## 字符串
for...of

	for (let str of strs) {}
# 存在
## 数组
## 字符串
	strs.indexOf(str); // 不建议使用，1.不够语义化，要和-1比较 2.内部用===比较，导致误判NaN
	strs.includes(str); // ES6, 推荐使用，没有indexOf的问题
	strs.startsWith(str); // ES6
	strs.endsWith(str); // ES6
# 拷贝
## 对象
深拷贝，返回新对象，不影响原对象

	const obj1 = Object.assign(
		Object.create(Object.getPrototypeOf(obj)),
		obj
	);
## 数组
深拷贝，返回新数组，不影响原数组

	arr.concat();
	arr.slice();
	arr1 = [...arr]; // 利用扩展运算符
# 获取
## 数组
最后一位，arr.slice(-1);
# 去重
## 数组
1. Array.from(new Set(arr)); // ES6, 不能去掉[]和{}
2. for循环嵌套，双指针思想，不能去掉NaN和{}，0, true, null和[]直接消失

		const length = arr.length;
		for (let i = 0; i < length; i++) {
			for (let j = i + 1; j < length; j++) {
				if (arr[i] == arr[j]) {
					arr.splice(j, 1);
					j--;
				}
			}
		}
3. indexOf，建一个空数组，遍历判断空数组是否存在对应元素，不存在就push，不能去掉NaN, []和{}
4. sort，先排序，再建一个数组，放入第一个元素，遍历相邻两个数值，两者不同就push，不能去掉NaN, []和{}
5. includes，建一个空数组，遍历判断空数组是否存在对应元素，不存在就push，不能去掉[]和{}
6. filter加indeOf, 元素在原始数组中第一次出现的索引是否等于当前索引值，不能去掉[]和{}，NaN直接消失

		return arr.filter(function(item, index, arr) {
    			return arr.indexOf(item, 0) === index;
    		});	 
7. 对象的hasOwnProperty加数组的filter，完美去重

		var obj = {};
		return arr.filter(function(item, index, arr) {
    			return obj.hasOwnProperty(typeof item + item) ? false : (				obj[typeof item + item] = true)
		})

# 合并
## 数组
返回新数组，当元素是原始类型时不影响原数组，若是复合类型(如对象)，就会影响原数组

	arr.concat(arr1, arr2);
	[...arr, ...arr1, ...arr2]; // 利用扩展运算符

# 注意点
## 数组
1. length属性，不过滤空位，用delete命令删除了元素后length的值还是不变，并且还可以读取元素(undefined)
2. 数组中元素是空位，和元素是undefined是不同的。空位，用forEach, for...in, Object.keys进行遍历，都会被跳过；undefined，不会跳过
3. **数组sort方法默认不是升序的，需要自己写排序算法**

		arr.sort((a, b) => { return a - b; })

# 转换
自动转换具有不确定性，不易排错，建议预期为布尔，数值，字符串时，全部使用显示转换（Boolean(), Number(), String()）
# 运算
## 位运算的应用
二进制否运算取整是所有方法中最快的

	~~ a;
异或运算是交换两个变量的值最快的方法，同时也能取整

	a ^= b;
	b ^= a;
	a ^= b;

	a ^ 0; // 取整数部分，小数直接舍去
开关，如声音，禁言，权限等

	某对象有4个属性，对应一个变量，那么可设计一个四位的二进制数
	let FLAG_A = 1; // 0001
	let FLAG_B = 2; // 0010
	let FLAG_C = 4; // 0100
	let FLAG_D = 8; // 1000
	每个属性占一个二进制位，之后就能进行二进制与运算&进行校验
	let flag = 5; // 0101
	if (flag & FLAG_A) {} // 0101 & 0001 => 0001 => true
	
	若需要打开a, b, c三个开关，可以构造一个掩码
		let mask = FLAG_A | FLAG_B | FLAG_C; // 0111
	或运算可以确保打开指定的开关
		flag = flag | mask;
	与运算可以设置当前设置中凡是与开关设置不同的全部关闭
		flag = flag & mask;
	异或运算可以切换当前设置，第一次执行得到当前设置的相反设置，再次就得到原来的设置
		flag = flag ^ mask;
	否运算可以翻转当前设置
		flag = ~flag;
	
# 数据结构
## 数组
1. push和pop结合，构成“后进先出”的栈结构
2. push和shift结合，否成“先进先出”的队列结构

# 技巧
1. 自定义数组排序方法，用a - b的形式，而不是a > b这种布尔形式
2. 查看负数在计算机内部的存储形式，最快的方式，-1 >>> 0
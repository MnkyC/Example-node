# 遍历
## 对象
Object.keys(obj).forEach(o => {});
## 数组
arr.forEach(element => {});
arr.forEach((element, index) => {})
arr.forEach((element, index, arr) => {})
## 字符串
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
**This**

this可以访问正在处理的对象，但是会随着执行环境的变化而变化

	两种方法帮助理解this的值
		1.每个函数体开始的地方加入console.log(this);，确保了解当前运行环境下正在处理的对象
		2.var obj = this; 将this赋值给一个变量，这样就可以安全地使用obj来指代最初的对象，不用担心后面this变化

	var obj = {
		foo: function () {
	    	console.log(this)
	  	}
	}

	var bar = obj.foo
	obj.foo() // 打印出的 this 是 obj
	bar() // 打印出的 this 是 window

	ES5中三种函数调用
		func(a, b);
		obj.child.method(a, b);
		func.call(context, a, b);
		前两种都是语法糖，第三种才是正常的调用方式
		第一种转换下：func.call(undefined, a, b);
		第二种转换下：obj.child.method(obj.child, a, b);

function func() {
	console.log(this);
}
func();

	转换下就是func.call(undefined)
**浏览器有条规则：传的context是null或undefined，window就是默认的context，严格模式下还是undefined**

obj.child.method(a, b);

		function f() { console.log(this); }
		var arr = [f, f2];
		arr[0]();
		可以将arr[0]()想成arr.0()，当然语法是错的，但可以和三种形式对比下，得到是第二种类型，所以是arr.0.call(arr)

	this其实就是你调用函数时传入的第一个参数context，不是call形式就先转为call形式，一下就看出来了
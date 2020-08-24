+ 1、常见的内置错误
	+ ReferenceError: 引用的变量错误
	例如使用：console.log(a);//ReferenceError: a is not defined
	
	+ TypeError: 数据类型不正确的错误
	let a;
	console.log(b.xxx)//TypeError: Cannot read property 'xxx' of undefined
	
	+ RangeError: 数据值不在其所允许的范围内
	function fn(){ fn() }
	fn()//RangeError: Maximum call stack size exceeded
	
	+ SysntaxError: 语法错误
	const c=""""//SysntaxError: Unexpected string
	
+ 2、错误处理
	+ 捕获错误： try...catch（捕获系统的错误）
	try{
        let a;
        console.log(b.xxx)
	}catch(error){
		//error.message/error.stack(显示错误位置)
		console.log(error)
	}
	//在浏览器的f12的source打断点刷新测试就可以看见
	
	+ 抛出错误： throw error(主动抛出--让下一级处理)
	//抛出错误
	function something(){
		if(Date.now()%2===1){
			console.log("当前时间为奇数，可以执行任务")
		}else{//如果时间是偶数抛出异常，由调用者来处理
			throw new Error('当前时间为偶数无法执行任务')
		}
	}
	//捕获处理异常
	try{
		somethig()
	}catch(error){
		alert(error.message)
	}

+ 3、promise的理解和使用
	+ 是什么？
		+ Promise是JS中进行异步编程的新的解决方案（回调地狱			  问题）
		+ 从语法上说promise是一个构造函数（实例可以做什么）
		+ 从功能上说Promise对象用来封装一个异步操作并获取其			最终执行的结果
		
	+ promise的状态改变
		+ pending 变成 resolved
		+ pending 变成 rejected
		+ 说明：一个promise对象只能改变一次，无论成功失败都			一个返回结果，成功返回结果一般为value，失败返回			  reason
		
	+ Promise的基本使用
		const p = new Promise((resolve,reject)=>{
			resolve(‘可以返回任何类型’)
			//reject(‘可以返回任何类型’)
		})
		p.then(value=>{ 接收得到成功的数据--触发promise的  onResolved回调 },reason=>{ 接收得到失败的数据 --触发promise的onRejected回调})
		
	+ 为什么使用promise
		+ 支持链式调用，解决回调地狱问题，回调地狱就是回调函数	      的嵌套调用，即下一个回调函数会以上一层回调函数的返回	      结果为前提，会造成不便于阅读和异常处理需要每个分开		      处理的问题----但是promise不是最优的解决回调地狱方           案，因为还需要写回调函数，最优的是async/await
		+ 可以灵活指定回调函数的时机，以前只能在请求发送前指定		  对应的回调函数，现在可以在请求后再指定回调函数，同样		  也会获得对应的返回结果
	
	
	+ 改变promise的状态
		+ resolve
		+ reject
		+ throw new Error('出错了')/throw 3---promise           状态为reject，返回的数据为error对象/返回3
		
	+ .then的参数如果上一个promise没有返回值，则该参数为undefined,例如：（12集重点）
	
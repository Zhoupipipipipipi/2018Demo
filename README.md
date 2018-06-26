# 2018Demo
### day1 
##### 写一个函数execTime, 参数：时间毫秒数，作用：什么都不做，但函数执行会耗时参数传递的毫秒数 
##### 总结：看到题目第一反应是为了让你误以为用setTimeout，但是settimeout是异步，这里是要3秒后才输出2，所以要采用同步方法。刚开始没有想到用while，百度了sleep看到while就知道了。获取毫秒数getTime()  
  
### day2 
##### 写一个函数execTime，参数t：时间毫秒数，参数callback：回调函数  
##### 总结：异步，settimeout  

### day3 
##### 用JS写出一个对象obj，使得obj.obj.obj.obj===obj 也就是说，不管出现多少次.obj, 都得到obj
##### 总结：可以用堆内存去思考，因为obj是个对象，指向堆内存，这时obj.obj=obj也是上面那个对象，同一个堆内存，形成一个循环  

### day4 
##### 写出一个函数fn，使得fn满足以下条件 1. fn() === fn 2. fn.fn === fn 
##### 总结：本来用es6写法写了，然后看到别人用了arguments.callee可以代替fn，arguments.callee指向拥有这个 arguments 对象的函。结果用arguments在es6中写的时候报错。
##### 原因：箭头函数有作用域（词法作用域），词法作用域简单来讲就是，一切变量（包括this）都根据作用域链来查找。箭头函数中的this因为绑定了词法作用域，所以始终指向自身外的第一个this（由于自身没有声明this，所以会去作用域上找this）,也就是始终等于调用它的函数this。严格模式下不允许使用arguments（规定），并且，普通函数中arguments代表了调用时传入的参数，但是箭头函数不是，箭头函数会把arguments当作一个普通的变量，顺着作用域链由内而外地查询。

### day5 
##### 写出一个函数fn,使得fn满足以下条件：1. fn()打印出‘a’ 2.fn()()打印出'b' 3.fn()()()打印出c 
##### 总结：刚刚开始完全不知道如何入手，看了别人写的才知道，改变chr的值，用setTimeout()延迟打印   

### day6 
##### 写出一个函数fn, 使得fn满足一下条件 fn()=='a' fn()()=='b' fn()()()=='c'
##### 总结：每一个引用类型的对象中都有相对应的valueOf方法，自带或者继承自父类，valueOf返回当前对象的原始值

### day7 
##### 小明成绩不好，每次考试都靠瞎猜。小明的老师对他说：小明，如果考不到60分你继续考，直到考到六十分，我实现你的愿望让你和凯莉做到一起将下述代码用promise改写
##### 总结：promise 一直在异步，回调。Promise的优势在于，可以在then方法中继续写Promise对象并返回，然后继续调用then来进行回调操作。reject用法：调用reject并传递一个参数，作为失败的原因。有个问题是settimeout没有成功  

### day8 
##### 写一个byField函数，实现数组按名字、年纪、任意字段排序   
##### 总结：利用sort函数可以传入自定义的函数来排序，返回ture或false进行排序。sort方法的参数必须是一个函数，该函数返回排序规则。直接打印结果的时候发现三个排序都一样，是因为对象指向同一个内存地址，所以显示的都是最后一个的排序 

### day10 
##### 总结：一定要去看promise   

### day11 
##### 写一个函数execTimes, 用于测试一个函数执行一定次数的时长.如：execTimes(sort, 1000)('hello')表示：执行sort函数1000次，sort的参数是'hello'
##### 总结：很久没有搞每日一练了，因为最近一直在加班。今天这题的点在函数内再执行一个函数，‘hello’作为第二个参数传给函数内的函数，用到了console.time()和console.timeEnd(),可以用来计算函数执行多少时间  

### day12 
##### 请使用Javascript实现一个方法，该方法能够判断两个字符串是否匹配.使用上一关的execTimes方法测试你的方案执行10000次的时长，该方案是否是最优方案？如果不是请给出优化方法，并说明时间复杂度，尽量使用ES6的语法。
##### 总结：用了三种方法解决这个问题，第一种是先转为数组split('')，排序sort()，再转为字符串join('')。第二种方法是通过替换str2中的字符，如果结果str2为空，则返回!''即为true，否则返回!'xx'即为false。第三种是用哈希表存键值的方法判断，先存，然后去判断键值，减去。这三种方法中，第二种方法最快了。打印太多东西也没耗时间。散列表（Hash table，也叫哈希表），是根据关键码值(Key value)而直接进行访问的数据结构。

### day17
##### 总结：day16-17考察的是同一个知识点异步macrotask和microtask。从上面代码可以看出，Promise的函数代码的异步任务会优先于setTimeout的延时为0的任务先执行，原因是因为任务队列会分为microtask和macrotask，而promise中的then方法的函数会被推入到microtasks队列中，而setTimeout函数会被推入到macrotasks。任务队列中，在每一次事件循环中，macrotask只会提取一个执行，而microtask会一直提取，直到microsoft队列为空为止。执行优先级的问题 microtasks > macrotasks。macrotasks: script(整体代码),setTimeout, setInterval, setImmediate, I/O, UI rendering  //////microtasks: process.nextTick, Promises, Object.observe, MutationObserver

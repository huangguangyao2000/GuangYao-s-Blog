# 命令模式

举例：订餐时的订单

### 用途

有时需向某些对象发送请求，但是并不知道请求的接收者是谁，也不知道被请求的操作是什么。此时希望用一种松耦合的方式来设计陈旭，使得请求发送者和请求接受者能够消除彼此之间的耦合关系。

相对于过程化的请求调用，command对象有更长的生命周期。请求已被封装在command对象的方法中，成了对象的行为。需要调用时才调用。

面向对象实现方法

```text
<body>
	<button id="btn1">按钮一</button>
	<button id="btn2">按钮二</button>
	<button id="btn3">按钮三</button>
</body>
<script type="text/javascript">
	//负责绘图的同志负责的代码
	var button1 = document.getElementById('btn1');
	var button2 = document.getElementById('btn2');
	var button3 = document.agetElementById('btn3');

	var setCommand = function(button,command){
		button.onclick = function(){
			command.execute();
		}
	}
	
	//负责点击后具体回调函数同志的代码
	var MenuBar = {
		refresh:function(){
			console.log('刷新菜单目录')
		}
	};
	var SubMenu = {
		add:function(){
			console.log('增加子菜单')
		},
		del:function(){
			console.log('删除子菜单')
		}
	}
	//将行为封装在命令类中
	var RefreshMenuBarCommand = function(receiver){
		this.receiver = receiver;
	}
	RefreshMenuBarCommand.prototype.execute = function(){
		this.receiver.refresh()
	}
	var AddSubMenuCommand = function(receiver){
		this.receiver = receiver;
	}
	AddSubMenuCommand.prototype.execute = function(){
		this.receiver.add();
	}
	var DelSubMenuCommand = function(receiver){
		this.receiver = receiver;
	}
	DelSubMenuCommand.prototype.execute = function(){
		console.log('删除子菜单')
	}

	//将命令接收者传入到command对象中，并且把command对象安装到button上
	var refreshMenuBarCommand = new RefreshMenuBarCommand(MenuBar);

	var addSubMenuCommand = new AddSubMenuCommand(SubMenu);

	var delSubMenuCommand = new DelSubMenuCommand(SubMenu);

	setCommand(button1,refreshMenuBarCommand);
	setCommand(button2,addSubMenuCommand);
	setCommand(button3,delSubMenuCommand); 
</script>
```

对象及函数方式

```text
<body>
	<button id="btn1">按钮一</button>
	<button id="btn2">按钮二</button>
	<button id="btn3">按钮三</button>
</body>
<script type="text/javascript">
	//负责绘图的同志负责的代码
	var button1 = document.getElementById('btn1');
	var button2 = document.getElementById('btn2');
	var button3 = document.getElementById('btn3');

	var bindClick = function(button,func){
		button.onclick = func;
	}

	var MenuBar = {
		refresh:function(){
			console.log('刷新')
		}
	}
	var SubMenu = {
		add:function(){
			console.log('添加子菜单')
		},
		del:function(){
			console.log('删除子菜单')
		}
	}

	bindClick(button1,MenuBar.refresh);
	bindClick(button2,SubMenu.add);
	bindClick(button3,SubMenu.del);
</script>

```

闭包实现

```text
<body>
	<button id="btn1">按钮一</button>
	<button id="btn2">按钮二</button>
	<button id="btn3">按钮三</button>
</body>
<script type="text/javascript">
	//负责绘图的同志负责的代码
	var button1 = document.getElementById('btn1');
	var button2 = document.getElementById('btn2');
	var button3 = document.getElementById('btn3');

	var setCommand = function(button,func){
		button.onclick = function(){
			func();
		}
	};

	var MenuBar = {
		refresh:function(){
			console.log('刷新')
		}
	}
	var SubMenu = {
		add:function(){
			console.log('添加子菜单')
		},
		del:function(){
			console.log('删除子菜单')
		}
	}

	var RefreshMenuBarCommand = function(receiver){
		return function(){
			receiver.refresh();
		}
	}

	var refreshMenuBarCommand = RefreshMenuBarCommand(MenuBar);
	setCommand(button1,refreshMenuBarCommand);
</script>
```

### 撤销和重做

```text
<!DOCTYPE html>
<html>
<head>
	<title>播放录像</title>
</head>
<body>
	<button id="replay">播放录像</button>
</body>
<script type="text/javascript">
	var Ryu = {
		attack:function(){
			console.log('攻击')
		},
		defense:function(){
			console.log('防御')
		},
		jump:function(){
			console.log('跳跃')
		},
		crouch:function(){
			console.log('蹲下')
		}
	};
	var makeCommand = function(receiver,state){
		return function(){
			receiver[state]();
		}
	}

	var commands = {
		'119':'jump',
		'115':'crouch',
		'97':'defense',
		'100':'attack'
	};
	var commandStack = [];
	document.onkeypress = function(ev){
		var keyCode = ev.keyCode,
			command = makeCommand(Ryu,commands[keyCode]);
		if(command){
			command();
			commandStack.push(command);
		}
	}
	document.getElementById('replay').onclick = function(){
		var command;
		while(command = commandStack.shift()){
			command();
		}
	}
</script>
</html>
```


# JS-表单脚本

## 基础知识

HTML中表单为`<form>`，在JS中为HTMLFormElement类型，下面为其独有属性和方法

* name
* method
* reset\(\)
* submit\(\)
* target

  可通过document.forms取得页面中所有表单。

  **主要：**

* 形式：表单如何在页面中用HTML语言生成
* 属性及方法
* 操作
* 事件触发

### 提交表单

1. 提交按钮——将type设为submit
2. 自定义提交按钮——button
3. 图像按钮——type设为image

   ```markup
   <input type='submit' value='Submit Form'>
   <button type='submit'>Submit Form</button>
   <input type='image' src='graphic.gif'>
   ```

   只要表单存在上面所示按钮，在相应表单控件**具有焦点**的情况下**回车键**也可提交该表单。

   ```javascript
   //阻止表单提交
   var form = document.getElementById("myForm");
   EventUtil.addHandler(form,"submit",function(event){
    event = EventUtil.getEvent(event);
    EventUtil.preventDefault(event);
   })
   ```

   最大问题是**重复提交表单**。解决方法有两个：

4. 第一次提交表单后就**禁用提交**按钮
5. 利用onsubmit事件处理程序**取消后续的表单提交操作**。

### 重置表单

```markup
<input type='reset' value='Reset Form'>
<button type='reset'>Reset Form</button>
```

重置表单后，所有表单字段都会恢复到**页面刚加载完毕时的初始值**。

单击重置表单时，会**触发reset事件**。

### 表单字段

可使用原生DOM方法访问表单元素。表单均有elements属性，该属性为表单中所有表单元素的集合，是一个有序列表，包含了表单中所有字段。可按照位置和name特性来访问。

#### 1.共有的表单字段属性

共有属性：disabled,name,type,tabIndex,value

#### 2. 共有的表单字段方法

1. focus\(\)

   ```javascript
   EventUtil.addHandler(window,"load",function(event){
    document.forms[0].elements[0].focus();
   })
   ```

   若所指向的`<input>`元素其type特性值为`hidden`

   或CSS的display或visibility属性隐藏了该字段了。

HTML5表单新增`autofocus`属性，只要设置了属性，不用JavaScript就能**自动把焦点移动到相应字段**。

```markup
<input type='text' autofocus>
```

1. blur\(\)

   作用为从元素中移走焦点

   `document.forms[0].elements[0].blur()`

**共用的表单字段事件**

1. blur
2. change
3. focus

**文本框脚本**

1. `<input>`

示例：

```markup
<input type='text' size='25' maxlength='50' value='initial value'>
```

1. `<textarea>`

始终会呈现为一个多行文本框。文本框大小可通过rows和cols特性指定。

示例：

```markup
<textarea rows='25' cols='5'>initial value</textarea>
```

### 选择文本

当文本框获得焦点时，选择文本框所有内容

```javascript
EventUtil.addHandler(textbox,'focus',function(event){
    event=EventUtil.getEvent(event);
    var target=EventUtil.getTarget(event);
    target.select();
})
```

### 过滤输入

#### 屏蔽字符

例：阻止向文本框中插入某种字符

```javascript
EventUtil.addHandler(textbox,'keypress',function(event){
    event=EventUtil.getEvent(event);
    EventUtil.preventDefault(event);
})
```

#### 操作剪贴板

* beforecopy
* cut
* paste

**自动切换焦点**

```javascript
(function(){
  function tabForward(event){
      event = EventUtils.getEvent(event);
      var target = EventUtil.getTarget(event);

      if(target.value.length == target.maxLength){
          var form = target.form;

          for(var i =0,len=form.elements.length;i<len;i++){
              if(form.elements[i]==target){
                  if(form.elements[i+1]){
                      form.elements[i+1].focus();
                  }
                  return;
              }
          }
      }
  }
  var textbox1 = document.getElementById('txtTel1');
  var textbox2 = document.getElementById('txtTel2');
  var textbox3 = document.getElementById('txtTel3');

  EventUtil.addHandler(textbox1,'keyup',tabForward)
  EventUtil.addHandler(textbox2,'keyup',tabForward)
  EventUtil.addHandler(textbox3,'keyup',tabForward)
})()
```

**HTML5约束验证表单**

* 必填字段

  ```markup
  <input type='text' name='username' required>
  ```

* 其他输入类型

  ```markup
  <input type='email' name='email'>
  <input type='url' name='homepage'>
  ```

* 数值范围

number、range、datetime、datetime-local、date、month、week、还有time; 4. 输入模式 pattern属性，属性值为正则表达式，用于匹配文本中的值。

```markup
<input type='text' pattern='\d+' name='count'>
```

1. 检测有效性

   `checkValidity()`检测表单中某字段是否有效。

2. 禁用认证

**选择框脚本**

通过`<select>`和`<option>`元素创建：

```markup
<select name='location' id='selLocation'>
 <option>1</option>
 <option>1</option>
 <option>1</option>
 <option>1</option>
 <option>1</option>
</select>
```

**表单序列化**


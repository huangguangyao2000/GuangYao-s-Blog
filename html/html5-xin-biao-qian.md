# HTML5新标签

## &lt;embed&gt; 标签

定义嵌入的内容，比如插件

```text
<embed src="helloworld.swf" />
```

| 属性 | 描述 |
| :--- | :--- |
| src | 来源url |
| type | 类型 |
| width | 嵌入内容的宽度 |
| height | 嵌入内容的高度 |

## &lt;canvas&gt; 标签

用于绘制图像，\(通过脚本，通常是 JavaScript\)

* 本身并没有绘制能力，为绘制的**容器**。必须使用脚本来完成绘制。
* 逐**像素**进行渲染,依赖**分辨率**
* **不支持事件处理器**
* 能够以 .png 或 .jpg 格式保存结果图像
* 最**适合图像密集型**的游戏，其中的许多对象会被频繁重绘

## &lt;svg&gt;标签

* 不依赖分辨率
* 使用 XML 格式定义图形
* 支持事件处理器
* 最适合带有大型渲染区域的应用程序（比如谷歌地图）
* 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
* 不适合游戏应用

## &lt;video&gt;

video元素支持三种视频格式——Ogg，MPEG4，WebM

```text
<video src="movie.ogg" controls="controls">
</video>
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C5E;&#x6027;</th>
      <th style="text-align:left">&#x503C;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">autoplay</td>
      <td style="text-align:left">autoplay</td>
      <td style="text-align:left">&#x5982;&#x679C;&#x51FA;&#x73B0;&#x8BE5;&#x5C5E;&#x6027;&#xFF0C;&#x5219;&#x89C6;&#x9891;&#x5728;&#x5C31;&#x7EEA;&#x540E;&#x9A6C;&#x4E0A;&#x64AD;&#x653E;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">controls</td>
      <td style="text-align:left">controls</td>
      <td style="text-align:left">&#x5982;&#x679C;&#x51FA;&#x73B0;&#x8BE5;&#x5C5E;&#x6027;&#xFF0C;&#x5219;&#x5411;&#x7528;&#x6237;&#x663E;&#x793A;&#x63A7;&#x4EF6;&#xFF0C;&#x6BD4;&#x5982;&#x64AD;&#x653E;&#x6309;&#x94AE;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">height</td>
      <td style="text-align:left">pixels</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x89C6;&#x9891;&#x64AD;&#x653E;&#x5668;&#x7684;&#x9AD8;&#x5EA6;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">preload</td>
      <td style="text-align:left">preload</td>
      <td style="text-align:left">
        <p>&#x5982;&#x679C;&#x51FA;&#x73B0;&#x8BE5;&#x5C5E;&#x6027;&#xFF0C;&#x5219;&#x89C6;&#x9891;&#x5728;&#x9875;&#x9762;&#x52A0;&#x8F7D;&#x65F6;&#x8FDB;&#x884C;&#x52A0;&#x8F7D;&#xFF0C;&#x5E76;&#x9884;&#x5907;&#x64AD;&#x653E;&#x3002;</p>
        <p>&#x5982;&#x679C;&#x4F7F;&#x7528; &quot;autoplay&quot;&#xFF0C;&#x5219;&#x5FFD;&#x7565;&#x8BE5;&#x5C5E;&#x6027;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">src</td>
      <td style="text-align:left">url</td>
      <td style="text-align:left">&#x8981;&#x64AD;&#x653E;&#x7684;&#x89C6;&#x9891;&#x7684; URL&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">width</td>
      <td style="text-align:left">pixels</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x89C6;&#x9891;&#x64AD;&#x653E;&#x5668;&#x7684;&#x5BBD;&#x5EA6;&#x3002;</td>
    </tr>
  </tbody>
</table>

## &lt;math&gt;

数学标记语言，是一种基于XML（标准通用标记语言的子集）的标准

## &lt;author&gt;

播放音频文件

| audio/mpeg |  |
| :--- | :--- |
| Ogg | audio/ogg |
| Wav | audio/wav |
| MP3 | audio/mpeg |

## 表单元素

* &lt;datalist&gt;
* &lt;keygen&gt;
* &lt;output&gt;

### &lt;datalist&gt; 

输入域的选项列表

```markup
<datalist id="browsers">
  <option value="Internet Explorer">
  <option value="Firefox">
  <option value="Chrome">
  <option value="Opera">
  <option value="Safari">
</datalist>
```

![](../.gitbook/assets/bu-huo%20%283%29.JPG)

### &lt;keygen&gt; 

验证用户，表单的密钥对生成器字段。提交表单时，会生成两个键，一个是私钥，一个公钥。

### &lt;output&gt;

用于不同类型的输出，比如计算或脚本输出


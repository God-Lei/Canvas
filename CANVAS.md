### CANVAS

#### 1. 基本知识

1. <canvas> 是一个使用脚本(通常为 JavaScript )在其中绘制图形的 HTML 元素.
2. <canvas> IE9以上,Firefox,Opera,Chrome 和 Safari 支持 .
3. <canvas> 标签只有两个属性----width 和 height,默认为  300px * 150px .
4. 没有为 canvas 规定样式时, 将会完全透明



#### 2. 检测浏览器的支持性

​	var canvas = document.getElementById('tutorial');

​	if (canvas.getContext){
 	 var ctx = canvas.getContext('2d');
 	 // 支持
​	} else {
 	 //不支持
​	}

#### 3. canvas详细说明(方法)

<script>

    /*利用js绘制*/
    /*1.获取canvas对象*/
    var canvas = document.querySelector('canvas');
    
    /*2.获取绘制工具（获取上下文，环境）*/
    var ctx = canvas.getContext('2d');  /*2d绘制平面效果*/   /*webgl 游戏开发*/
    
    /*3.绘制图形*/
    /*100，100 基于画布的坐标*/
    
    /*4.移动画笔*/
    ctx.moveTo(100,100);
    
    /*5.绘制直线  绘制的是路径 */
    ctx.lineTo(200,100);
    
    /*6.描边*/
    ctx.stroke();
</script>

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/path.jpg?raw=true



#### 4. 补充(方法)

- ctx.strokeStyle = "blue";     /*设置描边的颜色*/    ( 不能写在   ctx.stroke()  的后面)

- 新建一条路径,样式的设置不会影响其他路径

  beginPath()

- 闭合路径

  closePath()

- /*设置线的宽度*/
  ctx.lineWidth = 10;


- 画笔的状态
  - lineWidth 线宽，默认1px
  - lineCap 线末端类型：(butt默认)、round、square 
  - lineJoin 相交线的拐点 miter(默认)、round、bevel
  - strokeStyle 线的颜色
  - fillStyle 填充颜色
  - setLineDash() 设置虚线
  - getLineDash() 获取虚线宽度集合
  - lineDashOffset 设置虚线偏移量（负值向右偏移）
- 参考文档
  - [w3school](http://www.w3school.com.cn/tags/html_ref_canvas.asp)
  - [Canvas_API](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial)

#### 5. 绘制一个三角形

- ctx.moveTo(100,100);
  ctx.lineTo(200,100);
  ctx.lineTo(200,200);
  ctx.lineTo(100,100);
  ctx.stroke();

  https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E7%BC%BA%E8%A7%92%E4%B8%89%E8%A7%92%E5%BD%A2.png?raw=true


- ctx.moveTo(100,100);
      ctx.lineTo(200,100);
      ctx.lineTo(200,200);

   //  ctx.lineTo(100,100);

      /*用闭合方法 填充这个缺角*/
      ctx.closePath();
      ctx.stroke();
  https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E9%97%AD%E5%90%88%E5%90%8E%E7%9A%84%E4%B8%89%E8%A7%92.png?raw=true

#### 6. 绘制一个矩形

绘制一个填充的矩形

fillRect( x ,y ,width, height)

strokeRect( x ,y ,width, height)

清除指定矩形区域，让清除部分完全透明

clearRect( x ,y ,width, height)
#### 7. 绘制折线

ctx.moveTo(100,100);
ctx.lineTo(150,50);
ctx.lineTo(200,100);
ctx.lineWidth = 10;
ctx.strokeStyle = 'red';
//线的两端形状

​	//默认						

ctx.lineCap = 'butt';		ctx.lineCap = 'square';				 ctx.lineCap = 'round';
ctx.lineJoin = 'miter';		ctx.lineJoin = 'bevel';				 ctx.lineJoin = 'round';
ctx.stroke();

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E4%B8%89%E7%A7%8D%E6%8A%98%E7%BA%BF.png?raw=true

#### 8. 绘制一条虚线

ctx.moveTo(100,100);
ctx.lineTo(300,100);
//设置虚线 需要使用的属性类型是数组
//实线长度10，空白的长度20，实线的长度30，空白10。。。。
ctx.setLineDash([10,20,30]);	//平均的虚线 ctx.setLineDash([10]);

/*虚线的偏移  负值向右偏移*/
ctx.lineDashOffset = -10;

/*获取设置的虚线规律*/
/*规律：一段不重复的实线和虚线的设置*/
console.log(ctx.getLineDash());

ctx.stroke();

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E8%99%9A%E7%BA%BF.png?raw=true

#### 9. 线的颜色渐变

ctx.moveTo(100,100);
ctx.lineWidth = 10;
ctx.lineTo(355,100);

//    白色  rgb(255,255,255);
//    红色  rgb(255,0,0);

ctx.lineWidth = 10;
for(var i = 1 ; i <= 255 ; i ++){
  ctx.beginPath();
  ctx.moveTo(100+i-1,100);
  ctx.lineTo(100+i,100);
  ctx.strokeStyle = 'rgb(255,'+(255-i)+','+(255-i)+')';
  ctx.stroke();
https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E7%BA%BF%E7%9A%84%E9%A2%9C%E8%89%B2%E6%B8%90%E5%8F%98.png?raw=true

渐变Gradients

- 线性渐变

createLinearGradient(x1, y1, x2, y2) createLinearGradient 方法接受 4 个参数，表示渐变的起点 (x1,y1) 与终点 (x2,y2)。

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E7%BA%BF%E6%80%A7%E6%B8%90%E5%8F%98.png?raw=true

- 径向渐变

createRadialGradient(x1, y1, r1, x2, y2, r2) createRadialGradient 方法接受 6 个参数，前三个定义一个以 (x1,y1) 为原点，半径为 r1 的圆，后三个参数则定义另一个以 (x2,y2) 为原点，半径为 r2 的圆。

创建出 canvasGradient 对象后，我们就可以用 addColorStop 方法给它上色了。

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E5%BE%84%E5%90%91%E6%B8%90%E5%8F%98(%E5%90%8C%E5%BF%83).png?raw=true

- gradient.addColorStop(position, color)

addColorStop 方法接受 2 个参数，position 参数必须是一个 0.0 与 1.0 之间的数值，表示渐变中颜色所在的相对位置。例如，0.5 表示颜色会出现在正中间。color 参数必须是一个有效的 CSS 颜色值（如 #FFF， rgba(0,0,0,1)，等等）。



- 不同心但外圆包含内圆

```
var rr2=cxt.createRadialGradient(250,250,20,260,260,50);
  rr2.addColorStop(0,'red');
  rr2.addColorStop(.5,'yellow');
  rr2.addColorStop(1,'blue');
  cxt.fillStyle=rr2;
  cxt.fillRect(50,50,400,400);
  cxt.fill();
```

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E4%B8%8D%E5%90%8C%E5%BF%83(%E5%A4%96%E5%8C%85%E5%86%85).png?raw=true



- 不同心，外圆内圆分离

  ```
  var rr3=cxt.createRadialGradient(250,250,30,350,250,50);
    rr3.addColorStop(0,'red');
    rr3.addColorStop(.8,'yellow');
    rr3.addColorStop(1,'blue');
    cxt.fillStyle=rr3;
    cxt.fillRect(100,100,300,300);
  ```

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E4%B8%8D%E5%90%8C%E5%BF%83(%E5%A4%96%E4%B8%8E%E5%86%85%E5%88%86%E7%A6%BB).png?raw=true

#### 10.绘制一个弧线   或  圆

- arc(x, y, radius, startAngle, endAngle, anticlockwise)

  arc()

  - x 圆心横坐标
  - y 圆心纵坐标
  - r 半径
  - startAngle 开始角度
  - endAngle 结束角度
  - anticlockwise 是否逆时针方向绘制（默认false表示顺时针；true表示逆时针）



#### 11.绘制文本

- ctx.font = '微软雅黑' 设置字体
- strokeText()
- fillText(text,x,y,maxWidth)
  - text 要绘制的文本
  - x,y 文本绘制的坐标（文本左下角）
  - maxWidth 设置文本最大宽度，可选参数
- ctx.textAlign文本水平对齐方式，相对绘制坐标来说的
  - left
  - center
  - right
  - start 默认
  - end
  - direction属性css(rtl ltr) start和end于此相关
    - 如果是ltr,start和left表现一致
    - 如果是rtl,start和right表现一致
- ctx.textBaseline 设置基线（垂直对齐方式  ）
  - top 文本的基线处于文本的正上方，并且有一段距离
  - middle 文本的基线处于文本的正中间
  - bottom 文本的基线处于文本的证下方，并且有一段距离
  - hanging 文本的基线处于文本的正上方，并且和文本粘合
  - alphabetic 默认值，基线处于文本的下方，并且穿过文字
  - ideographic 和bottom相似，但是不一样
- measureText() 获取文本宽度obj.width




#### 12.做动画

##### 	绘制图片

- drawImage()
  - 三个参数drawImage(img,x,y)
    - img 图片对象、canvas对象、video对象
    - x,y 图片绘制的左上角
  - 五个参数drawImage(img,x,y,w,h)
    - img 图片对象、canvas对象、video对象
    - x,y 图片绘制的左上角
    - w,h 图片绘制尺寸设置(图片缩放，不是截取)
  - 九个参数drawImage(img,x,y,w,h,x1,y1,w1,h1)
    - img 图片对象、canvas对象、video对象
    - x,y,w,h 图片中的一个矩形区域
    - x1,y1,w1,h1 画布中的一个矩形区域




#### 13. 坐标变换

- 平移 移动画布的原点
  - translate(x,y) 参数表示移动目标点的坐标
- 缩放
  - scale(x,y) 参数表示宽高的缩放比例
- 旋转
  - rotate(angle) 参数表示旋转角度 



#### 14. 移动(translate)

- canvas的移动是指移动 canvas 和它的原点到一个不同的位置。

- ```
  translate(x, y)
  ```

  例子：

  ```
  ctx.fillRect(0,0,100,100);
  ctx.save();
  ctx.translate(60,60);
  ctx.fillStyle="red";
  ctx.fillRect(0,0,100,100);
  ctx.restore();
  ```

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E7%A7%BB%E5%8A%A8.png?raw=true

#### 15. 阴影 Shadows

shadowOffsetX = float shadowOffsetX 和 shadowOffsetY 用来设定阴影在 X 和 Y 轴的延伸距离，它们是不受变换矩阵所影响的。

负值表示阴影会往上或左延伸，正值则表示会往下或右延伸，它们默认都为 0。 

shadowOffsetY = float shadowOffsetX 和 shadowOffsetY 用来设定阴影在 X 和 Y 轴的延伸距离，它们是不受变换矩阵所影响的。

负值表示阴影会往上或左延伸，正值则表示会往下或右延伸，它们默认都为 0。 

shadowBlur = float shadowBlur 用于设定阴影的模糊程度，其数值并不跟像素数量挂钩，也不受变换矩阵的影响，默认为 0。 

shadowColor = color shadowColor 是标准的 CSS 颜色值，用于设定阴影颜色效果，默认是全透明的黑色。

例子：

```
var img=new Image();
img.src="图片地址";
img.onload=function(){
  cxt.shadowOffsetX=10;
  cxt.shadowOffsetY=10;
  cxt.shadowBlur=8;
  cxt.shadowColor="#333";
  cxt.drawImage(img,10,10);
}
```



#### 16.旋转

用于以原点为中心旋转 canvas。

```
rotate(angle)
cxt.beginPath();
cxt.moveTo(0,50);
cxt.lineTo(100,50);
cxt.stroke();
cxt.save();
cxt.rotate(Math.PI/12);
cxt.strokeStyle="red";
cxt.beginPath();
cxt.moveTo(0,50);
cxt.lineTo(100,50);
cxt.stroke();
cxt.restore();
```


https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E6%97%8B%E8%BD%AC.png?raw=true

#### 17.缩放

**缩放（scale）**

```
scale(x, y)

```

例子：

```
cxt.fillRect(20,20,50,50);
cxt.save();
cxt.scale(.5,.5);
cxt.fillStyle="red";
cxt.fillRect(20,20,50,50);
```

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E7%BC%A9%E6%94%BE.png?raw=true

#### 18. **Canvas 填充规则**

当我们用到 fill（或者 clip和isPointinPath ）你可以选择一个填充规则，该填充规则根据某处在路径的外面或者里面来决定该处是否被填充，这对于自己与自己路径相交或者路径被嵌套的时候是有用的。

两个可能的值： "nonzero": 默认值. "evenodd":

```
cxt.beginPath();
  cxt.arc(100,100,50,0,Math.PI*2,true);
  cxt.arc(100,100,20,0,Math.PI*2,true);
  cxt.fill("evenodd");
```

https://github.com/God-Lei/Typora-images/blob/master/Typora%E4%B8%ADimages/%E5%A1%AB%E5%85%85%E8%A7%84%E5%88%99.png?raw=true

#### 未完待续......


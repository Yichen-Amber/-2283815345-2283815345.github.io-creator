   # 2283815345.github.io
            浏览器渲染原理
            transform介绍
            transition介绍
            总结
           
   

# 浏览器渲染原理
## 浏览器渲染步骤：
* 根据HTML构建HTML树（DOM树）
* 根据CSS构建CSS树（CSSOM）
* 将两棵树合并成渲染树（render tree）
* Layout布局（文档流、盒模型、计算大小和位置）
* Paint绘制（把边框颜色、文字颜色、阴影等画出来）
* Compose合成（根据层叠关系展示画面）
    
### 三种更新方式：
* JS/CSS > 样式 > 布局 > 绘制 > 合成
* S/CSS > 样式 > 绘制 > 合成
* JS/CSS > 样式 > 合成
    
第一种方式，全部走一遍，例子： ```div.remove()```会触发当前元素消失，其他元素重布局（```relayout```）

第二种方式，跳过布局，例子： 改变背景颜色，直接重绘（```repaint```）+ 合成（```composite```）

第三种方式，跳过布局和绘制，例子： 改变transform，只需要合成（```composite```）


从上面可以看出，改变不同的属性会造成不同的渲染步骤，那么我们怎么知道改变了某个属性会怎么渲染呢？
这时候就要用到"CSSTriggers.com"CSSTriggers.com个网站了，在里面可以查询CSS的各个属性都触发了哪些渲染步骤，十分的方便。


最后是一些google的参考资料：

[渲染树构建、布局及绘制](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction)   
[渲染性能](https://developers.google.com/web/fundamentals/performance/rendering/)       
[使用transform来实现动画](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)


# transform介绍
  
## 四个常用功能
* 位移translate
* 缩放scale
* 旋转rotate
* 倾斜skew

    注意：
        一般都需要配合transition过渡
      linline元素不支持transform，需要先变成block
    
### transform---translate常用写法：
```translateX(<length-percentage>)```

```translateY(<length-percentage>)```

```translate(<length-percentage>,<length-percentage>)```

```translateZ(<length-percentage>)```

```translate3d(x,y,z)```
   
    注意：
        要学会看懂MDN的语法示例
        translate(-50%,-50%)可做绝对定位元素的居中
  
### transform---scale常用写法
```scaleX(<number>)```

```scaleY(<number>)```
```scale(<number>,<number>?)```

    
### transform---rotate常用写法：
```rotate([<angle>|<zero>])```

```rotateX([<angle>|<zero>])```

```rotateY([<angle>|<zero>])```

```rotateZ([<angle>|<zero>])```

```rotate3d```
       
    
### transform---skew常用写法：

        
```skewX([<angle>|<zero>])```
```skewY([<angle>|<zero>])```
```skew([<angle>|<zero>],[<angle>|<zero>]?)```
 
  
### transform多重效果

```组合使用```

```transform：scale(0.5)translate(-100%,-100%);```

```tranform:none;取消所有```
    
## ransition介绍
    
作用:补充中间帧

### 语法：
```transition:属性名 时长 过渡方式 延迟```

```transition:left 200ms linear```

```可以用逗号分隔两个不同属性```

```transition:left 200ms,top 400ms```

```可以用all代表所有属性```

```transition:all 200ms```

### 过渡方式有：
```linear|ease|ease-in|ease-out|ease-in-out|cubic-bezier|step-start|step-end|steps,具体含义要靠数学知识```

### 并不是所有属性都能过渡：

```display：none=>block没法过渡；```

```一般改成visibility:hidden=>visible```

```display和visibility的区别：```
   

##  总结:

* 还是需要上手前代码；
* 很多东西多查看MDN文档；
* 坚持记笔记，好记性不如烂笔头。    
 

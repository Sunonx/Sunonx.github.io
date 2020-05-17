# LoveIt-AddVideo

# 主题优化（二）：添加视频
`在博文中插入保持宽高比的iframe视频`

##### 问题描述：
视频无法根据页面宽度自动调整宽高比，导致视频在手机这种小屏幕上会出现上下黑边。
##### 解决方案：
这个问题可以使用`CSS`来解决。最简单的方式就是将视频的iframe放在一个保持宽高比的div中（代码源自[此处](https://igloo302.github.io/2020/%E5%9C%A8hugo%E5%8D%9A%E5%AE%A2%E6%8F%92%E5%85%A5%E4%BF%9D%E6%8C%81%E5%AE%BD%E9%AB%98%E6%AF%94%E7%9A%84iframe%E8%A7%86%E9%A2%91/)）：

(1)打开~\themes\主题名\assets\css，在—_custom.scss中添加
```javascript
/* 这个规则规定了iframe父元素容器的尺寸，16:9的近似值为56%*/  
.selfadapting-video {   
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 56%; /* 高度应该是宽度的56% */
  }   
    
  /* 设定iframe的宽度和高度，让iframe占满整个父元素容器 */
  .selfadapting-video iframe {   
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
  }
```

(2)删去iframe中关于高度和宽度的设定，将其添加到 `<div class="selfadapting-video-bilibili"> ... </div>`之中：
```javascript
<div class="selfadapting-video">
<iframe src='https://player.youku.com/embed/XMjk4NzA1OTMzNg=='  scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="max-width: 100%"></iframe>
</div>
```


##### 对于优酷、Youtube这种，这个CSS已经可以用了，但是我常用的B站的iframe有一个特殊的机制：


<div class="selfadapting-video">
<iframe src='https://player.youku.com/embed/XNDA4ODQ5OTcxNg=='  scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="max-width: 100%"></iframe>
</div>


##### 对于B站
哈哈，开心的是，该主题[LoveIt]()已经内置好了`shortcodes`模板，可直接使用

具体详细配置，可参考[一篇博文](https://blog.iyu.icu/posts/shortcode_bilibili/)

**使用方法**：


在markdown文章中直接写 `{{ <bilibili BV17z4y1d72b> }}`（ps:{{和<之间没有空格）

###### 使用效果如下：
{{<bilibili id="BV17z4y1d72b" autoplay="true">}}

<center>·end·</center>

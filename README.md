# Animations
通过 css3 animation 实现多个入门级动画效果

# Animation 动画的组成

CSS Animation 动画是由两个基础模块构成：

1. 关键帧（keyframes）- 定义动画的阶段和样式
1. Animation 属性 - 将 @keyframes 赋给一个特定的CSS元素，并定义它是如何动画的。

## 组成模块 #1: `Keyframes`

关键帧（keyframes）定义了动画在动画时间轴（animation timeline）的每个阶段是怎样的。每个 @keyframes 由以下部分组成：

- 动画的名字
- 动画的阶段：动画的每个阶段都用百分比表示。0%表示动画的开始状态。100%表示动画的结束状态。可以在中间添加多个中间状态。
- CSS 属性：为动画时间轴（animation timeline）的每个阶段定义的CSS属性。

举例：

```css
/*
让我们看看一个简单的@关键帧，我命名为“bounceIn”。
这个@关键帧有三个阶段。
在第一阶段(0%)，将元素设置为全透明（CSS3 opacity 0），并使用 CSS3 transform scale 将其缩小到默认大小的10%。
在第二阶段(60%)，元素逐渐变为完全不透明（CSS3 opacity 1），并增大到默认大小的120%。
在最后阶段(100%)，它稍微缩小并回到默认大小。
*/
@keyframes bounceIn {
  0% {
    transform: scale(0.1);
    opacity: 0;
  }
  60% {
    transform: scale(1.2);
    opacity: 1;
  }
  100% {
    transform: scale(1);
  }
}

// 在动画中结合 CSS3 transform 是真正神奇的地方！
```

## 

## 组成模块 #2: `animation`属性

一旦定义了 @keyframes，就必须添加 animation 属性才能使你的动画发挥作用。

animation 属性做两件事：

1. 将 @keyframes 分配给你想要动画化的元素。
1. 定义了动画的方式。

animation 属性被添加到你想要动画的 CSS 选择器（或元素）中。必须添加以下两个 animation 属性才能使动画生效：

- animation-name: 动画的名称，在 @keyframes 中定义。
- animation-duration: 动画的持续时间，以秒（如：5s）或毫秒（如：200ms）为单位。

继续上面的 bounceIn 例子，我们将添加 animation-name 和 animation-duration 到我们想要动画的 div。

```css
div {
  animation-duration: 2s;
  animation-name: bounceIn;
}

/* 可以简写为 */
div {
  animation: bounceIn 2s;
}
```

![](https://cdn.nlark.com/yuque/0/2022/gif/22203542/1647495362195-69848b87-e799-48bb-a821-5f1fc7f216a9.gif#clientId=u25433b3e-6a17-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=222&id=u97c1c157&margin=%5Bobject%20Object%5D&originHeight=358&originWidth=499&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u738d6625-dab1-46e5-a1e2-f522663c283&title=&width=309)

## `animation` 属性简写

为了更简洁和更快地编码，建议您使用 animation 的简写。

```css
animation: [animation-name] [animation-duration] [animation-timing-function]
[animation-delay] [animation-iteration-count] [animation-direction]
[animation-fill-mode] [animation-play-state];
```

为了使动画正确运行，需要遵循适当的简写顺序，并且至少指定前两个值。

## 注意前缀

许多基于 Webkit 的浏览器仍然使用 `-webkit`前缀的 animations, keyframes, 和 transitions 版本。在它们采用标准版本之前，需要在代码中同时包含无前缀和 Webkit 版本。(为了简单起见，我在示例中只使用无前缀的版本。)

为了让工作更轻松，可以考虑使用 Bourbon，这是一个 Sass mixin 库，包含所有现代浏览器的最新属性前缀。

```css
div {
  @include animation(bounceIn 2s);
}

@include keyframes(bouncein) { /* styles */}
```

## 额外的 `animation` 属性

除了必需的 animation-name 和 animation-duration 属性外，你还可以使：以下属性进一步定制和创建复杂的动画：

- animation-timing-function
- animation-delay
- animation-iteration-count
- animation-direction
- animation-fill-mode
- animation-play-state

### animation-timing-function

定义动画的速度曲线或速度。可以使用以下预定义的选项：ease、linear、ease-in、ease-out、ease-in-out、initial、inherit。(甚至可以使用三次贝塞尔曲线创建自定义的时间轴函数)

默认值是ease，它开始时很慢，然后加速，然后慢慢变慢。
![](https://cdn.nlark.com/yuque/0/2022/gif/22203542/1647495324360-6fddf9ec-9f1a-4983-9e01-c38eba06ba60.gif#clientId=u25433b3e-6a17-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=174&id=uae884bfc&margin=%5Bobject%20Object%5D&originHeight=315&originWidth=431&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uaa7c9b07-ce93-402f-a117-46038b06736&title=&width=238)

### animation-dalay

指定动画何时开始。正值（如：2）将在动画被触发 2 秒后开始动画。在此之前，该元素将保持无活动状态。负值（如：-2）将立即执行动画，动画跳过 2 秒进入动画周期。

单位为秒(s)、毫秒(mil)。
![](https://cdn.nlark.com/yuque/0/2022/gif/22203542/1647496576190-fcc98ca4-a9b1-44ed-8f56-781c3d8e67c9.gif#clientId=u25433b3e-6a17-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=194&id=ua6abbca5&margin=%5Bobject%20Object%5D&originHeight=428&originWidth=539&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uee48b02e-489a-4943-9e47-887c75b568f&title=&width=244)

### animation-iteration-count

指定动画播放的次数。
`#`- 特定的迭代次数（默认为 1）
`infinite` - 动画一直重复
`initial` - 将迭代计数设置为默认值
`inherit` - 从父类继承该值
![](https://cdn.nlark.com/yuque/0/2022/gif/22203542/1647496933870-1ca1cdf0-5768-48fe-99ab-5bfd0e16163e.gif#clientId=u25433b3e-6a17-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=167&id=u8f5e60ef&margin=%5Bobject%20Object%5D&originHeight=358&originWidth=499&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u93daf5c1-72b2-4bb1-a1a4-0282401ae96&title=&width=233)

### animation-direction

指定动画是向前播放、反向播放还是交替播放。

可能的值包括：
`normal`（默认）- 动画向前播放。在每个循环中，动画重置到开始状态(0%)，并再次播放(100%)。
`reverse` - 动画向后播放。在每个循环中，动画重置到结束状态(100%)并向后播放(到0%)。
`alternate` - 动画每个循环都反转方向。在每个奇数周期，动画向前播放(0%到100%)。在每一个偶数循环中，动画会向后播放 (100% 到 0%)。
`alternate-reverse` - 动画在每个循环中都是反向的。在每个奇数周期，动画反向播放(100% 到 0%)。在每个偶数周期中，动画向前播放(0% 到 100%)。
![](https://cdn.nlark.com/yuque/0/2022/gif/22203542/1647497715413-f1e0e4fa-0f73-44ca-b98d-591ae94bb0dc.gif#clientId=u25433b3e-6a17-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=173&id=u888ada1b&margin=%5Bobject%20Object%5D&originHeight=429&originWidth=706&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=ueb4f2b49-9cb3-4509-8f2a-208fecd5d66&title=&width=284)

### animation-fill-mode

动画在播放之前（动画延迟）或之后，其动画效果是否可见。

默认情况下，动画在动画开始之前(如果有动画延迟)或动画结束之后不会影响元素的样式。animation-fill-mode属性可以用以下可能的值覆盖此行为：

`backwards` - 在动画开始之前(动画延迟期间)，初始关键帧的样式(0%)被应用到元素上。
`forwards` - 动画完成后，在最终关键帧中定义的样式(100%)被元素保留。
`both` - 动画将遵循向前和向后的规则，在动画之前和之后扩展动画属性。
`normal` (default) - (默认)-动画不应用任何样式的元素，在动画之前或之后。
![](https://cdn.nlark.com/yuque/0/2022/gif/22203542/1647500125520-0c2aeb93-c852-4d24-90d7-952a66c97670.gif#clientId=u25433b3e-6a17-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=202&id=uc8c70980&margin=%5Bobject%20Object%5D&originHeight=462&originWidth=785&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u48212865-39c6-4276-b435-a67bf447d9f&title=&width=344)

### animation-play-state

指定动画是否正在播放或暂停。恢复暂停的动画会在动画停止的地方开始。

可能的值包括：
`playing`- 动画正在运行
`pause` - 动画当前处于暂停状态
![](https://cdn.nlark.com/yuque/0/2022/gif/22203542/1647501492719-43cdaa39-4f8c-4133-ba75-1d92d07b7b15.gif#clientId=u25433b3e-6a17-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=173&id=ud5ad91ba&margin=%5Bobject%20Object%5D&originHeight=462&originWidth=499&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u623f2a4b-c110-45bc-902c-de5a7f8e6dc&title=&width=187)

```css
.div:hover {
  animation-play-state: paused;
}
```

## 多个动画

要向一个选择器添加多个动画，只需用逗号分隔这些值。

```css
.div {
  animation: slideIn 2s, rotate 1.75s;
}
```


> 参考文献：[https://thoughtbot.com/blog/css-animation-for-beginners](https://thoughtbot.com/blog/css-animation-for-beginners)
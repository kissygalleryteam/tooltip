## 综述

作者：ni184775761@gmail.com

功能：绑定Tooltip和其触发节点事件，并根据屏幕空间计算显示位置

* 快速建立trigger和tooltip的hover显示事件关系，添加延迟消失机制
* 自动根据用户的视域情况调整显示位置（设置窗口大小自行尝试效果）
* 箭头位置/tooltip位置等均可配置
* 可选的Bubble样式

源码：[index.js](https://github.com/kissygalleryteam/tooltip/1.0/index.js)

## 组件快速使用

### HTML

可以自定义Tooltip样式，也可以通过use`gallery/tooltip/1.0/assets/bubble.css`并配合下面的bubble结构来呈现气泡类型的Tooltip样式效果

```html
<!-- 下面为tooltip的触发节点，trigger为触发节点，refer为tooltip计算的参考点，两者可以为一个节点 -->
<div class="J_Trigger tooltip-trigger">
    <div class="J_Refer tooltip-refer"></div>
</div>

<!--下面使用组件自带的bubble样式，只要遵循下面的结构，并添加'bubble'和'arrow-*'样式就可以 -->
<div class="bubble J_Tooltip">
    <!-- 箭头，通过arrow-top, arrow-left, arrow-right, arrow-bottom来设置箭头方向 -->
    <span class="J_TooltipArrow arrow-top"><i></i></span>
    <div class="tooltip-content">
        这是Tooltip
    </div>
</div>

```

### JavaScript

使用`#attach()`方法对trigger和tooltip之间建立关系

```javascript
// 引入Tooltip，注意bubble.css为可选
KISSY.use('gallery/tooltip/1.0/index, gallery/tooltip/1.0/assets/bubble.css', function(S, Tooltip) {

    Tooltip.attach({
        trigger: '.J_Trigger',      // 用于触发Tooltip出现的节点
        refer: '.J_Refer',          // 用于Tooltip进行位置计算的节点
        tooltip: '.J_Tooltip',      // Tooltip节点
        // ------------ 以下参数可选 ------------------------------
        position: 'right',          // 可选：默认情况下，Tooltip会根据当前视域进行位置的计算，但是你也可以通过这个属性来强制Tooltip的显示位置，可用值：top,bottom,right,left
        arrowAlign: 'center',       // 可选：Tooltip的箭头和refer的位置关系: left,center,right
        align: 'center',            // 可选：Tooltip主体和refer的位置关系
        container: '.container',    // 可选：默认Tooltip将插入到body中，可以通过该字段限定容器
        arrowHook '.J_TooltipArrow', // 可选：箭头的钩子，默认为.J_TooltipArrow
        onHide: function( trigger, tooltip ){ /* do sth */ },
        onShow: function( trigger, tooltip ){ /* do sth */ }
    });
});

```

还可以通过`#freeze()`方法来将某个Tooltip固定在某个trigger中

```javascript
Tooltip.freeze( config ); // Config同attach方法参数，但是没有onHide与onShow
```

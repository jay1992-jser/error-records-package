### List 组件 使用过程中的兼容问题

##### 1、针对部分Android 机型， List组件下拉加载过后，上拉加载不触发onload事件问题；

```
<template>
	<list  @loadmore="onloadmore" offset-accuracy=100 loadmoreoffset=100 ref="listWrap">
	...
		
	</list>
</template>	

<script>
	export default {
        methods:{
            onloadmore() {
                this.$ref.listWrap.resetLoadmore(); // 重置loadmore 非常有必要
            }
        }
	} 
</script>
	
```

#####  2、针对Android 机型，List 组件部分区域无法加载完全的问题；

方案：根节点利用flex盒模型属性，自动铺满屏幕；注意事项：list组件必须是根节点的子组件，而不能是孙组件或者更深层级的嵌套；

```
<template>
  <div class="app flex1">
  	<div>...</div> // 
    <list  offset-accuracy=100 loadmoreoffset=100 ref="listWrap">
        ...
    </list>
    <div>...</div>
  </div>
</template>	
```


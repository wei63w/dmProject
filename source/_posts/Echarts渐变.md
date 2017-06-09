---
title: Echarts渐变
date: 2016-12-12 17:53:14
categories: 
	- IOS
tags: 
	- Echarts
    
---

#### 线性渐变，前四个参数分别是 x0, y0, x2, y2, 范围从 0 - 1，相当于在图形包围盒中的百分比，如果最后一个参数传 `true`，则该四个值是绝对的像素位置
```
color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
  offset: 0, color: 'red' // 0% 处的颜色
}, {
  offset: 1, color: 'blue' // 100% 处的颜色
}], false)
```
#### 径向渐变，前三个参数分别是圆心 x, y 和半径，取值同线性渐变
```
color: new echarts.graphic.RadialGradient(0.5, 0.5, 0.5, [...], false)
// 纹理填充
color: new echarts.graphic.Pattern(
  imageDom, // 支持为 HTMLImageElement, HTMLCanvasElement，不支持路径字符串
  'repeat' // 是否平铺, 可以是 repeat-x, repeat-y, no-repeat
)
```
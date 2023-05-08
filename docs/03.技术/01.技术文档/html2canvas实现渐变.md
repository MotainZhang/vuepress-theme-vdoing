---
title: html2canvas实现渐变
date: 2022-08-11 10:51:18
permalink: /pages/9a7ee40fc232253e
categories:
  - 技术
  - 技术文档
tags:
  -
author:
  name: MotainZhang
  link: https://github.com/MotainZhang
---

# html2canvas插件本身不支持文字渐变字（`background-clip: text` nor `box-shadow` are currently supported），如果要实现渐变字，这里涉及到修改插件源码

# 第一步

## 实现渐变字需要用到canvas的`createLinearGradient`需要四个参数，其中两个参数需要计算出来

| 参数 | 描述 |
| --- | --- |
| x0 | 渐变开始点的 x 坐标 |
| y0 | 渐变开始点的 y 坐标 |
| x1 | 渐变结束点的 x 坐标 |
| y1 | 渐变结束点的 y 坐标 |

# 第二步修改renderNodeContent(6845行)，case1(6857行)

## 找到html2canvas源码`renderNodeContent`方法，里面case1渲染文本的方法`renderTextNode`添加代码

```
  var changyiWidth = 0;
  var changyiLeft = child.textBounds[0].bounds.left;
  for (var changyii = 0; changyii < child.textBounds.length; changyii++) {
	changyiWidth += child.textBounds[changyii].bounds.width;
  }
  changyiWidth = changyiLeft + changyiWidth;
  return [4 /*yield*/, this.renderTextNode(child, styles, changyiWidth, changyiLeft)];
```

# 第三步修改renderTextNode方法(6745行)

## 找到 html2canvas源码`renderTextNode`方法加入canvas渐变，注意这里需要css加入特殊样式来区别哪些字需要渐变（必须输唯一的）

## 例如，这里加了一个fontWeight:410需要渐变字

```
if (styles.fontWeight == 410) {
	  var gradient = _this.ctx.createLinearGradient(changyiLeft, 0, changyiWidth, 0);
	  gradient.addColorStop(0, '#946036');
	  gradient.addColorStop(0.17, '#B37B46');
	  gradient.addColorStop(0.22, '#E3BC7B');
	  gradient.addColorStop(0.26, '#FDDF98');
	  gradient.addColorStop(0.48, '#B37B46');
	  gradient.addColorStop(0.58, '#C9985D');
	  gradient.addColorStop(0.64, '#D2A467');
	  gradient.addColorStop(1, '#946036');
	  _this.ctx.fillStyle = gradient;
}
```

# css样式里加入样式，color: transparent必须加，也不能是别的色值

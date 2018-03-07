---
title: 引入FastClick后使用js模拟input点击事件失败
date: 2018-03-07 10:41:13
tags: [移动端填坑记, fastclick]
---

## 简述

有一需求，点击一按钮出来选择框，选择上传图片类型，选择玩类型后弹出系统文件选择框，根据需求自然而然想到了js模拟点击事件。很简单直接调用<code>fileInput.click()就可以？？？</code>

## 事故现场

```js
// jsx
<input 
  style={{display: 'none'}}  
  ref={i => this.fileIput = i} 
  type="file"  
  onChange={this.onChange} />

// 调用
this.ref.fileInput.click()
```
调用<code>this.ref.fileInput.click()</code>并没有出现想要的效果（chrome 手机模式下）.
试了下手机端
Android 正常
IOS 失败
神奇的是调用两次<code>this.ref.fileInput.click()</code>，chrome， IOS都正常了，但是android却不正常了弹出两次文件选择框。。。
心想是不是<code>fastclick</code>导的鬼，tmd还真是，去掉<code>fastclick</code>都正常了，只需要调用一次<code>this.ref.fileInput.click()</code>
但是fastclick不能去掉啊，移动端有300ms延迟,查阅了Api后发现官网还真有解决办法，就是让input使用原生事件，具体操作就是给你点击的那个元素（不是input）添加<code>className="needsclick"</code>即可

源码如下
```js
/**
  * Determine whether a given element requires a native click.
  *
  * @param {EventTarget|Element} target Target DOM element
  * @returns {boolean} Returns true if the element needs a native click
  */
FastClick.prototype.needsClick = function(target) {
  switch (target.nodeName.toLowerCase()) {

  // Don't send a synthetic click to disabled inputs (issue #62)
  case 'button':
  case 'select':
  case 'textarea':
    if (target.disabled) {
      return true;
    }

    break;
  case 'input':

    // File inputs need real clicks on iOS 6 due to a browser bug (issue #68)
    if ((deviceIsIOS && target.type === 'file') || target.disabled) {
      return true;
    }

    break;
  case 'label':
  case 'iframe': // iOS8 homescreen apps can prevent events bubbling into frames
  case 'video':
    return true;
  }

  return (/\bneedsclick\b/).test(target.className);
};
```
看完源码发现我的标题得改了。。。(不只是input，不只是click事件)
> 具体问什么会产生这种问题，这里就不做深究了可以[点击这里查看](https://segmentfault.com/a/1190000009246194)

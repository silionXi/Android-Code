**本文转自与郭霖的博客，原博客地址参考[这儿][1]**
-----------------------------

## Android事件分发机制完全解析，带你从源码的角度彻底理解(上)

其实我一直准备写一篇关于Android事件分发机制的文章，从我的第一篇博客开始，就零零散散在好多地方使用到了Android事件分发的知识。也有好多朋友问过我各种问题，比如：onTouch和onTouchEvent有什么区别，又该如何使用？为什么给ListView引入了一个滑动菜单的功能，ListView就不能滚动了？为什么图片轮播器里的图片使用Button而不用ImageView？等等……对于这些问题，我并没有给出非常详细的回答，因为我知道如果想要彻底搞明白这些问题，掌握Android事件分发机制是必不可少的，而Android事件分发机制绝对不是三言两语就能说得清的。
在我经过较长时间的筹备之后，终于决定开始写这样一篇文章了。目前虽然网上相关的文章也不少，但我觉得没有哪篇写得特别详细的(也许我还没有找到)，多数文章只是讲了讲理论，然后配合demo运行了一下结果。而我准备带着大家从源码的角度进行分析，相信大家可以更加深刻地理解Android事件分发机制。
阅读源码讲究由浅入深，循序渐进，因此我们也从简单的开始，本篇先带大家探究View的事件分发，下篇再去探究难度更高的ViewGroup的事件分发。
那我们现在就开始吧！比如说你当前有一个非常简单的项目，只有一个Activity，并且Activity中只有一个按钮。你可能已经知道，如果想要给这个按钮注册一个点击事件，只需要调用：
```java
button.setOnClickListener(new OnClickListener() {
	@Override
	public void onClick(View v) {
		Log.d("TAG", "onClick execute");
	}
});
```
这样在onClick方法里面写实现，就可以在按钮被点击的时候执行。你可能也已经知道，如果想给这个按钮再添加一个touch事件，只需要调用：
```java
button.setOnTouchListener(new OnTouchListener() {
	@Override
	public boolean onTouch(View v, MotionEvent event) {
		Log.d("TAG", "onTouch execute, action " + event.getAction());
		return false;
	}
});
```
onTouch方法里能做的事情比onClick要多一些，比如判断手指按下、抬起、移动等事件。那么如果我两个事件都注册了，哪一个会先执行呢？我们来试一下就知道了，运行程序点击按钮，打印结果如下：
![打印结果](http://img.blog.csdn.net/20160824111202077)



--------
[1]:http://blog.csdn.net/guolin_blog/article/details/9097463
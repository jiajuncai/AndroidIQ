# AndroidIQ
Android Interview questions
#### OkHttps怎么支持https
#### 过度绘制由哪些造成，解决办法，用哪些控件优化（https://www.jianshu.com/p/2cc6d5842986）
* 合理选择控件容器
* 去掉window的默认背景
* 去掉其他不必要的背景
* ClipRect & QuickReject
* 使用ViewStub占位
* 用Merge减少布局深度
* 善用draw9patch
* 慎用Alpha
* 避免“OverDesign”
#### handler机制
不同线程之间的通信。为了避免ANR，我们会通常把 耗时操作放在子线程里面去执行，因为子线程不能更新UI，所以当子线程需要更新的UI的时候就需要借助到安卓的消息机制，也就是Handler机制了。
#### 动画种类，特点，区别
* Drawable Animation也就是所谓的帧动画，Frame动画。指通过指定每一帧的图片和播放时间，有序的进行播放而形成动画效果。
* View Animation视图动画，也就是所谓补间动画，Tween动画。指通过指定View的初始状态、变化时间、方式，通过一系列的算法去进行图形变换，从而形成动画效果，主要有Alpha、Scale、Translate、Rotate四种效果。注意：只是在视图层实现了动画效果，并没有真正改变View的属性。
* Property Animation属性动画，通过不断的改变View的属性，不断的重绘而形成动画效果。相比于视图动画，View的属性是真正改变了。注意：Android 3.0(API 11)以上才支持。
#### Glide的缓存有几种
Glide 缓存策略 内存缓存和磁盘缓存
#### 解析XML方式，特点
* DOM:处理大型文件时其性能下降的非常厉害。这个问题是由DOM的树结构所造成的，这种结构占用的内存较多，而且DOM必须在解析文件之前把整个文档装入内存,适合对XML的随机访问
* SAX:不现于DOM,SAX是事件驱动型的XML解析方式。它顺序读取XML文件，不需要一次全部装载整个文件。当遇到像文件开头，文档结束，或者标签开头与标签结束时，它会触发一个事件，用户通过在其回调事件中写入处理代码来处理XML文件，适合对XML的顺序访问 
* STAX:Streaming API for XML (StAX)
#### 如何选择ListView还是RecycleView
列表页展示界面，需要支持动画，或者频繁更新，局部刷新，建议使用RecyclerView，更加强大完善，易扩展；其它情况(如微信卡包列表页)两者都OK，但ListView在使用上会更加方便，快捷。
#### 如何让Activity窗口化
* 在AndroidManifest.xml文件当中设置当前activity的一个属性（系统自带的属性）：
android:theme="@android:style/Theme.Dialog"
* 在你的styles.xml文件中可以新建一如下的style:
<style name="Theme.FloatActivity" parent="android:style/Theme.Dialog">
<!-- float_box为我们定义的窗口背景 ，这个不是必须的-->
<item name="android:windowBackground">@drawable/float_box</item>
</style>
#### ANR是什么，怎么解决，Activity几秒，service几秒
应用程序无响应
Activity的最长执行时间是5秒，BroadcastReceiver的最长执行时间则是10秒。service20秒
#### webview和js交互（https://www.jianshu.com/p/345f4d8a5cfa）
对于Android调用JS代码的方法有2种：
* 通过WebView的loadUrl（）（方便简洁，效率低下，获取返回值麻烦；使用场景：不需要获取返回值，对性能要求较低）
* 通过WebView的evaluateJavascript（）（效率高，向下兼容性差，使用场景：Android4.4以上）

对于JS调用Android代码的方法有3种：
* 通过WebView的addJavascriptInterface（）进行对象映射（方便简洁，Android4.2一下存在漏洞，使用场景：Android4.2以上相对简单互调场景）
* 通过 WebViewClient 的shouldOverrideUrlLoading ()方法回调拦截 url（使用复杂：需要协议的约束；从Native层往Web层传递值比较繁琐，使用场景：不需要返回值情况下的互调场景）
* 通过 WebChromeClient 的onJsAlert()、onJsConfirm()、onJsPrompt（）方法回调拦截JS对话框alert()、confirm()、prompt（） 消息（使用复杂：需要协议的约束；能满足大多数情况下的互调场景）

#### Git传错文件，如何处理
* git filter-branch --tree-filter 'rm -f 文件名' HEAD把文件彻底从库中删除
* 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file
* 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
* 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，使用git reset --hard HEAD


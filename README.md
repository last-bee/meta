## 常用meta整理

## 定义与用法

* `<meta>` 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
* `<meta>` 标签位于文档的头部，不包含任何内容。
* `<meta>` 标签的属性定义了与文档相关联的名称/值对。

## 属性

属性 | 值 | 描述
----|------|----
charset | character_set  | 定义文档的字符编码。
http-equiv | content-type / expire / refresh  | 把content属性关联到HTTP头部。
name | application-name / author / description / generator / keywords  | 把 content 属性关联到一个名称。
content | text | 定义与 http-equiv 或 name 属性相关的元信息。

## meta属性分组

* **name属性与content属性**

    `name属性`用于描述网页,它是以名称/值形式的名称，name属性的值所描述的内容(值)通过content属性表示，便于搜索引擎机器人查找分类。其中最重要的是description,keywords和robots。
    
    `例如`
    ```html
    <meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
    ```

* **http-equiv属性与content属性**

    `http-equiv属性`用于提供HTTP协议的响应头报文(MIME文档头),它是以名称/值形式的名称,http-equiv属性的值所描述的内容(值)通过content属性表示，通常为网页加载前提供给浏览器等设备使用.其中最重要的是content-type charset 提供编码信息，refresh刷新与跳转页面，no-cache 页面缓存，expires网页缓存过期时间。
    
    `例如`    
    ```html
    <meta http-equiv="content-type" content="text/html; charset=ISO-8859-1">
    ```

---

#### HTML 4.01 与 HTML 5 之间的差异
1. 在 HTML 5 中，不再支持 scheme 属性。
2. 在 HTML 5 中，有一个新的 charset 属性，它使字符集的定义更加容易。
3. 在 HTML 4.01 中，不得不这么写：

```html
<meta http-equiv="content-type" content="text/html; charset=ISO-8859-1">
```
在 HTML 5 中，这样就够了：
```html
<meta charset="ISO-8859-1">
```

## 下面以相关性分别介绍用法：

### 网页相关

* **编码格式**


```html
<meta charset='utf-8' />
```

* **优先使用 IE 最新版本和 Chrome：** X-UA-Compatible是自从IE8新加的一个设置，对于IE8以下的浏览器是不识别的。 通过在meta中设置X-UA-Compatible的值，可以指定网页的兼容性模式设置。

```html
<meta http-equiv="X-UA-Compatible" content="IE=7">  
<!--以上代码告诉IE浏览器，无论是否用DTD声明文档标准，IE8/9都会以IE7引擎来渲染页面。  -->
<meta http-equiv="X-UA-Compatible" content="IE=8">  
<!--以上代码告诉IE浏览器，IE8/9都会以IE8引擎来渲染页面。 --> 
<meta http-equiv="X-UA-Compatible" content="IE=edge">  
<!--以上代码告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面。-->  
<meta http-equiv="X-UA-Compatible" content="IE=7,IE=9">  
<meta http-equiv="X-UA-Compatible" content="IE=7,9">  
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
<!--以上代码IE=edge告诉IE使用最新的引擎渲染网页，chrome=1则可以激活Chrome Frame.-->
```
`Chrome Frame 介绍：`
Google Chrome Frame是Google推出的一款免费的Internet Explorer专用插件。使用此插件，用户可以通过Internet Explorer的用户界面，以Chrome内核的渲染方式浏览网页。[Google Chrome Frame百科](http://baike.baidu.com/view/2831140.htm)

* **浏览器内核控制：** renderer是为双核浏览器准备的，用于指定双核浏览器默认以何种方式渲染页面,国内浏览器很多都是双内核（webkit和Trident），webkit内核高速浏览，IE内核兼容网页和旧版网站。而添加meta标签的网站可以控制浏览器首先选择何种内核进行渲染

    * 若页面需默认用极速核，增加标签：
    ```html
    <meta name="renderer" content="webkit">
    ```
    * 若页面需默认用ie兼容内核，增加标签：
    ```hmtl
    <meta name="renderer" content="ie-comp">
    ```
    * 若页面需默认用ie标准内核，增加标签：
    ```html
    <meta name="renderer" content="ie-stand">
    ```
    * 同时我们也可以同时指定多个内核名称，之间以符号”|”进行分隔,此时浏览器将会按照从左到右的先后顺序选择其具备的渲染内核来处理当前网页。
    ```html
    <meta name="renderer" content="webkit|ie-comp|ie-stand">
    ```

    * 规定360安全浏览器使用webki内核进行渲染
    
    ```html
    <meta name="renderer" content="webkit">
    ```

* **禁止浏览器从本地计算机的缓存中访问页面内容：** 不缓存页面(为了提高速度，一些浏览器会缓存浏览者浏览过的页面，通过下面的定义，浏览器一般不会缓存页面,而且浏览器无法脱机浏览。)

```html
<meta http-equiv="Pragma" content="no-cache">
```

* **设置http cache时间:** 在快速迭代的项目中，我们可以设置max-age=604800s，也就是七天

```html
<meta http-equiv="Cache-Control" content="max-age=604800" />
```


* **申明网站为pc站，避免被转码：** 

```html
<meta name="applicable-device" content="pc">
```

* **转码申明：** 用百度打开网页可能会对其进行转码，避免转码可添加如下meta

```html
<meta http-equiv="Cache-Control" content="no-siteapp" />
```



### SEO优化

* **页面关键词：** 每个网页应具有描述该网页内容的一组唯一的关键字。
使用人们可能会搜索，并准确描述网页上所提供信息的描述性和代表性关键字及短语。标记内容太短，则搜索引擎可能不会认为这些内容相关。另外标记不应超过 874 个字符。

```html
<meta name="keywords" content="your tags" />
```

* **页面描述：** 每个网页都应有一个不超过 150 个字符且能准确反映网页内容的描述标签。

```html
<meta name="description" content="150 words" />
```

* **搜索引擎索引方式：** robotterms是一组使用逗号(,)分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。确保正确使用nofollow和noindex属性值。

```html
<meta name="robots" content="index,follow" />
<!--
    all：文件将被检索，且页面上的链接可以被查询；
    none：文件将不被检索，且页面上的链接不可以被查询；
    index：文件将被检索；
    follow：页面上的链接可以被查询；
    noindex：文件将不被检索；
    nofollow：页面上的链接不可以被查询。
 -->
```

* **页面重定向和刷新：** content内的数字代表时间（秒），既多少时间后刷新。如果加url,则会重定向到指定网页（搜索引擎能够自动检测，也很容易被引擎视作误导而受到惩罚）。

```html
<meta http-equiv="refresh" content="0;url=" />
```

* **搜索引擎爬虫重访时间：** 如果页面不是经常更新，为了减轻搜索引擎爬虫对服务器带来的压力，可以设置一个爬虫的重访时间。如果重访时间过短，爬虫将按它们定义的默认时间来访问。

```html
<meta name="revisit-after" content="7 days" >
```
* **使用 Referer Meta 标签控制referer：** html 文档可以控制 http 请求中的 referer ，比如是否发送 referer、只发送 hostname 还是发送完整的 referer 等。
```html
<meta name="referrer" content="never,default,origin,always">
<!--
1.如果 referer-policy 的值为never：删除 http head 中的 referer；
2.如果 referer-policy 的值为default：如果当前页面使用的是 https 协议，而正要加载的资源使用的是普通的 http 协议，则将 http header 中的 referer 置为空；
3.如果 referer-policy 的值为 origin：只发送 origin 部分；
4.如果 referer-policy 的值为 always：不改变http header 中的 referer 的值，注意：这种情况下，如果当前页面使用了 https 协议，而要加载的资源使用的是 http 协议，加载资源的请求头中也会携带 referer。
-->
```
* **其他**

```html
<meta name="author" content="author name" /> <!-- 定义网页作者 -->
<meta name="copyright" content="lyl"> <!-- 定义网站版权 -->
<meta name="generator" content="Sublime Text3"> <!-- 定义网站制作软件 -->
```

### 移动设备

* **viewport：** 能优化移动浏览器的显示。如果不是响应式网站，不要使用initial-scale或者禁用缩放。
大部分4.7-5寸设备的viewport宽设为360px；5.5寸设备设为400px；iphone6设为375px；ipone6 plus设为414px。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
<!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边  -->
```

1. width：宽度（数值 / device-width）（范围从200到10,000，默认为980 像素）
1. height：高度（数值 / device-height）（范围从223 到10,000）
1. initial-scale：初始的缩放比例 （范围从>0 到10）
1. minimum-scale：允许用户缩放到的最小比例
1. maximum-scale：允许用户缩放到的最大比例
1. user-scalable：用户是否可以手动缩 (no,yes)
1. minimal-ui：可以在页面加载时最小化上下状态栏。（已弃用）

`注意` 很多人使用initial-scale=1到非响应式网站上，这会让网站以100%宽度渲染，用户需要手动移动页面或者缩放。如果和initial-scale=1同时使用user-scalable=no或maximum-scale=1，则用户将不能放大/缩小网页来看到全部的内容。

* **WebApp全屏模式：** 伪装app，离线应用。

```html
<meta name="apple-mobile-web-app-capable" content="yes" /> <!-- 启用 WebApp 全屏模式 -->
```

* **隐藏状态栏/设置状态栏颜色：** 只有在开启WebApp全屏模式时才生效。content的值为default | black | black-translucent 。

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
```

* **添加到主屏后的标题**

```html
<meta name="apple-mobile-web-app-title" content="标题">
```
![view](https://cloud.githubusercontent.com/assets/3378002/15988534/3b48533e-3087-11e6-9f74-f2c8721c15e0.png)

* **忽略数字自动识别为电话号码**

```html
<meta name="format-detection" content="telephone=no" /> 
```

* **忽略识别邮箱**

```html
<meta name="format-detection" content="email=no" />
```

* **添加智能 App 广告条 Smart App Banner：** 告诉浏览器这个网站对应的app，并在页面上显示下载banner(如下图)。

```html
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL"> 
```
![view1](https://cloud.githubusercontent.com/assets/3378002/15988549/d90954ec-3087-11e6-8efb-a1447e01a167.png)

* **IOS相关**

```html
<meta name="apple-mobile-web-app-title" content="标题">
<!-- 添加到主屏后的标题（iOS 6 新增） -->
<meta name="apple-mobile-web-app-capable" content="yes"/>
<!-- 是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏 --> 
<meta name="apple-itunes-app" content="app-id=myAppStoreID,
    affiliate-data=myAffiliateData, app-argument=myURL">
<!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
<meta name="apple-mobile-web-app-status-bar-style" content="black"/>
<!-- 设置苹果工具栏颜色 -->
```

* **其他**

```html
<!-- 不让百度转码 -->
<meta http-equiv="Cache-Control" content="no-siteapp" />
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
```

```html
<meta name="msapplication-TileColor" content="#000"/>
<!-- Windows 8 磁贴颜色 -->
<meta name="msapplication-TileImage" content="icon.png"/>
<!-- Windows 8 磁贴图标 -->


<!-- sns 社交标签 begin -->
<!-- 参考微博API -->
<meta property="og:type" content="类型" />
<meta property="og:url" content="URL地址" />
<meta property="og:title" content="标题" />
<meta property="og:image" content="图片" />
<meta property="og:description" content="描述" />
<!-- sns 社交标签 end -->
```

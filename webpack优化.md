前段时间，项目基本上做完了需要上线，我build了一下，发现打包后的有些文件后面提示big，文件很大。做完了，就要去优化，用了几天，效果很不错，一些方法如下：

1.将一些第三方工具和包不再用npm模块引入，改用cdn引入
![image](https://github.com/liulinqiang121/myblog/image/1.png)
            图1
这里讲要用cdn引入的模块名放在externals里面，防止将某些 包(package)打包到 bundle 中，然后像：import vue from 'vue'这些引入可以去掉。
![](https://upload-images.jianshu.io/upload_images/13382831-27ceae159fb20521.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

             图2
这里讲要用cdn引入的资源放在html里用script标签引入，上面的例子就可以引用了element,vue-router,moment,echarts的静态资源。这一步应该就能将生成的第三方模块打包成的vendor.js减小很多

2 特别突出的echarts

![](https://upload-images.jianshu.io/upload_images/13382831-d53d1d85f8a8a09c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


             图3
项目中引用了echarts，结果图3打包后的vendor-async竟然达到了将近800k,好怕怕啊。

![](https://upload-images.jianshu.io/upload_images/13382831-c481cf655989b5bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
             图4
用webpack分析工具webpack-bundle-analyzer，发现echarts特别大之后，将echarts用静态资源引入。但是，有出现问题，因为项目中使用了中国地图，所以china.js引入不了，之后经这个文件也用静态进入，参考图2，这才能够出现地图。


![](https://upload-images.jianshu.io/upload_images/13382831-0af75583e523c418.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

             图5
结果，发现这个文件由170多k直接到6k,^_^。

3  将js,css压缩成zip文件



![](https://upload-images.jianshu.io/upload_images/13382831-4527f033e82bb852.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
             图6
这里我将vue-cli中设置的productionGzip设置为true,打包的js，css文件可以同时生成的压缩zip文件。如果浏览器支持，就会直接下载zip文件


![](https://upload-images.jianshu.io/upload_images/13382831-638bf38974c2e75c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

            图7  未压缩打包后的大小

![](https://upload-images.jianshu.io/upload_images/13382831-272f334633bfcc89.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

            图8 打包后的zip文件
这少了三分之一的样子，我本地浏览器用的就是zip文件



![](https://upload-images.jianshu.io/upload_images/13382831-880ef690d4b5fa62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

                图9

4 将vender.js切割



![](https://upload-images.jianshu.io/upload_images/13382831-89234a15f2c40b87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

                图10
如果最后第三方模块打包生成的vendor.js过大，可以将其切割成多个文件。




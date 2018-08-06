从今天起，简单看下webpack的源码。
webpack打包是从node_modules/.bin/webpack.cmd这个位置开始的，简单看下这个文件：
源码是这样的：
@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\..\webpack\bin\webpack.js" %*
) ELSE (
  @SETLOCAL
  @SET PATHEXT=%PATHEXT:;.JS;=;%
  node  "%~dp0\..\webpack\bin\webpack.js" %*
)
%~dp 代表的是当前位置，%接受的是指令后面带的参数，
上面基本的意思是 当前文件下如果有node.exe这个文件，就执行node_module下webpack模块下/bin/webpack.js这个文件，否则就执行系统默认的文件，还是会执行webpack模块下/bin/webpack.js这个文件。所以这个文件是webpack的启动文件

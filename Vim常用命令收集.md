# Vim常用命令



### 删除

x    		删除光标下的字符 ("dl" 的缩写)
X    		删除光标前的字符 ("dh" 的缩写)
D    		从当前位置删除到行尾 ("d$" 的缩写)
dw   	从当前位置删除到下一个单词开头
db    	从当前位置删除到前一个单词的开头
diw    	删除光标上的单词 (不包括空白字符)
daw    	删除光标上的单词 (包括空白字符)
dG    	删除到文件末
dgg    	删除到文件首
dl  		删除字符 (缩写: "x")         

diW    	删除内含字串 (见 |WORD|)      

daW    	删除一个字串 (见 |WORD|)      

dd    	删除一行               

dis    	删除内含句子           

das    	删除一个句子            

dib    	删除内含 '(' ')' 块           

dab    	删除一个 '(' ')' 块          

dip    	删除内含段落               

dap    	删除一个段落                

diB    	删除内含 '{ ' ' }' 大块            

daB    	删除一个 '{ ' ' }' 大块           



|CTRL-E|        N  CTRL-E       window N lines downwards (default: 1)  窗口向下移动一行（文本是反方向，向下一行）
|CTRL-D|        N  CTRL-D       window N lines D ownwards (default: 1/2 window) 窗口向下移动半屏（文本向上）
|CTRL-F|        N  CTRL-F       window N pages F orwards (downwards) 窗口向下移动一屏（文本上向上）下同
|CTRL-Y|        N  CTRL-Y       window N lines upwards (default: 1)
|CTRL-U|        N  CTRL-U       window N lines U pwards (default: 1/2 window)
|CTRL-B|        N  CTRL-B       window N pages B ackwards (upwards)
|z<CR>|        z<CR> or zt    redraw, current line at t op of window   把当前行搞到顶上去
|z.|                z.    or zz         redraw, current line at center of window 把当前行搞到屏幕中间去
|z-|                z-    or zb        redraw, current line at b ottom of window 把当前行搞到屏幕底部去

These only work when 'wrap' is off:（当某些行特长，超过一个屏幕的宽度时使用）
|zh|              N  zh                scroll screen N characters to the right
|zl|               N  zl                 scroll screen N characters to the left
|zH|              N  zH               scroll screen half a screenwidth to the right
|zL|              N  zL                scroll screen half a screenwidth to the left
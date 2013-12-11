


从chrome的[webstore](https://chrome.google.com/webstore/detail/markdown-preview-plus/febilkbfcbhebfnokafefeacimjdckgl)安装Markdown Preview Plus插件
打开chrome://extensions/，在设置页中勾选 “允许访问文件网址”
在chrome中打开本地markdown文件，http/https也是可以支持的
你会看到已经转换成html的内容
在chrome中打开markdown文件，用vim编辑markdown，保存后页面就会自动刷新，实现预览。虽然不像一些工具一样是实时的，但是保存后再预览，这样我觉得也挺好。再在vimrc中加入以下内容：
1
autocmd BufRead,BufNewFile *.{md,mdown,mkd,mkdn,markdown,mdwn} map <Leader>p :!start "C:\Program Files\Google\Chrome\Application\chrome.exe" "%:p"<CR>
以后，需要预览时再\p打开浏览器预览。

[ref](http://howiefh.github.io/2013/05/16/vim-markdown-preview/)

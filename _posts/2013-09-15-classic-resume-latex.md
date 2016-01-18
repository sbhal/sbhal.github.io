---
layout: post
title: Classic Resume using LATEX
---

This is a guide to make your classic resume using LATEX typesetting engine.
Checkout the my [Resume](https://dl.dropboxusercontent.com/u/18904197/Blogger/resume_1.pdf) first!

Platform: Windows 7, 64bit
PDF viewer: SumatraPDF

IMP: Please add path to SumatraPDF in your Environment PATH variable. In my case I added ';C:\Program Files\SumatraPDF' to my windows PATH variable. Check [this](http://geekswithblogs.net/renso/archive/2009/10/21/how-to-set-the-windows-path-in-windows-7.aspx) for little demo.
Install Fontin font which can be downloaded for free from here: http://www.exljbris.com/fontin.html

1. I used [vim-latex](http://vim-latex.sourceforge.net/) for being a big fan of VIM. But for your convenience, you can go for  [MiKtex](http://miktex.org/) for windows.
2. Made the following changes in my ~/_vimrc(for windows)/ ~/.vimrc(other platforms)
	* let g:tex_flavor='xelatex'
	* let g:Tex_DefaultTargetFormat = 'pdf'
	* let g:Tex_CompileRule_pdf = 'xelatex -interaction=nonstopmode $*'
	* let g:Tex_ViewRule_pdf = 'SumatraPDF -reuse-instance'
3. Download the *.tex file from [here](https://dl.dropboxusercontent.com/u/18904197/Blogger/resume_1.tex) .
Source of Template: http://www.LaTeXTemplates.com 
4. Compile the *.tex file using xelatex only.
	* Vim Binding for vim-latex plugin are as follows: (assuming leader key is '\')
	* \ll - compiling
	* \lv - open the compiled file (in our case, a pdf file)
5. Make any modifications required to the file and recompile to get changes reflected.
Hope this helps. Please drop by your comments!

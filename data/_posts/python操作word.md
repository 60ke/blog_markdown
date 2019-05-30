---
title: python操作word
date: 2018-02-26 09:21:51
categories: default
tags: []
urlname: 76
---
使用python-docx生成Word文档
---------------------
首先安装python-docx：

`pip  install python-docx`

例子：

    from  docx import  Document
    from  docx.shared import  Pt
    from  docx.oxml.ns import  qn
    from docx.shared import Inches
    
    #打开文档
    document = Document()
    
    #加入不同等级的标题
    document.add_heading('Document Title',0)
    document.add_heading(u'二级标题',1)
    document.add_heading(u'二级标题',2)
    
    #添加文本
    paragraph = document.add_paragraph(u'添加了文本')
    #设置字号
    run = paragraph.add_run(u'设置字号')
    run.font.size=Pt(24)
    
    #设置字体
    run = paragraph.add_run('Set Font,')
    run.font.name='Consolas'
    
    #设置中文字体
    run = paragraph.add_run(u'设置中文字体，')
    run.font.name=u'宋体'
    r = run._element
    r.rPr.rFonts.set(qn('w:eastAsia'), u'宋体')
    
    #设置斜体
    run = paragraph.add_run(u'斜体、')
    run.italic = True
    
    #设置粗体
    run = paragraph.add_run(u'粗体').bold = True
    
    #增加引用
    document.add_paragraph('Intense quote', style='Intense Quote')
    
    #增加有序列表
    document.add_paragraph(
        u'有序列表元素1',style='List Number'
    )
    document.add_paragraph(
        u'有序列别元素2',style='List Number'
    )
    
    #增加无序列表
    document.add_paragraph(
        u'无序列表元素1',style='List Bullet'
    )
    document.add_paragraph(
        u'无序列表元素2',style='List Bullet'
    )
    
    #增加图片（此处使用相对位置）
    document.add_picture('jdb.jpg',width=Inches(1.25))
    
    #增加表格
    table = document.add_table(rows=3,cols=3)
    hdr_cells=table.rows[0].cells
    hdr_cells[0].text="第一列"
    hdr_cells[1].text="第二列"
    hdr_cells[2].text="第三列"
    
    hdr_cells = table.rows[1].cells
    hdr_cells[0].text = '2'
    hdr_cells[1].text = 'aerszvfdgx'
    hdr_cells[2].text = 'abdzfgxfdf'
    
    hdr_cells = table.rows[2].cells
    hdr_cells[0].text = '3'
    hdr_cells[1].text = 'cafdwvaef'
    hdr_cells[2].text = 'aabs zfgf'
    
    #增加分页
    document.add_page_break()
    
    #保存文件
    document.save('demo.docx')
效果：

![](http://ww1.sinaimg.cn/large/006Gd5nOly1fotytxlec8j30jm0fg3z2.jpg)
打开及保存文件：

    from docx import Document  
    document = Document('test.docx')  
    document.save('test.docx') 

 

添加文本：

    document.add_paragraph('test text')


调整文本位置格式为居中：

    from docx import Document  
    from docx.enum.text import WD_ALIGN_PARAGRAPH  
    document = Document('test.docx')  
    paragraph = document.add_paragraph('123')  
      
    paragraph.paragraph_format.alignment = WD_ALIGN_PARAGRAPH.CENTER  
    document.save('test.docx')  

调整左缩进0.3英寸：

    document = Document('test.docx')  
    paragraph = document.add_paragraph('this is test for left_indent with inches')  
    paragraph_format = paragraph.paragraph_format  
    paragraph_format.left_indent = Inches(0.3)  
    document.save('test.docx')  

首行缩进：

    paragraph_format.first_line_indent = Inches(0.3) 


上行间距：

    paragraph_format.space_before = Pt(18)  

下行间距：

    paragraph_format.space_after = Pt(12) 

行距：

    paragraph_format.line_spacing = Pt(18)  

分页格式：
紧跟上段：

    paragraph_format.keep_together 

 
若本页无法完全显示，另起一页：

    paragraph_format.keep_with_next  

强制另起一页：
    paragraph_format.page_break_before  

字体格式：

    <pre name="code" class="python">p = document.add_paragraph()  
    run = p.add_run('test typeface')  
    #加粗  
    run.font.bold = True  
    #斜体  
    run.font.italic = True  
    #下划线  
    run.font.underline = True  
    WD_UNDERLINE 中有所有下划线格式

调用样例：

    run.underline = WD_UNDERLINE.DOT_DASH  


字体颜色：

    from docx.shared import RGBColor  
    test = document.add_paragraph().add_run('color')  
    font = test.font  
    font.color.rgb = RGBColor(0x42, 0x24 , 0xE9)  

调用预设颜色：

    from docx.enum.dml import MSO_THEME_COLOR  
    font.color.theme_color = MSO_THEME_COLOR.ACCENT_1  
参考连接：
http://blog.csdn.net/u011932355/article/details/51769803
https://www.jianshu.com/p/1f60cdd9655a

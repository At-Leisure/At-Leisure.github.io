---
layout:       post
title:        "导出具备原始视觉效果地HTML版Jupyter"
author:       "周(๑•̌.•๑)"
catalog:      true
tags:
  - Python
---

> 直接导出地html没有任何格式，不和原版一样居中和边缘阴影效果，但是可以通过修改html代码，调整body的css样式来达成目的


1. 通过命令行将 jupyter 转化为 html。

    ```shell
    jupyter nbconvert --to html xxx.ipynb
    #jupyter nbconvert --to html --no-input xxx.ipynb
    ```

    如果不加上–no-input，会默认在当前路径下生成一个含有代码块部分内容的xxx.html文件；加上–no-input参数，就会将notebook中的代码块隐藏，只显示代码块的运行结果及notebook中类型为markdown的cell。


2. 调整body的css样式

    ```css
    body{
      width: 75%;         /*宽度为75%*/
      margin-left: auto;  /*边缘自适应居中*/
      margin-right: auto; /*边缘自适应居中*/
      border-radius: 5px; /*圆角效果*/
      box-shadow: 0 0 15px 10px #e9e9e9;  /*边缘阴影效果*/
    }
    ```

3. Python一键转换

      ```python
      import subprocess


      def jupyter2html(path: str, *, modify=True):
          fn = path.rsplit('.', 1)[0]
          p = subprocess.run(f'jupyter nbconvert --to html "{fn}.ipynb"')  # 阻塞式运行

          if modify:
              with open(f'{fn}.html', 'r', encoding='utf-8') as f:
                  text = f.read()
              with open(f'{fn}.html', 'w', encoding='utf-8') as f:
                  f.write(text.replace(
                      '<body',
                      '''<body style="width: 75%; /*宽度为75%*/
                          margin-left: auto;  /*边缘自适应居中*/
                          margin-right: auto; /*边缘自适应居中*/
                          border-radius: 5px; /*圆角效果*/
                          /*边缘阴影效果*/
                          box-shadow: 0 0 15px 10px #e9e9e9;  "
                      '''))
          NormalCode = 0
          return p.returncode == NormalCode
      ```
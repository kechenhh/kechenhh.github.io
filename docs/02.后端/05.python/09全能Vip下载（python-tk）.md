---
title: 09全能Vip下载（python-tk）
date: 2021-07-27 09:26:22
permalink: /pages/c2d1fa/
categories:
  - 后端
  - python
tags:
  - 

---

```python
# -*- coding: UTF-8 -*-
import requests
from lxml import etree
from tkinter import *
import tkinter as tk
 
headers = {'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36'}
# 创建窗口
window = tk.Tk()
window.title("VIPdownload--v1.0")
window.geometry('800x700')
 
# 定义触发事件时的函数（注意：因为Python的执行顺序是从上往下，所以函数一定要放在按钮的上面）
def get_one():
    name = e1.get()
    url = 'http://so.qnvod.net:55555/'
    data = {
        'keyword':name,
        'searchtype':'vodsearch',
        'keytype':1}
 
    res = requests.post(url, headers=headers, data=data)
    res.encoding = res.apparent_encoding
    html = res.text
    res_xpath = etree.HTML(html)
    url_lists = res_xpath.xpath('//div[@class="lit"]/dl')
    for li in url_lists:
        title_list = li.xpath('./dd/a/text()')[0]
        url_list = li.xpath('./dd/a/@href')[0]
        t1.insert('insert', title_list+':'+ url_list + '\n')  # 文本框，光标位置插入文字
 
def get_two():
    var_url = e2.get()  # 得到输入框中数据
 
    response = requests.get(var_url, headers=headers)
    response.encoding = response.apparent_encoding
    html = response.text
 
    res_xpath = etree.HTML(html)
    url_lists = res_xpath.xpath('//ul[@class="textdown"]/li')
    for li in url_lists:
        url_list = li.xpath('./dt/a/@onclick')[0]
        url_out = url_list[13:-2]
        t2.insert('insert', url_out+'\n')  # 文本框，光标位置插入文字
# 清除
def clear():
    t1.delete('1.0', 'end')
    t2.delete('1.0', 'end')
 
 
#搜索1
l1 = tk.Label(window,
              text='输入要搜索的资源：',
              font=('Arial', 12),
              width=18,
              height=2)
l1.place(x=1,y=10)
 
# 创建输入框entry
e1 = tk.Entry(window, width=50,background='#d3fbfb')
e1.place(x=150,y=25)
 
b1 = tk.Button(
    window,
    text='搜索',
    width=10,
    command=get_one)
b1.place(x=520,y=22)
 
b11 = tk.Button(
    window,
    text='全部清除',
    width=10,
    command=clear)
b11.place(x=620,y=22)
 
#搜索2
l2 = tk.Label(window,
              text='输入URL:',
              font=('Arial', 12),
              width=20,
              height=2)
l2.place(x=10,y=50)
 
# 创建输入框entry
e2 = tk.Entry(window, width=50,background='#d3fbfb')
e2.place(x=150,y=60)
 
b2 = tk.Button(
    window,
    text='采集',
    width=10,
    command=get_two)
b2.place(x=520,y=60)
 
 
# 创建一个文本框用于显示1
t1 = tk.Text(window,font=16,height=6,background='#D3D3D3')
t1.place(x=80,y=100)
 
# 创建一个文本框用于显示2
t2 = tk.Text(window,font=16,background='#D3D3D3')
t2.place(x=80,y=220)
window.mainloop()
 
 

```

![QQ截图20191223161546](https://ke-pic.oss-cn-beijing.aliyuncs.com//img/QQ截图20191223161546.png)


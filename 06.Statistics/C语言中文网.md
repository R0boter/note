## 爬取教程制作PDF

```python
#!/usr/bin/env python3
# coding=utf-8
import requests
import pdfkit
import re
from bs4 import BeautifulSoup
from PyPDF2 import PdfFileMerger

html_template = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
</head>
<body>
{content}
</body>
</html>
"""
def get_number():
    url = "http://c.biancheng.net/asm/10/"
    html = requests.get(url)
    soup = BeautifulSoup(html.content,"html.parser")
    tetle = soup.find_all('span',class_="channel-num")
    
#    html=requests.get(url+str(i))
#    soup=BeautifulSoup(html.content,'html.parser')  # 格式化请求到的网页
#    title=soup.find('dd',class_="this")             # 获取大章节名称的标签
#    text=soup.find('dl',class_="dl-sub")            # 获取小章节名称的标签
#    title1=title.find('span').string+'.'+title.find('a').string     # 获取大章节名称
#
#    j = 0
#    while j < len(text):                            # 获取小章节的名称
#        text1=text.find_all('a')[j].string
#        j += 1
#
#    i += 10

website="http://c.biancheng.net"
starturl = "http://c.biancheng.net/asm/10"
bookhtml = requests.get(starturl)
i=0
while i < 237:
    booksoup = BeautifulSoup(bookhtml.content,'html.parser')
    title = booksoup.find('div',id="article").find('h1').get_text()
    text = booksoup.find('div',id="arc-body")
    
    center_tag =booksoup.new_tag("center")
    title_tag = booksoup.new_tag("h1")
    title_tag.string = title
    center_tag.insert(1,title_tag)
    text.insert(1,center_tag)
    html = str(text)
    # body中的img标签的src相对路径的改成绝对路径
    pattern = "(<img .*?src=\")(.*?)(\")"
    def func(m):
      if not m.group(3).startswith("http"):
        rtn = m.group(1) + website + m.group(2) + m.group(3)
        return rtn
      else:
        return m.group(1)+m.group(2)+m.group(3)
    html = re.compile(pattern).sub(func, html)

    html = html_template.format(content=html)
    html = html.encode("utf-8")
    with open(str(i)+".html",'wb') as f:
        f.write(html)


    nextone=booksoup.find('span',class_="next")         # 获取下一页地址的标签
    nexturl=nextone.find('a')['href']               # 获取下一页的地址
    bookhtml= requests.get(website+str(nexturl))
    print(title)
    i += 1


options = {
  'page-size': 'Letter',
  'margin-top': '0.75in',
  'margin-right': '0.75in',
  'margin-bottom': '0.75in',
  'margin-left': '0.75in',
  'encoding': "UTF-8",
  'custom-header': [
    ('Accept-Encoding', 'gzip')
  ],
  'cookie': [
    ('cookie-name1', 'cookie-value1'),
    ('cookie-name2', 'cookie-value2'),
  ],
  'outline-depth': 10,
}

pdfs = []
for j in range(0,236):
    pdfs.append('Compilation'+str(j)+'.pdf')
    pdfkit.from_file(str(j)+'.html','Compilation'+str(j)+'.pdf')

merger = PdfFileMerger()
for pdf in pdfs:
    merger.append(open(pdf,'rb'))

output = open(u"Compilation.pdf","wb")
merger.write(output)

```


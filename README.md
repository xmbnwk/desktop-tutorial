#coding=gb2312

import bs4
import json
from http.client import responses
import requests
import re
from bs4 import BeautifulSoup
import csv
import time
import xlwt

head={
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.42"
}
for page in range(0,100):
  url="https://club.jd.com/comment/productPageComments.action?&productId=100019125569&score=0&sortType=5&page={}&pageSize=10&isShadowSku=0&fold=1".format(page)
  html=requests.get(url,headers=head)
  result=html.json()
  comment=result["comments"]
  for element in comment:
    name=element["nickname"]
    content=element["content"]
    product_time=element["creationTime"]
    print(name)
    print(content)
    print(product_time)
    print("\n")
  time.sleep(5)


newTable='test.xls'
wb=xlwt.Workbook("encoding='utf-8")

ws=wb.add_sheet("sheet1")
headData=['id','评价','时间']
for i in range(0,3):
    ws.write(0,i,headData[i])
index=1
for results in comment:
    for i in range(0,3):
        print(result[i])
        ws.write(index,i,result[i])
        index+=1
        wb.save(newTable)

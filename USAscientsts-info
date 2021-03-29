#!usr/bin/env python3.7
#-*- coding:utf-8 -*-

__author__ = 'shenlingyun'

import time
import requests
from bs4 import BeautifulSoup
import bs4
import re

def getHtml(url):
    try:
        r = requests.get(url)
        r.raise_for_status()
        html = r.text  # 获取request访问到的页面
        soup = BeautifulSoup(html, "html.parser")  # 用beautifulsoup解析HTML，使HTML格式化
        info= soup.find('div',attrs= {'id':'contact_info'})
        name_origin = info.find('h2')          #["\r\n          G. \r\n          \r\n          't Hooft\r\n          \r\n        "]
        for t in name_origin.contents:
            namesp1 = re.sub(r'\r\n', ' ', t)  # r表示不需要处理反斜杠
            namesp2 = namesp1.split() # 去掉空格
            #print(namesp2)

        detail = info.find('td')      #\r 回车不换行
        #print(detail)
        year = detail.contents[2]
        do=detail.contents[3]
        # < br ><span class ="secondary_section" style="font-weight:bold;" > Primary Section:</ span > 13, Physics < br / >
        # < span style = "font-weight:bold;" > Membership Type: < / span > International Member < br / >
        # < / br >
        do1 =do.contents
        do2=do1[2]
        do3 = re.sub(r'[\d,]', '', do2).replace(' ', '')

        #print(namesp2+"\t"+do3+"\t"+year+"\t"+url)
        # i=1
        # for h in detail.contents:
        #     print(str(i)+":")
        #     print(h)
        #     i=i+1
        #
        with open('Americanlist-list2.txt', 'a') as f:
            f.write(namesp2+"\t"+do3+"\t"+year+"\t"+url+"\n")

                #名字、领域、当选年份、介绍文字、网址

        f.close()

    except:
        return "faild"


def main():

    file = open('Americanlist-personweb.txt','r', encoding='utf-8')  # r是读， w是写，  a是追加
    i=1
    for line in file:

        url = re.sub(r'\n','',line)
        getHtml(url)
        #if i % 50 == 0:
        print("page_num to"+str(i))
        i = i + 1
    file.close()

    # url="http://www.nasonline.org/member-directory/members/2540456.html"
    # getHtml(url)

main()

---
layout: post
title:  "selenium识别验证码登录"
date:   2020-07-29 11:01:02
categories: software
tags: selenium,python
excerpt: 本文主要讲述自动化登录中识别二维码登录情况，两种方式。
---
* content
{:toc}


###实现思路一 

1.打开页面后将整个登录页面截图

2.定位验证码坐标位置

3.打开截图图片使用pillow库截取验证码图片

4.调用百度ocr通用文字识别

5.返回结果中提取二维码文字


```
# -*- coding: utf-8 -*-
# @Time     : 2020/7/23 21:00
# @Author   : iTreeNewBee
# @File     : 图形验证码.py
# @Project  : py

from selenium import webdriver
import time
from PIL import Image
import requests
import base64
import tkinter as tk


def get_CodeImg(url):
    root = tk.Tk()# 获取电脑屏幕大小
    screen_w = root.winfo_screenwidth()
    screen_h = root.winfo_screenheight()
    root.destroy()
    browser = webdriver.Chrome()
    browser.maximize_window()
    browser.implicitly_wait(10)
    browser.get(url)
    browser.save_screenshot('/Users/itreenewbee/Downloads/image/pic.png')
    browser.find_element_by_name('name').send_keys('fanglin')
    browser.find_element_by_name('pwd').send_keys('1qaz!QAZ')
    # code_ele = browser.find_element_by_xpath('/html/body/div/div/div[2]/div/div/form/p[4]/img')
    code_ele = browser.find_element_by_id('code_img')
    # 获取验证码图片坐标
    left = code_ele.location['x']
    top = code_ele.location['y']
    right = code_ele.size['width']
    down = code_ele.size['height']
    image = Image.open('/Users/itreenewbee/Downloads/image/pic.png')
    image_w = image.size[0]
    image_h = image.size[1]
    # 图片与屏幕比例
    multiple_w = image_w/screen_w
    multiple_h = image_h/screen_h
    img_left = left * multiple_w
    img_top = top * multiple_h + 150
    img_right = right * multiple_w +img_left
    img_down = down * multiple_h + img_top + 70
    code_image = image.crop((img_left, img_top, img_right, img_down))
    imgUrl = code_image.save('/Users/itreenewbee/Downloads/image/code.png')
    token = get_token()
    code = get_code(token)
    time.sleep(4)
    browser.find_element_by_xpath('//*[@id="codeInput"]').send_keys(code)
    time.sleep(4)
    browser.find_element_by_id('submit_btn').click()
    time.sleep(1000)



def get_token():
    # client_id 为官网获取的AK， client_secret 为官网获取的SK
    host = 'https://aip.baidubce.com/oauth/2.0/token?grant_type=client_credentials&client_id=P4NCHeK3wlhm3XcOdSxZB9be&client_secret=CxeyyyNPI4GIOp2yBAs2Vp3nbMSVEcYW'
    response = requests.get(host)
    access_token = response.json()['access_token']
    return access_token

def get_code(token):
    '''
    通用文字识别（高精度版）
    '''
    request_url = "https://aip.baidubce.com/rest/2.0/ocr/v1/accurate_basic"
    # 二进制方式打开图片文件
    f = open('/Users/itreenewbee/Downloads/image/code.png', 'rb')
    img = base64.b64encode(f.read())

    params = {"image": img}
    access_token = token
    request_url = request_url + "?access_token=" + access_token
    headers = {'content-type': 'application/x-www-form-urlencoded'}
    response = requests.post(request_url, data=params, headers=headers)
    # print(response.json()['words_result'])
    if response.json()['words_result']:
        words_result = response.json()['words_result'][0]['words']
        #去掉空格
        code = str(words_result).replace(' ', '')
        f.close()
        if len(code) == 4:
            return code
        else:
            get_code(token)
    else:
        get_code(token)


if __name__ == '__main__':
    global CODE
    url = 'http://1.1.1.1/#/'
    imgUrl = get_CodeImg(url)
```


ps:这种方式实现有一定局限性，首先坐标定位需要根据自己实际情况调整，不能精准定位到；其次百度到ocr识别效率没有那么高，登录成功几率50%吧。推荐看下第二种方式，100%登录成功，且更简单。 



###实现思路二  

1.定位到验证码图片，获取属性拿到图片css地址  

2.下载图片

3.循环调用ocr识别库识别验证码直到登录成功  

4.OCR识别服务使用的华为OCR-SDK，可下载文档查看SK、AK如何获取 


```
# -*- coding: utf-8 -*-
# @Time     : 2020/7/27 19:52
# @Author   : iTreeNewBee
# @File     : approve.py
# @Project  : 登录实例
from HWOcrClientAKSK import HWOcrClientAKSK
from HWOcrClientToken import HWOcrClientToken
from selenium.webdriver.common.action_chains import ActionChains
from selenium import webdriver
import os
import base64
from time import sleep
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.common.by import By



def get_code(img_path):
    '''
    传入图片路径获取验证码,AK、SK是华为OCR服务的授权
    :param img_path:
    :return: code
    '''
    AK = '***'
    SK = "***"
    region = "cn-north-4"
    req_uri = "/v1.0/ocr/general-text"
    img_path = img_path
    option = {}
    try:
        ocr_client = HWOcrClientAKSK(AK, SK,
                                     region)
        response = ocr_client.request_ocr_service_base64(req_uri, img_path,
                                                         option)
        # print(response.json()['result'])
        words = response.json()['result']['words_block_list'][0]['words']
        code = ''.join(list(filter(str.isalnum, str(words).replace(' ', ''))))
        return code
    except ValueError as e:
        print(e)


def isElementExist(driver,elements):
    """
    :param driver:  浏览器驱动
    :param elements: 元素classname定位方法
    :return:  type bool ，True or False
    """
    try:
        driver.find_element_by_class_name(elements)
        print("True")
        return True
    except:
        print("False")
        return False


def get_codeimg(img_base64):
    '''
    下载验证码图片
    :param img_base64:
    :return:
    '''
    imagedata = base64.b64decode(img_base64)
    file = open('code.jpg', "wb")
    file.write(imagedata)
    file.close()


def login():
    '''
    登录
    :return:
    '''
    browers = webdriver.Chrome()
    browers.maximize_window()
    browers.get('http://1.1.1.1:8080/#/')
    try:
        WebDriverWait(browers, 1).until(EC.presence_of_element_located((By.NAME, 'name')))
    except Exception as e:
        browers.implicitly_wait(3)
    # browers.implicitly_wait(3)
    browers.find_element_by_name('name').send_keys('fanglin')
    browers.find_element_by_name('pwd').send_keys('1qaz!QAZ')
    # 获取验证码图片base64
    base64_img = browers.find_element_by_id('code_img').get_property('src').split(',')[1]
    # get_codeimg(base64_img)
    code = get_code('code.jpg')
    code_input = browers.find_element_by_id('codeInput')
    code_input.send_keys(code)
    browers.find_element_by_id('submit_btn').click()
    try:
        WebDriverWait(browers, 1).until(EC.presence_of_element_located((By.CLASS_NAME, 'el-message-box')))
    except Exception as e:
        sleep(1)
    flag = isElementExist(browers, 'el-message-box')
    while flag:
        browers.find_element_by_css_selector('body > div.el-message-box__wrapper > div > div.el-message-box__btns > button').click()
        # sleep(1)
        code_input.clear()
        base64_img = browers.find_element_by_id('code_img').get_property('src').split(',')[1]
        # get_codeimg(base64_img)
        code = get_code('code.jpg')
        code_input.send_keys(code)
        browers.find_element_by_id('submit_btn').click()
        # sleep(1)
        # flag1 = isElementExist(browers, 'el-loading-text')
        try:
            WebDriverWait(browers, 1).until(EC.presence_of_element_located((By.CLASS_NAME, 'icon_logout')))
        except Exception as e:
            pass
        is_login = isElementExist(browers, 'icon_logout')
        if is_login:
            break
    return browers
    #     print(4444)
    # else:
    #     print('222222')
    #     return browers
    # print('333333')

if __name__ == '__main__':
    browers = login()
    sleep(1000)
    # browers.find_element_by_class_name('popper__arrow').send_keys('ljsdlfk')
```

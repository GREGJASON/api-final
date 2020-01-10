# 文档说明

|发布日期|2019.12.09|
| ---------- | --- |
|产品名称|闻香计划|
|文件现状|进行中|
|文件的主人|石恒|
|更新|2020.1.1|
[PPT和录屏]( https://github.com/NFUNewMedia2017/PPT)
# 1. 产品说明
##  价值宣言
- 阿里的花伴侣智能植物识别API的价值:
> 将识别到图片中植物的信息转化成文字，省去了用户搜索筛选的时间，提高了效率。

- 百度细粒度图像识别API的价值：
> 更进一步地识别图片 完善信息。

- 百度语音合成API的价值：
> 用户在不方便阅读文字信息的时候 可以进行语音播报。

## 产品宣言

> 闻香—每朵花都有它独特的香味

闻香是一款识别植物的小程序，在认识各种植物还能在线上开启属于自己的植物图鉴，用户在认知植物的同时还能获取植物科普知识。

##  用户痛点

- 遇到野生植物不认识，需要识别工具

- 不懂植物专业栽培理念和实际技巧，导致植物生长过程中受阻（生病 虫害）/致死

- 不愿去阅读冗长枯燥的百科文字知识

##  产品核心目标

- 识别图片植物，得出植物相关的百科信息。

- 植物百科信息语音读取，语音播报植物百科。

## d) 产品核心功能举例

植物图鉴模块

辨认植物模块

#### AR识别植物模块
个人模块

##  价值宣言
市场上已有的通过花果叶等特征部位图片识别各种植物花卉的产品，设有语音播报功能。用户在扫描完植物时，焦点更应该放在大自然，而不是手机上，因此基于此用户痛点，结合百度语音合成技术，制作出这款产品。

##  产品概述(最小可行性产品）
闻香以拍照识别图片中的植物为基础功能，用户拍照上传植物图片，可获得植物百科信息，一键点击语音播报植物百科信息。

##  人工智能概率性

花伴侣智能植物识别-品类最全，含花卉，植物和农田杂草共一万一千种，准确率>95%。

形色植物识别API总计识别4000种植物，准确率>98%。

百度语音合成API，准确率>97%。

# 2. 用户分析
## a) 目标用户群体
- 年龄：13-30岁 

- 学历：初中及以上

- 地区：城市

- 以学生、白领为主要用户

- 主要集中在90、00后

- 居住在三四线城市（目前一二线城市植物爱好者呈上升趋势）

- 植物爱好者、花艺爱好者、孩子家长、教育者、旅行者


## b) 用户需求
|.|功能|应用|技术|
| --- | --- |--- | --- |
|1| 植物花卉识别|看到未知植物 进行拍照并识别|图像识别
|2| 常见草类识别|即使是小草也想要知道其具体品种|图像识别
|3|植物百科信息|愿进一步了解身边植物详细资料，获取植物专业养护资料|图像识别
|4|语音播报|不想看太多的文字或者是不方便进行文字阅读的状况下|语音合成


## c) 使用的API

- [花伴侣智能植物识别API](https://market.aliyun.com/products/57124001/cmapi018620.html?spm=5176.10695662.1996646101.searchclickresult.698566bbXs1Z67#sku=yuncode1262000007)

- [形色植物识别API](https://market.aliyun.com/products/57124001/cmapi029377.html?spm=5176.10695662.1996646101.searchclickresult.1aef61a2LJohk8#sku=yuncode2337700006)

- [百度语音合成API](http://ai.baidu.com/tech/speech/tts)

- [百度细粒度图像识别API](https://cloud.baidu.com/product/imagerecognition/fine_grained)


# 3.可行性分析

**调用花伴侣智能植物识别API**

1.识别清晰的植物图片
![杜鹃.jpeg](https://upload-images.jianshu.io/upload_images/9130153-c795a559701a8cb8.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



```python
import base64
import requests
url_host = "http://plantgw.nongbangzhu.cn"
app_code = 'c29f496b34324aa7a7448845bf6148bc' #这里替换为你购买的AppCode
# 植物花卉识别接口_v2的请求示例http://localhost:8888/notebooks/Untitled4.ipynb?kernel_name=python3#
def recognize2():
    url_path = '/plant/recognize2'

    with open("20180927212049_91150.jpg", "rb") as image_file:
        img_base64 = base64.b64encode(image_file.read()).decode('ascii')
        body = {'img_base64': img_base64}

        headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE" + app_code}
        response = requests.request("POST","http://plantgw.nongbangzhu.cn"+'/plant/recognize2', data=body, headers=headers) # 默认utf-8
        print(response.text)

    return
# 植物百科信息获取
def info():
    url_path = '/plant/info'

    code = "gRznEHlcJyg46Tpd" # 这个植物代号是调用recognize2()时获得的InfoCode字段
    body = {'code': code}
    headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE " + app_code}
    response = requests.request("POST", url_host+url_path, data=body, headers=headers) # 默认utf-8
    print(response.text)

    return
info()
```

返回结果

{"log_id": 6350852702531560411, "result": [{"score": 0.9089241027832, 
"name": "杜鹃"}, {"score": 0.29999804496765, "name": "石竹"}, {"score": 0.036180101335049, 
"name": "迎红杜鹃"}, {"score": 0.028431579470634, "name": "锦带花"}, {"score": 0.020664585754275, "name": "皋月杜鹃"}]}




**调用百度细粒度图像识别API**

![蒲公英.jpeg](https://upload-images.jianshu.io/upload_images/9443754-cf8a9eee1e9928ac.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```python
# encoding:utf-8
import base64
import urllib
from urllib.request import urlopen
from urllib.request import Request
from urllib.error import URLError
from urllib.parse import urlencode

'''
植物识别
'''

request_url = "https://aip.baidubce.com/rest/2.0/image-classify/v1/plant"


f = open('20180927212049_91150.jpg', 'rb')
img = base64.b64encode(f.read()).decode('ascii')

params = {"image":img}
params = urlencode(params).encode("utf-8")

access_token = '24.509ddd490e9f742e99c0106a6c27ab9d.2592000.1579846768.282335-17996248'
request_url = request_url + "?access_token=" + access_token
request = Request(url=request_url, data=params)
request.add_header('Content-Type', 'application/x-www-form-urlencoded')
response = urlopen(request)
content = response.read()
content=content.decode('utf-8')
if content:
    print (content)

返回结果

```{"log_id": 304085595462192825, "result": [{"score": 0.708844780921936, "name": "蒲公英"}, {"score": 0.05350668728351593, "name": "辽东蒲公英"}, {"score": 0.024197814986109734, "name": "药用蒲公英"}]}
In [77]:

```

2.识别杂草
#### 狗尾草
![狗尾草.jpg](https://upload-images.jianshu.io/upload_images/9130153-0662418171084be3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```python
def weed():
    url_path = '/plant/recognize_weed'

    with open("./pics/狗尾草.jpg", "rb") as image_file:
        img_base64 = base64.b64encode(image_file.read()).decode('ascii')
        body = {'img_base64': img_base64}

        headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE " + app_code}
        response = requests.request("POST", url_host+url_path, data=body, headers=headers) # 默认utf-8
        print(response.text)

    return
weed()

```

```json
{"Status":0,"Message":"OK","Result":[{"Score":"71.10","AliasList":[],"Genus":"狗尾草属","InfoCode":"lxBYUeDkinFIebDN","AliasName":"","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E9%87%91%E8%89%B2%E7%8B%97%E5%B0%BE%E8%8D%89/57b22cd5eee20ca7a42052f2c295ec24bee56743bf4082d8b386d0fb1f22a51e.jpeg","LatinName":"Setaria pumila",
"Name":"金色狗尾草"},{"Score":"26.63","AliasList":["谷莠子","莠"],"Genus":"狗尾草属","InfoCode":"Ldky3VBXkBXT1gk1","AliasName":"谷莠子、莠","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%8B%97%E5%B0%BE%E8%8D%89/3eb25266b9522aa0c4579c4cee8509ffe595f981c0792c5881a77087a353ce99.jpeg","LatinName":"Setaria viridis",
"Name":"狗尾草"},{"Score":"2.04","AliasList":["法氏狗尾草"],"Genus":"狗尾草属","InfoCode":"LTRjFvZfKKGC42gA","AliasName":"法氏狗尾草","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E5%A4%A7%E7%8B%97%E5%B0%BE%E8%8D%89/3c685666212f4bcddabc866372f6261d3e53e770a2e8c0a14904c5a85b8e2d03.jpeg","LatinName":"Setaria faberi",
"Name":"大狗尾草"},{"Score":"0.01","AliasList":["荠菜","菱角菜"],"Genus":"荠属","InfoCode":"O0OUVuZnuRzsdf6E","AliasName":"荠菜、菱角菜","Family":"十字花科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E8%8D%A0/eb35c6ecc963232588968eb2efa297f81ab84f0171c3a008bb71adb85fa8bf05.jpeg","LatinName":"Capsella bursa-pastoris",
"Name":"荠"},{"Score":"0.01","AliasList":[],"Genus":"菵草属","InfoCode":"hMKVHhUAV4entqJr","AliasName":"","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E8%8F%B5%E8%8D%89/2a3064175a9d0506a4b4fec259ad40044bdb4a93a6b3a26d521d0e32d0941d04.jpeg","LatinName":"Beckmannia syzigachne",
"Name":"菵草"}]}
```

**百度API**

```json
{"log_id": "6791850728801845563",
	"result": [
	    {"score": 0.96171873807907,
			"name": "狗尾草"},
		{"score": 0.11733993142843,
			"name": "小草"},
		{"score": 0.020295264199376,
			"name": "金色狗尾草"},
		{"score": 0.0097219282761216,
			"name": "梯牧草"},
		{"score": 0.0089892046526074,
			"name": "猫尾草"}]}
```
百度细粒度图像识别的结果较正确，图片是狗尾草而不是金色狗尾草，因为光线原因，狗尾草的根须被阳光照射，看起来像金色的，导致花伴侣识别出现差错。

3.识别模糊的植物图片
#### 曼莎珠华、曼陀罗

![image](https://upload-images.jianshu.io/upload_images/9130153-685ad592134f1e13.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**花伴侣API**
输出
![60QN)DG[AWX6HM}Y)SZ{GAQ.png](https://upload-images.jianshu.io/upload_images/9130153-df3f0f29d4c5438a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```json
{"Status":0,"Message":"OK","Result":[{"Score":"68.33","AliasList":["蟑螂花","龙爪花"],"Genus":"石蒜属","InfoCode":"b7bK68TQkpSYFWQy","AliasName":"蟑螂花、龙爪花","Family":"石蒜科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%9F%B3%E8%92%9C/a57f668fc68e5576ecd5629079b2f62a7883a7981a98d43c84ea8ee12f734fe0.jpeg","LatinName":"Lycoris radiata",
"Name":"石蒜"},{"Score":"10.90","AliasList":[],"Genus":"虎耳兰属","InfoCode":"YYsDD68zEX3S5IJA","AliasName":"","Family":"石蒜科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%BD%91%E7%90%83%E8%8A%B1/326d5acf43296dcfea5403c200090b10553ffe018cc05ff8801072d334d4c326.jpeg","LatinName":"Haemanthus multiflorus",
"Name":"网球花"},{"Score":"3.47","AliasList":["宽苞茅膏菜"],"Genus":"茅膏菜属","InfoCode":"r7GxejtzIogOxTAh","AliasName":"宽苞茅膏菜","Family":"茅膏菜科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E5%8C%99%E5%8F%B6%E8%8C%85%E8%86%8F%E8%8F%9C/b0ed070faf73d9ceda1c7b5fd787947e2b1563adb89033e373f47e721d13625f.jpeg","LatinName":"Drosera spatulata",
"Name":"匙叶茅膏菜"},{"Score":"1.56","AliasList":["灯笼花","假西藏红花"],"Genus":"木槿属","InfoCode":"aSYfLGuDxcY7KUCr","AliasName":"灯笼花、假西藏红花","Family":"锦葵科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E5%90%8A%E7%81%AF%E8%8A%99%E6%A1%91/bb0a9452a68edf55a1e43e3facde2c1d67088ffdc41b7af0a7ee418a06137986.jpeg","LatinName":"Hibiscus schizopetalus",
"Name":"吊灯芙桑"},{"Score":"0.75","AliasList":[],"Genus":"","InfoCode":"qvguYOtMzX26EKoS","AliasName":"","Family":"","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%9C%B1%E7%A0%82%E6%A2%85/32ca46e12651f98ad9c8fb729f64f9a39df403a2859ccaae2bbacdf49a019457.jpeg","LatinName":"Turpinia pomifera var. pomifera",
"Name":"朱砂梅"}]}
```
**百度细粒度图像识别API**
```json
{
	"log_id": "4001458201794735259",
	"result": [
		{"score": 0.96764361858368,
			"name": "石蒜"	},
		{"score": 0.36455509066582,
			"name": "红花石蒜"	},
		{"score": 0.22701632976532,
			"name": "秦艽"	},
		{"score": 0.02585749514401,
			"name": "曼陀罗"	},
		{"score": 0.012681784108281,
			"name": "玫瑰石蒜"}]}
```
两家API识别结果都有偏差，第一结果均为石蒜，但是百度API，第四个结果是正确的，曼莎珠花又称曼陀罗。


4.百度语音合成API

![语音合成.jpg](https://upload-images.jianshu.io/upload_images/9130153-401f0f852291377b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 4.API使用风险评估
#### 图片灰暗的蒲公英花
![暗蒲公英花.jpg](https://upload-images.jianshu.io/upload_images/9130153-74d5a74558e2005f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
输出结果

**花伴侣API**
```python
import base64
import requests
url_host = "http://plantgw.nongbangzhu.cn"
app_code = '-' #这里替换为你购买的AppCode
# 植物花卉识别接口_v2的请求示例
def recognize2():
    url_path = '/plant/recognize2'

    with open("./pics/暗蒲公英花.jpg", "rb") as image_file:
        img_base64 = base64.b64encode(image_file.read()).decode('ascii')
        body = {'img_base64': img_base64}

        headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE " + '38ef43ff3c704a7c8bc5f934185b3a3d'}
        response = requests.request("POST", url_host+url_path, data=body, headers=headers) # 默认utf-8
        print(response.text)

    return
recognize2()
```

```json

{"Status":0,"Message":"OK","Result":[{"Score":"21.48","AliasList":["红毛大字草"],"Genus":"虎耳草属","InfoCode":"54rnyde9GLF7wR4i","AliasName":"红毛大字草","Family":"虎耳草科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%BA%A2%E6%AF%9B%E8%99%8E%E8%80%B3%E8%8D%89/120d6ca9d339de3ab7245cf239ad26cd443bfdccf4e6de083f90f5f5c57955f9.jpeg","LatinName":"Saxifragarufescens",
"Name":"红毛虎耳草"},
{"Score":"4.06","AliasList":[],"Genus":"星果草属","InfoCode":"oXlVI0VNZdLaedPm","AliasName":"","Family":"毛茛科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%98%9F%E6%9E%9C%E8%8D%89/90500c265a59f7ab961096372778d28dc567f032a997bea7d91895ee68c1e691.jpeg","LatinName":"Asteropyrum peltatum",
"Name":"星果草"},
{"Score":"2.87","AliasList":[],"Genus":"水毛茛属","InfoCode":"Glr2LtWgQR1CcBv4","AliasName":"","Family":"毛茛科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%B0%B4%E6%AF%9B%E8%8C%9B/abb8e9fda07414340cab3916495d11fb2ba015225f867660a6627a578e71ed5a.jpeg","LatinName":"Batrachium bungei",
"Name":"水毛茛"},
{"Score":"1.64","AliasList":["异叶水车前","龙爪菜"],"Genus":"水车前属","InfoCode":"j6Q5iuIK3EWPOdho","AliasName":"异叶水车前、龙爪菜","Family":"水鳖科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%B5%B7%E8%8F%9C%E8%8A%B1/26f4ed8bbc7d71603d73afce4cac80bf9291b7b8f1a70562b9976ec5590c0850.jpeg","LatinName":"Ottelia acuminata",
"Name":"海菜花"},
{"Score":"1.50","AliasList":[],"Genus":"淫羊藿属","InfoCode":"k3v1uRBPjzoGmQpR","AliasName":"","Family":"小檗科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%B2%97%E6%AF%9B%E6%B7%AB%E7%BE%8A%E8%97%BF/ba6b39491fb2641199574174486066e574a19552ad6398f774c260bd4a3c7d8e.jpeg","LatinName":"Epimedium acuminatum",
"Name":"粗毛淫羊藿"}]}
```
**百度API**

```json
{"log_id": "4447856955722587387",
	"result": [
		{"score": 0.62893480062485,
			"name": "款冬"},
		{"score": 0.23325063288212,
			"name": "蒲公英"},
		{"score": 0.081424951553345,
			"name": "毛果一枝黄花"},
		{"score": 0.049502149224281,
			"name": "向日葵"},
		{	"score": 0.047010716050863,
			"name": "菊花"}]}
```
百度细粒度图像识别API识别结果第2个是正确的，而花伴侣API的结果都是错误的。

---
植物图片清晰识别的效果最好，甚至使用模糊的、图片上有字体遮盖的图片，曼莎珠花属石蒜科，但并不是石蒜，所以识别结果有偏差。
但是使用昏暗且模糊化的图片，识别结果是错误的。光照和清晰度都在影响着植物的识别结果。

# 5.产品原型

1.产品结构图
![image.png](https://upload-images.jianshu.io/upload_images/9443754-98e0a4814b95c087.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2.产品流程图
![image.png](https://upload-images.jianshu.io/upload_images/9443754-87b1fd3e47dc1111.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.产品原型
[ARPLANT]( http://nfunm073.gitee.io/api-final-axure-all)
[原型下载地址](http://nfunm073.gitee.io/api-final-axure-all)
4.api调用页面展示
[植物识别api调用结果展页面]( https://nfunm073.gitee.io/api-final-axure-all/#g=1&id=ffref1&p=%E9%89%B4%E5%AE%9A%E7%BB%93%E6%9E%9C)

# 将要做
- 语音播报可选择播放声音（男声、女声、儿童）
- 播放时可选择从何处开始播报。做进度条，拖动进度条可到达播放位置
- 可调整播放语速

# GeeTest请求分析

***
###一号请求:

v为Unix时间戳加上0-10000的随机整数  gt和challenge为后面的请求会用到的参数

req:GET
http://www.gsxt.gov.cn/SearchItemCaptcha?v=1489633318000

res:
{"success":1,"gt":"1d2c042096e050f07cb35ff3df5afd92","challenge":"e30bbb08a4180588709602555b322fcf"}
***
###二号请求:

callback可能是本地生成的回调函数，后缀是随机数+目前时间

req:GET
http://api.geetest.com/gettype.php?gt=1d2c042096e050f07cb35ff3df5afd92&callback=geetest_1489633324804

res:
geetest_1489633324804({"status": "success", "data": {"static_servers": ["static.geetest.com", "dn-staticdown.qbox.me"], "path": "/static/js/geetest.5.10.10.js", "type": "slide"}})
***
###三号请求:

响应中fullbg和bg则分别是完整的背景和缺块的背景, 图片Host为http://static.geetest.com 
staticservers和https可以帮我们还原出完整的图片地址

req: GET
http://api.geetest.com/get.php?gt=1d2c042096e050f07cb35ff3df5afd92&challenge=e30bbb08a4180588709602555b322fcf&product=popup&offline=false&protocol=&path=/static/js/geetest.5.10.10.js&type=slide&callback=geetest_1489633321850

res:
geetest_1489633321850({"benchmark": false, "id": "ae30bbb08a4180588709602555b322fcf", "fullbg": "pictures/gt/895656306/895656306.jpg", "https": false, "xpos": 0, "challenge": "e30bbb08a4180588709602555b322fcf98", "hide_delay": 800, "ypos": 33, "fullpage": false, "feedback": "", "link": "", "gt": "1d2c042096e050f07cb35ff3df5afd92", "clean": true, "type": "slide", "static_servers": ["static.geetest.com/", "dn-staticdown.qbox.me/"], "api_server": "http://api.geetest.com/", "mobile": false, "theme_version": "3.2.0", "version": "5.10.10", "bg": "pictures/gt/895656306/bg/12398010a.jpg", "slice": "pictures/gt/895656306/slice/12398010a.png", "logo": false, "height": 116, "show_delay": 250, "product": "popup", "theme": "golden"})

***

###四号请求:

get和challenge参数已有
passtime 应该是耗时，给个随机数即可
imload ?
userresponse 明显是最终计算出来的滑块长度通过加密后的值

req:GET
http://api.geetest.com/ajax.php?gt=1d2c042096e050f07cb35ff3df5afd92&challenge=035c84f8e9230e7b46865d5f68825e0b78&userresponse=82282288cddcb&passtime=1614&imgload=60&a=C--%2C--%2C----%2C-%2C-%2C----(!!%3Atstyty(t(tytysstssstusst!*((!)((!)(!)(!*y(y!)(yyytysstssstsssttyt((t(ttsssttsysstssstssst(!!(q6%2C4-2020111919%3A10111%24)L911911111111111112020111119EU9111120113%2F1111191111111M9%3F03%24)A%24)a%24)L%24.m&callback=geetest_1489721184474

res:



***

###最终查询请求:

req: POST
http://www.gsxt.gov.cn/corp-query-search-1.html

param:
tab=ent_tab
token=44593646
searchword=xxx
geetest_challenge=c2b0c5ffd7d9b9c984c99651013720e263
geetest_validate=e7841308e7655fb2b15e4aeb4efd3eeb
geetest_seccode=e7841308e7655fb2b15e4aeb4efd3eeb|jordan

res:
查询后网页
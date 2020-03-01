# fws

VFP的WEB接口函数，用于web开发，可以运行于IIS或者nginx下，扩展你的VFP WEB开发能力。支持CGI和FASTCGI模式。

一个经典 hello world  例子：


Set Path To JustPath(_vfp.ServerName) ADDITIVE 

Set Library To  fws.dll 

If _vfp.StartMode=0

	fws_listen("0.0.0.0",9000)
	
EndIf 

nCount=0

Do while fws_accept()>=0

    fws_write(Transform(Datetime())+" : hello 汉字测试") 
    
    nCount = nCount + 1 
    
    If nCount>5000
    	Exit
    EndIf 
EndDo 


函数说明：

fws_Write(cString)
向浏览器输出字符串

fws_Header(cHeaderKey[,cValue])
读取客户端HTTP请求头的信息，或向客户端输出HTTP头

fws_Request(cFormKey)
读取客户端form提交的字段值

fws_Cookies(cKey[,cValue[,tExpires[cPath,[cDomain]]]])  
读取客户端的Cookies设置，或设置客户端的cookies值，失效日期，有效路径和有效域名

fws_Redirect(cUrl)
重转向URL

fws_Status(cHttpCode)
输出HTTP状态

fws_Expires(tTime)
设置页面的有效时间

fws_accept()
等待接受客户端连接

fws_listen(cIP,nPort)
本地监听，仅用于fastcgi调试模式

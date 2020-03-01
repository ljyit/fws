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

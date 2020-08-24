## 爬取好友名单

```python
#!/usr/bin/env python3

import itchat
import os
import re

itchat.auto_login(hotReload=True)
roomlist = itchat.get_chatrooms()

with open("./memberlist.txt","w",encoding="utf8") as f1:
    f1.write("你一共加入了{0}个群".format(str(len(roomlist))))
    
for i in roomlist:
    memberList = itchat.update_chatroom(i["UserName"],detailedMember=True)
    ImageFlore = "./"+str(memberList["NickName"])
    os.makedirs(ImageFlore)
    with open("./memberlist.txt","a",encoding="utf8") as f2:
        f2.write('\n\n----------------------------------群名称：'+str(memberList["NickName"])+",该微信群一共有{0}个成员".format(str(len(memberList['MemberList'])))+'------------------------------------------\n')
        for j in memberList["MemberList"]:
            img = itchat.get_head_img(userName=j["UserName"],chatroomUserName=memberList["UserName"])
            name = str(j["NickName"])
            name = name.replace("\r",r"_").replace('\n','_').replace("\|",'_')
            name = re.sub("[\\\/\:\*\?\"\<\>\|\.！@#￥%… … &*（）— — +？》《|\、\-\=]+', ","_",name)
            f2.write(name+"\n")
            try:
                fileImage = open(ImageFlore+"/"+name+".jpg",'wb')
            except:
                continue
            else:         
                fileImage.write(img)
                fileImage.close()


```


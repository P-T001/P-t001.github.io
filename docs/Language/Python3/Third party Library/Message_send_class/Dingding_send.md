# Dingding_send

---

前提：

在钉钉中拉群（群需要3人或3人以上才能组建，组完后删除其他人，自己独享）

群设置/智能群助手/添加机器人/.../自定义/ (**Webhook/自定义关键词**)

代码：

```
import json
import requests

def Dingding_send_msg(webhook,keyword,msg,reminders=None):
    '''
    :param webhook:   机器人的webhook地址
    :param keyword:   机器人设置的关键词
    :param msg:       发送的信息内容
    :param reminders: @提醒人 例：{"群用户手机" @群用户 | "all" @所有人 | 空列表 不@}
    :return:
    '''
    headers = {'Content-Type': 'application/json;charset=utf-8'}     # 请求头部
    if len(reminders)==0:
        data = {
            "msgtype": "text",
            "text": {
                "content": keyword + msg
            },
        }
    elif len(reminders)==1 and reminders[0]=='all':
        data = {
            "msgtype": "text",
            "text": {
                "content": keyword + msg
            },
            "at": {
                "isAtAll": True  # 此处为是否@所有人,会忽略@单独用户
            }
        }
    else:
        data = {
            "msgtype": "text",
            "text": {"content": keyword+msg
            },
        "at": {
            "atMobiles":reminders,   #此处为需要@什么人。填写具体用户手机号码
        }
        }
    r = requests.post(webhook,data=json.dumps(data),headers=headers)
    return r.text

if __name__ == '__main__':
    webhook = 'https://oapi.dingtalk.com/robot/send?access_token=xxxxxxx'    
    keyword='/'
    msg = '我是发送内容'
    reminders = ['all']
    print(Dingding_send_msg(webhook,keyword,msg,reminders))
```


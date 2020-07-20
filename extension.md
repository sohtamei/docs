## 拡張ブロック作成 補足
[拡張ブロック作成](http://sohta02.web.fc2.com/familyday_extension.html) の補足です。

![dd](http://sohta02.web.fc2.com/images/image621.png)

#### つくるっち→ロボット プロトコル
| | 内容 |
| ---- | ---- |
| byte0 | FF |
| byte1 | 55 |
| byte2 | length |
| byte3 | command |
| byte4~(2+length) | 引数(length-1) |

#### ロボット→つくるっち プロトコル
| | 内容 |
| ---- | ---- |
| byte0 | FF |
| byte1 | 55 |
| byte2 | length |
| byte3 | type<br />1:byte<br />2:short<br />3:long<br />4:float<br />5:double<br />6:string<br />7:bytes |
| byte4~(2+length) | 戻り値(length-1) |


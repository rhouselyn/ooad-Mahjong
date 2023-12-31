# Mahjong 设计



## 界面（2D）

登陆界面
搭配服务器。有名字密码和ID。ID唯一且不可变

大厅界面
皮肤切换，玩家信息，创建房间，加入房间（输入房间码进入）

组队界面
房间 随机码

读档的界面
	仅房主可存档和读档		
	检测是否为对应的4个玩家

纯3D 或 2D加3D

## 信息存储

仅房主可存档和读档

每局游戏都有对应的key存在于服务器且与玩家有map（方便回访）

服务器与玩家本地均拥有**完整**的牌局信息（待定）

Hash Map A：名字为圈数和局数 eg. 1_2.内容为B和C的map

Hash Map B：玩家和门风的map

Hash Map C：牌序和游戏日志的map

双向链表：

1. 牌序
2. 游戏日志：哪个玩家打了什么牌

## 游戏流程



正常游戏流程：

1. 服务器根据玩家信息分配门风，第一圈第一局随机分配，后续根据国标麻将规则分配位置。

2. 玩家：洗牌动画，同时从服务器拉取牌桌信息。
   服务器：洗牌

3. 摸牌，补花等操作

4. 庄家开始
   玩家：打牌，向服务器传递信息
   服务器：接受信息，并传递给其他玩家

5. 3秒读条时间
   玩家：思考，选择吃碰杠和（这四种操作下文简称为“额外操作”）

   玩家的计时仅供参考，实际由服务器的信息为准。（网络延迟，服务器卡顿等）

   服务器：静默等待接受消息并计时

   1. 若有额外操作，检测是否合法（安全性），不合法则静默。合法则处理，并合理安排下一位
   2. 若无，即计时结束后，安排下一位出牌

6. 由服务器安排的玩家进行回合
   玩家：摸牌，是否和牌，打牌。并向服务器传递信息
   服务器：该玩家开始时，“模拟” 进张。等待玩家和牌或打牌信息
   若和牌，根据国标计算番数。->7

   若不和牌，检测是否还有剩余，若有则->5 ,若无 -> 7

7. 结束牌局，根据结果统计分数。并更新玩家分数。

8. 根据国标规则调换玩家位置。->2



## 交流

局内交流，大厅交流

## 难点 

服务器的搭建

# ADVANCE

- [x] 更精美的游戏：游戏内可更改的牌背、桌布、背景⾳乐等 
- [ ] AI ⼈机对战：⼈机对战时使⽤算法或者模型，⽽不是随机出牌 
- [x] 在线对战：通过局域⽹或服务器，与在线玩家联⽹对战 
- [ ] 数据统计：统计玩家的得分、⾛势等数据，其他玩家可以在游戏内查看 
- [x] 交流和沟通：⼤厅、对局内的玩家可以发送⽂字对话、表情包等 
- [x] 更好的⽹络服务：例如更合理的同步⽅式，玩家掉线后的处理等 
- [ ] 更多⿇将玩法：例如四川⿇将、台湾⿇将等，也可以是⾃定义的⿇将规则

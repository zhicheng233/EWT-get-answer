# EWT-get-answer
获取升学E网通（EWT）选择题答案

[![EWT Killer](https://img.shields.io/github/v/release/zhicheng233/EWT-get-answer?color=5d89d2&label=EWT%20Killer)](https://github.com/zhicheng233/EWT-get-answer/releases/latest)
[![Published at](https://img.shields.io/github/v/release/zhicheng233/EWT-get-answer?color=5d89d2&label=Published%20at)](https://github.com/zhicheng233/EWT-get-answer/releases/latest)
[![GitHub license](https://img.shields.io/github/v/release/zhicheng233/EWT-get-answer)](https://github.com/zhicheng233/EWT-get-answer/blob/main/LICENSE)
[![GitHub stars](https://img.shields.io/github/v/release/zhicheng233/EWT-get-answer)](https://github.com/zhicheng233/EWT-get-answer/stargazers)
[![GitHub forks](https://img.shields.io/github/v/release/zhicheng233/EWT-get-answer)](https://github.com/zhicheng233/EWT-get-answer/network/members)
[![GitHub issues](https://img.shields.io/github/v/release/zhicheng233/EWT-get-answer)](https://github.com/zhicheng233/EWT-get-answer/issues)

DL:https://blog.zhicheng233.ml/data/DL/EWT%E9%80%89%E6%8B%A9%E9%A2%98%E7%AD%94%E6%A1%88%E8%8E%B7%E5%8F%96.exe

~~最近可能会将该软件移植到JS脚本~~由houtarchat移植的js脚本，适用于Tampermonkey® 
其源码在 [Github](https://github.com/houtarchat-cyber/EWT-get-answer) 
[Greasy Fork](https://greasyfork.org/zh-CN/scripts/450155)


# 如何构建

1.下载 易语言 5.9 （破不破解都行自己喜欢）

2.导入 .e 源码至易语言

3.导入相关模块

4.修改、编译、发布

## 常见编译问题

Q：为毛我编译出来的大小和MD5和你发布的版本不一样

A：使用了精易助手（易语言助手）里的智能编译，编译过程中会进行脱壳压缩后再进行加壳，所以大小和MD5不同


Q：为毛我编译出来的报毒了？

A：同上一问答案

Q: 编译提示动态链接失败

A：将VC链接器版本切换到VC8以下

## ​本程序遵循GPL ( GNU General Public License )开源许可协议，程序仅供学习交流，严禁商用或其他非法用途

## 调用的API
https://web.ewt360.com/customerApi/api/studyprod/web/answer/quesiton/analysis?questionId=填写&paperId=填写&reportId=填写&platform=填写&bizCode=填写
PS:questionId需通过旧API获取(https://web.ewt360.com/customerApi/api/studyprod/web/answer/paper?paperId=填写&platform=填写&bizCode=填写&reportId=0&isRepeat=0   作者:solstice23)

## 核心函数（方法）  方便没有运行环境的开发者调用
````#
.版本 2
.支持库 ExuiKrnln
.支持库 spec

.子程序 _按钮EX1_鼠标左键单击, 整数型
.参数 坐标x, 整数型
.参数 坐标y, 整数型
.参数 保留参数1, 整数型
.参数 保留参数2, 整数型


编辑框EX6.内容 ＝ “”
.如果 (选择夹EX1.现行子夹 ＝ 1)
    ' 切换界面
    选择夹EX1.现行子夹 ＝ 0
    创建缓动任务Ex (1, #缓动_二次方缓动_Out, -20, 8, 1, 动画速度, 到整数 (&事件_缓动任务回调), 0, , )
    创建缓动任务Ex (1, #缓动_二次方缓动_Out, 0, 255, 1, 动画速度, 到整数 (&事件_缓动任务回调), 1, , )
    ' 暂时禁用按钮
    暂停按钮事件 ()
    返回 ()

.否则
    编辑框EX1.内容 ＝ 编辑框EX1.内容 ＋ “&”  ' 必须！！否则有些题目会获取不了
.如果结束
题号 ＝ 0
' 切换界面
选择夹EX1.现行子夹 ＝ 1
创建缓动任务Ex (1, #缓动_二次方缓动_Out, -20, 8, 1, 动画速度, 到整数 (&事件_缓动任务回调), 0, , )  ' 选择框缓动
' 暂时禁用按钮
暂停按钮事件 ()
' 获取paperId
paperId ＝ 文本_取出中间文本 (编辑框EX1.内容, “paperId=”, “&”, , )
' 获取platform
platform ＝ 文本_取出中间文本 (编辑框EX1.内容, “platform=”, “&”, , )
' 获取bizCode
bizCode ＝ 文本_取出中间文本 (编辑框EX1.内容, “bizCode=”, “&”, , )
' 给3个编辑框分别赋值
编辑框EX3.内容 ＝ paperId
编辑框EX4.内容 ＝ platform
编辑框EX5.内容 ＝ bizCode
' Cookie 更新、获取Cookie
Cookie ()
' 获取解析
获取网页数据 ()
获取id ()


.子程序 Cookie, , , 更新、获取cookie

.如果 (ewt_user ＝ “” 或 user ＝ “”)
    信息框 (“Cookie为空，接下来将获取Cookie！”, 0, “错误”, )
    载入 (登录器, , 真)

.否则

.如果结束

.如果 (文本_取出中间文本 (编码_utf8到gb2312 (网页_访问S (“https://web.ewt360.com/customerApi/api/studyprod/web/answer/paper?paperId=” ＋ paperId ＋ “&platform=” ＋ platform ＋ “&bizCode=” ＋ bizCode ＋ “&reportId=0&isRepeat=0”, 0, , “ewt_user=” ＋ ewt_user ＋ “;user=” ＋ user, , , , , , , , , , , , , , , , , )), “msg” ＋ #引号 ＋ “:” ＋ #引号, #引号 ＋ “,” ＋ #引号, , ) ＝ “页面失效，请重新登录”)
    调试输出 (编码_utf8到gb2312 (网页_访问S (“https://web.ewt360.com/customerApi/api/studyprod/web/answer/paper?paperId=” ＋ paperId ＋ “&platform=” ＋ platform ＋ “&bizCode=” ＋ bizCode ＋ “&reportId=0&isRepeat=0”, 0, , “ewt_user=” ＋ ewt_user ＋ “;user=” ＋ user, , , , , , , , , , , , , , , , , )))

    信息框 (“Cookie失效，接下来将重新获取Cookie！”, 0, “错误”, )
    载入 (登录器, , 真)

.否则

.如果结束




.子程序 获取网页数据, , , 获取网页数据

' https://web.ewt360.com/customerApi/api/studyprod/web/answer/paper?paperId=填写&platform=填写&bizCode=填写&reportId=0&isRepeat=0   ewt流出的API 用来获取questionId


答题页面数据 ＝ 编码_utf8到gb2312 (网页_访问S (“https://web.ewt360.com/customerApi/api/studyprod/web/answer/paper?paperId=” ＋ paperId ＋ “&platform=” ＋ platform ＋ “&bizCode=” ＋ bizCode ＋ “&reportId=0&isRepeat=0”, 0, , “ewt_user=” ＋ ewt_user ＋ “;user=” ＋ user, , , , , , , , , , , , , , , , , ))
调试输出 (“https://web.ewt360.com/customerApi/api/studyprod/web/answer/paper?paperId=” ＋ paperId ＋ “&platform=” ＋ platform ＋ “&bizCode=” ＋ bizCode ＋ “&reportId=0&isRepeat=0”)

调试输出 (答题页面数据)



.子程序 获取id, , , 拆分解析数据
.局部变量 questionId, 文本型

' 重点！！！！这里写了好久，所以特意把注释写的非常详细，慢慢看
' 重点！！！！这里写了好久，所以特意把注释写的非常详细，慢慢看
' 重点！！！！这里写了好久，所以特意把注释写的非常详细，慢慢看

questionId ＝ “null”  ' 初始化变量，不然循环跑不起来！！
' 已弃用
' |这里先跑一次防止最前面的ID获取不了！！是[{ 不是 },{
' |questionId ＝ 文本_取出中间文本 (答题页面数据, “[{” ＋ #引号 ＋ “id” ＋ #引号 ＋ “:” ＋ #引号, #引号 ＋ “,” ＋ #引号 ＋ “scoreCriterion”, , )
' |答题页面数据 ＝ 子文本替换 (答题页面数据, “[{” ＋ #引号 ＋ “id” ＋ #引号 ＋ “:” ＋ #引号 ＋ questionId ＋ #引号 ＋ “,” ＋ #引号 ＋ “scoreCriterion”, “ ”, , , 假)
' |获取答案 (questionId)  ' 传递questionId为 获取答案的参数

编辑框EX7.内容 ＝ questionId
延迟 (1)
' 一个简单的循环，如果id为空时停止循环（就是判断获取完没）
.判断循环首 (questionId ≠ “”)

    ' 取出文本，但有些在这里取出会有问题所以下面还加个判断再处理一次
    questionId ＝ 文本_取出中间文本 (答题页面数据, “{” ＋ #引号 ＋ “id” ＋ #引号 ＋ “:” ＋ #引号, #引号 ＋ “,” ＋ #引号 ＋ “scoreCriterion”, , )

    ' 正常取出是没有“ID”这给字符串的，应该为整数数据，所以如果questionId里有“id”则进行处理
    .如果真 (文本_寻找文本 (questionId, “id”, , ) ≠ -1)  ' 找到了就执行下面
        questionId ＝ questionId ＋ “!”  ' 加个标识符，不然下面行运行不了
        questionId ＝ 文本_取出中间文本 (questionId, “{” ＋ #引号 ＋ “id” ＋ #引号 ＋ “:” ＋ #引号, “!”, , )  ' 取id
        调试输出 (“一次过滤”)
    .如果真结束
    ' 有时取出来还是有问题的，但里面没有“id”所以判断是否有“title”
    .如果真 (文本_寻找文本 (questionId, “title”, , ) ≠ -1)
        questionId ＝ questionId ＋ “!”
        questionId ＝ 文本_取出中间文本 (questionId, “{” ＋ #引号 ＋ “id” ＋ #引号 ＋ “:” ＋ #引号, “!”, , )
        调试输出 (“二次过滤”)
    .如果真结束

    .判断循环首 (文本_寻找文本 (questionId, “title”, , ) ≠ -1)
        questionId ＝ questionId ＋ “!”
        questionId ＝ 文本_取出中间文本 (questionId, “{” ＋ #引号 ＋ “id” ＋ #引号 ＋ “:” ＋ #引号, “!”, , )
        调试输出 (“n次过滤”)
    .判断循环尾 ()


    ' 取完后删除取出的文本（替换成“”）避免干扰，不然只会一直取出一个数据
    答题页面数据 ＝ 子文本替换 (答题页面数据, “{” ＋ #引号 ＋ “id” ＋ #引号 ＋ “:” ＋ #引号 ＋ questionId ＋ #引号 ＋ “,” ＋ #引号 ＋ “scoreCriterion”, “ ”, , , 假)

    .如果 (小题数 ≠ 0)  ' 通过为真这跳过获取答案子程序
        小题数 ＝ 小题数 － 1
    .否则
        获取答案 (questionId)  ' 传递questionId为 获取答案的参数
    .如果结束

    编辑框EX7.内容 ＝ questionId
    延迟 (1)
    调试输出 (“ID” ＋ questionId)

.判断循环尾 ()


.子程序 获取答案, , , 调用api获取答案
.参数 questionId, 文本型
.局部变量 正确答案, 文本型
.局部变量 答案网页数据, 文本型

' “https://web.ewt360.com/customerApi/api/studyprod/web/answer/quesiton/analysis?questionId=填写&paperId=填写&reportId=填写&platform=填写&bizCode=填写” EWT新流出的API
' 发现 By 志成zhi_cheng#2885
正确答案 ＝ “null”  ' 初始化

答案网页数据 ＝ 编码_utf8到gb2312 (网页_访问S (“https://web.ewt360.com/customerApi/api/studyprod/web/answer/quesiton/analysis?questionId=” ＋ questionId ＋ “&paperId=” ＋ paperId ＋ “&reportId=1&platform=” ＋ platform ＋ “&bizCode=” ＋ bizCode, 0, , “ewt_user=” ＋ ewt_user ＋ “;user=” ＋ user, , , , , , , , , , , , , , , , , ))

题号 ＝ 题号 ＋ 1
.判断循环首 (正确答案 ≠ “”)

    正确答案 ＝ 文本_取出中间文本 (答案网页数据, “rightAnswer” ＋ #引号 ＋ “:[” ＋ #引号, #引号 ＋ “]”, , )
    ' 取完后删除取出的文本（替换成“”）避免干扰，不然只会一直取出一个数据
    答案网页数据 ＝ 子文本替换 (答案网页数据, “rightAnswer” ＋ #引号 ＋ “:[” ＋ #引号, “ ”, , 1, 假)  ' 我是傻逼，因为这里没写全导致排
    .如果真 (正确答案 ＝ “”)  ' 如果取到的是 空 就跳出循环
        跳出循环 ()
    .如果真结束

    ' 对HTML预留字符进行替换（如果有的话）
    正确答案 ＝ 子文本替换 (正确答案, “&nbsp;”, “ ”, , , 真)  ' 空格
    正确答案 ＝ 子文本替换 (正确答案, “&lt;”, “<”, , , 真)  ' <
    正确答案 ＝ 子文本替换 (正确答案, “&gt;”, “>”, , , 真)  ' <
    正确答案 ＝ 子文本替换 (正确答案, “&amp;”, “&”, , , 真)  ' &
    正确答案 ＝ 子文本替换 (正确答案, “&quot;”, #引号, , , 真)  ' "
    正确答案 ＝ 子文本替换 (正确答案, “&apos;”, “,”, , , 真)  ' ,
    调试输出 (“————————————————————”)
    调试输出 (文本_取出中间文本 (答案网页数据, “rightAnswer” ＋ #引号 ＋ “:[” ＋ #引号, #引号 ＋ “]”, , ))

    小题数 ＝ 小题数 ＋ 1


    编辑框EX6.内容 ＝ 编辑框EX6.内容 ＋ 到文本 (题号) ＋ “（” ＋ 到文本 (小题数) ＋ “）” ＋ “:” ＋ 正确答案 ＋ “!” ＋ #换行符
    .如果真 (窗口_是否存在 (“悬浮窗”) ≠ 0)
        悬浮窗.刷新 ()

    .如果真结束

    延迟 (1)

.判断循环尾 ()


.如果真 (小题数 ＝ 1)  ' 1=单题，要重置一下，不然会漏掉，我当时又傻逼了Debug了一个小时才想到
    小题数 ＝ 0

```#

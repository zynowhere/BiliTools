

# 项目说明

## 主要功能
**一、B站自动操作脚本BiliExp.py**

* [x] 每日获取经验(投币(支持自定义up主)、点赞、分享视频) 
* [x] 自动转发互动抽奖并评论点赞(官抽，非官抽支持指定关键字如"#互动抽奖#",支持跟踪转发模式)(Actions上默认1天执行1次，1次转发过去1天的动态，云函数上每次只转发过去10分钟的动态，建议修改为每10分钟执行1次)
* [x] 获取主站@和私聊消息提醒(便于多账号抽奖时获取中奖信息)
* [x] 参与官方转盘抽奖活动(目前没有自动搜集活动的功能,需要在配置文件config/activities.json里面手动指定活动列表)
* [x] 每日直播签到
* [x] 直播挂机(获取小心心,点亮粉丝牌，云函数默认关闭此功能，Actions上默认每次每个粉丝牌房间分别挂机45分钟)
* [x] 直播自动送出快过期礼物(默认送出两天内过期的礼物)
* [x] 直播天选时刻抽奖 (支持条件过滤，云函数默认搜索1次后立即退出，Actions上默认执行45分钟后退出，云函数上建议10分钟执行1次)
* [x] 直播应援团每日签到 
* [ ] ~~直播开启宝箱领取银瓜子(本活动已结束，不知道B站以后会不会再启动)~~ 
* [x] 每日兑换银瓜子为硬币 
* [x] 自动领取大会员每月权益(B币劵，优惠券)
* [x] 自动花费大会员剩余B币劵(支持给自己充电、兑换成金瓜子或者兑换成漫读劵)
* [x] 漫画APP每日签到
* [x] 自动花费即将过期漫读劵(默认不开启)
* [x] 自动积分兑换漫画福利券(需中午12点启动，默认不开启)
* [x] 自动领取大会员漫画每月福利劵
* [ ] ~~自动参加每月"站友日"活动(本活动已结束，不知道B站以后会不会再启动)~~
* [x] 定时清理无效动态(转发的过期抽奖，失效动态，支持自定义关键字，非官方渠道抽奖无法判断是否过期，默认不开启本功能)
* [x] 风纪委员投票(云函数默认没有案件立即退出，Actions默认45分钟内没有案件自动退出，云函数上建议每20分钟运行1次)

***默认所有任务每天只执行1次***，但建议***云函数***上***风纪投票***，***抽奖转发***，***天选时刻***等任务每天***多次***执行，***Actions***上***风纪投票***，***天选时刻***，***直播挂机(领小心心)***等任务可以***设置更长的超时时间***(默认45分钟后退出)。


## 使用方式(仅自动操作脚本部分)

## 下载直接运行操作：
#### 1.直接下载下来安装运行 python3 BiliExp.py 只要不关闭程序程序就会每一个小时运行一次(也可以定时某个时间运行一次 我把代码注释在里面需要的自行修改)。
#### 2.如果python3 BiliExp.py 运行错误 请运行 pip3 install -r requirements.txt 安装模块即可。
#### 3.事先修改config文件夹中的config.json 文件添加上你们的 账号信息Key推送Key信息。




## 使用方式(下载器部分)

* 1.转至[release](https://github.com/happy888888/BiliExp/releases) ，下载BiliDownloader，解压。
* 2.将账户密码填入config文件夹中的user.json文件(linux可将文件放入/etc/BiliExp/user.json)
* 3.使用videoDownloader
    ```
	命令行参数
	videoDownloader -a -p <下载文件夹> -v <视频1> -e <分集数> -q <质量序号> -v <视频2> -e <分集数> -q <质量序号> ...
	-a --ass       下载视频时附带ass文件,配合支持ass字幕的播放器可以显示弹幕
	-p --path      下载保存的路径，提供一个文件夹路径，没有会自动创建文件夹，默认为当前文件夹
	-v --video     下载的视频地址，支持链接，av号(avxxxxx)，BV号(BVxxxxxx)，ep，ss
	-e --episode   分p数，只对多P视频和多集的番剧有效，不提供默认为1，多个用逗号分隔，连续用减号分隔  -e 2,3,5-7,10 表示2,3,5,6,7,10集
	-q --quality   视频质量序号，0为能获取的最高质量(默认)，1为次高质量，数字越大质量越低
	-x --proxy     是否使用接口代理(可下载仅港澳台)，0为不使用(默认)，1为使用代理
	注意，一个 -v 参数对应一个 -e(-q, -x) 参数，如果出现两个 -v 参数但只有一个 -e(-q, -x) 参数则只应用于第一个，可以有多个 -v 参数以一次性下载多个视频
	-V --version   显示版本信息
	-h --help      显示帮助信息
	
	使用例子
	windows上(假如文件在D:\bilidownloader\videoDownloader.exe)，下载BV1qt411x7yQ的1,2,3,6集到D:\download目录
	打开cmd执行如下命令
	cd /d D:\bilidownloader
	videoDownloader -v BV1qt411x7yQ -e 1-3,6 -p D:\download
	
	linux上(提前将videoDownloader移动到/usr/local/bin)，下载BV1qt411x7yQ的1,2,3,6集到用户的download目录
	shell中执行
	videoDownloader -v BV1qt411x7yQ -e 1-3,6 -p ~/download
	```
* 4.使用mangaDownloader
    ```
	命令行参数
	mangaDownloader -p <下载文件夹> -m <漫画> -e <章节数> -f --width=<PDF每页宽度> --height=<PDF每页高度> --split
	-p --path      下载保存的路径，提供一个文件夹路径，没有会自动创建文件夹，不提供默认为当前文件夹
	-m --manga     下载的漫画mc号，整数
	-e --episode   章节数，不提供默认下载所有章节，多个用逗号分隔，连续用减号分隔  -e 2,3,5-7,10 表示2,3,5,6,7,10章节，注意番外也算一个章节
	-f --pdf       下载后合并为一个pdf，如果未指定-m --manga参数，则直接合并-p --path指定的文件夹内的jpg图片
	   --width     合并为pdf时指定每页宽度(像素)，若未指定 --height 则会按漫画比例自适应高度，仅当使用-f --pdf参数后有效，否则忽略
	   --height    合并为pdf时指定每页高度(像素)，若未指定 --width  则会按漫画比例自适应宽度，仅当使用-f --pdf参数后有效，否则忽略
	   --split     合并为pdf时拆分每个章节为一个pdf，仅当使用-f --pdf参数后有效，否则忽略
	-V --version   显示版本信息
	-h --help      显示帮助信息
	
	使用例子
	windows上(假如文件在D:\bilidownloader\mangaDownloader.exe)，下载漫画mc28565的3,9,12,13,14章到D:\download目录
	打开cmd执行如下命令
	cd /d D:\bilidownloader
	mangaDownloader -m 28565 -e 3,9,12-14 -p D:\download
	
	linux上(提前将mangaDownloader移动到/usr/local/bin)，下载漫画mc28565的3,9,12,13,14章到用户的download目录
	shell中执行
	mangaDownloader -m 28565 -e 3,9,12-14 -p ~/download
	```

</br></br></br>

## 使用说明(视频投稿部分)
* 1.转至[release](https://github.com/happy888888/BiliExp/releases) ，下载videoUploader，解压。
* 2.将账户密码填入config文件夹中的user.json文件(linux可将文件放入/etc/BiliExp/user.json)
* 3.使用videoUploader
    ```
	命令行参数
	VideoUploader -v <视频文件路径> -t <视频标题> -d <视频简介> -c <视频封面图片路径> -t <视频标签> -n -s <非原创时视频来源 网址>
	-v --videopath     视频文件路径
	-t --title         视频标题，不指定默认为视频文件名
	-d --desc          视频简介，不指定默认为空
	-c --cover         视频封面图片路径，不提供默认用官方提供的第一张图片
	-i --tid           分区id，默认为174，即生活,其他分区
	-T --tags          视频标签，多个标签用半角逗号隔开，带空格必须打引号，不提供默认用官方推荐的前两个标签
	-n --nonOriginal   勾选转载，不指定本项默认为原创
	-s --source        -n参数存在时指定转载源视频网址
	-D --DelayTime     发布时间戳,10位整数,官方的延迟发布,时间戳距离现在必须大于4小时
	-V --version       显示版本信息
	-h --help          显示帮助信息
	以上参数中只有-v --videopath为必选参数，其他均为可选参数
	
	使用例子
	windows上(假如程序在D:\VideoUploader\VideoUploader.exe,视频在D:\VideoUploader\测试视频.mp4)
	打开cmd执行如下命令
	cd /d D:\VideoUploader
	VideoUploader -v "D:\VideoUploader\测试视频.mp4"
	
	linux上(提前将VideoUploader移动到/usr/local/bin,视频文件在/root/upload/测试视频.mp4)
	shell中执行
	VideoUploader -v "/root/upload/测试视频.mp4"
	```

</br></br></br>



<br>

#### 获得cookies方法
B站操作需要的cookie数据可以按照以下方式获取
浏览器打开B站主页--》按F12打开开发者工具--》application--》cookies
<div align="center"><img src="https://s1.ax1x.com/2020/09/23/wjM09e.png" width="800" height="450" title="获取cookies示例"></div>


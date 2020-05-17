# LoveIt-AddMusic


<meting-js auto="https://music.163.com/#/song?id=449818741" list-folded=true></meting-js>

# 主题优化（一）：添加音乐
`由于qq音乐版权维护比较严重，在此处转为使用网易云音乐`

添加音乐外链有多种方法实现
### 1.进入网易云音乐网页版

实现起来比较简单,打开[网易云网页版](https://music.163.com/),搜索一首歌(ps:歌曲没有版权保护，可生成外链),直接把`外链`链接复制到博客中就可以了。

由于此方法缺点较多，没有歌词，有很多受版权保护的歌曲无法生成外链等等，这里就不多说了，强烈建议使用`第二种`方法。
### 2.使用Aplayer和MetingJS实现

使用平台：网易云音乐   &emsp;操作简单

(1)在博客的`head.html`中添加一下代码

```javascript
 
 <!-- require APlayer -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
    <script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
 <!-- require MetingJS -->
    <script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>
```

(2)在博文中需要的位置添加以下代码
```javascript
<meting-js auto="link" list-folded=true></meting-js>
```
上述`link`是你打开网易云的音乐链接，`list-folded=true`是在有多首歌曲时默认折叠列表
#### 例子
光年之外的音乐链接
```javascript
<meting-js auto="https://music.163.com/#/song?id=449818741" list-folded=true></meting-js>
```

### 3.悬浮音乐播放器的设置

[在此特别感谢 code show](https://corpython.github.io/post/hugo%E6%B7%BB%E5%8A%A0%E9%9F%B3%E4%B9%90%E6%9C%80%E7%BB%88%E7%AB%A0%E4%B9%8B%E6%82%AC%E6%B5%AE%E9%9F%B3%E4%B9%90%E6%92%AD%E6%94%BE%E5%99%A8/)

为实现`随时`播放和暂停音乐，符合阅读习惯，特寻找到`悬浮播放器`的设置

（1）在你的博客主题`partials`文件夹中添加`music.html`文件
```javascript 
<!DOCTYPE html>
<html>
<head>
    <!-- require APlayer -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
    <script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
    <!-- require MetingJS -->
    <script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>
</head>

<body>
    <div class="demo">
        <div id="player1">
        </div>
    </div>
    <script>
        var ap = new APlayer
            ({
                element: document.getElementById('player1'),
                narrow: false,
                fixed: true,
                autoplay: false,
                showlrc: true,
                mini: true,
                theme: '#FADFA3',
                loop: 'all',
                order: 'random',
                preload: 'auto',
                volume: 0.7,
                mutex: false,
                listFolded: false,
                listMaxHeight: 90,
                lrcType: 2,
                music:
                    [
                        {
                            artist: '要不要买菜',
                            name: '下山',
                            url: 'https://sharefs.yun.kugou.com/202001192159/203f75e19edc8d4abf66b2e7a7668422/G177/M04/18/07/8Q0DAF3VSvKAc3KNACpan3BcZnU587.mp3',
                            cover: 'https://p3fx.kgimg.com/stdmusic/20191120/20191120204014790242.jpg',
                            lrc:"[00:00.000] 作曲 : 朱斌语[00:01.000] 作词 : 朱斌语[00:04.39]编曲：王中易[00:12.61][00:15.16]要想练就绝世武功[00:17.15]就要忍受常人难忍受的痛[00:20.42]师傅喜欢喝的茶叫做乌龙[00:22.81]衣服爱穿中国红(嘿  师傅）[00:26.17]无论是炎夏或寒冬[00:28.68]我都很向往山门外的天空[00:31.83]还在南方等我 下山的我[00:35.00]的人叫小落[00:38.06]我左手一式太极拳[00:40.87]右手一剑刺身前[00:43.79]扫腿这招叫清雪[00:46.66]破轻功飞燕[00:49.44]我奇筋异脉力破天[00:52.41]一身正气荡人间[00:55.40]除暴安良我心愿[00:58.16]老师傅再见[01:01.77][01:13.40]要想练就绝世武功[01:15.56]就要忍受常人难忍受的痛[01:18.78]师傅喜欢喝的茶叫做乌龙[01:21.28]衣服爱穿中国红（师傅）[01:24.68]无论是炎夏或寒冬[01:27.23]我都很向往山门外的天空[01:30.23]还在南方等我 下山的我[01:33.43]的人叫小落（来）[01:36.54]我左手一式太极拳[01:39.40]右手一剑刺身前[01:42.35]扫腿这招叫清雪[01:45.13]破轻功飞燕[01:48.08]我奇筋异脉力破天[01:50.98]一身正气荡人间[01:53.98]除暴安良我心愿[01:56.76]老师傅再见[02:00.16](人法地~地法天~天法道~道法孜然 师..师傅，什么是孜然）[02:11.64]我左手一式太极拳[02:14.35]右手一剑刺身前[02:17.30]扫腿这招叫清雪[02:20.22]破轻功飞燕[02:23.11]我奇筋异脉力破天[02:26.06]一身正气荡人间[02:28.99]除暴安良我心愿[02:32.00]老师傅再见[02:35.35][02:36.32]制作人：王中易[02:37.15]混音：王宇呈[02:37.17]和声：朱斌语／涵木之／陈迪庭[02:38.16]配唱：王中易／谭佳瑶[02:39.03]统筹：谭佳瑶[02:40.04]制作公司/录音室：Hikoon Music[02:40.99]OP：嗨库文化",
                        },{
                            name: '悬日',
                            artist:'田馥甄',
                            url:'http://cdn.knowempty.xyz/%E7%94%B0%E9%A6%A5%E7%94%84%20-%20%E6%82%AC%E6%97%A5.mp3',
                            cover:'http://p1.music.126.net/qX7ixB5ZT2wVJwgACuf_nA==/109951164623078367.jpg',
                            lrc:'[00:00.000] 作曲 : 刘庭佐[00:01.000] 作词 : 葛大为[00:05.410]编曲 Arrangement ：柯宏升 Keke Ke、罗恩妮 Annie Lo[00:23.309]黄昏宣告着 今天已死亡[00:28.944]淡去的光阴 是我的战场[00:34.243]重遇在热络的市集[00:37.893]我很喜欢你的她[00:45.361]多配你呀[00:57.944]是真的开心 不是在作假[01:03.763]没有烟硝 互动健康[01:09.176]赶紧拿出我的手机[01:12.544]也让你看看我的他[01:19.660]不介意的话[01:25.743]落下 同一颗太阳[01:30.348]有什么特别的吗[01:38.426]你还不是一样[01:42.012]温暖却停在远方[01:49.143]对峙着不可能的爱情[01:53.561]也该像悬日那样[02:00.443]让它落下[02:24.709]她刻意放空自己[02:28.226]想留点时间让我们[02:31.461]再说说话[02:36.097]我像在愚弄自己[02:39.810]演哪出破绽百出的[02:43.112]心胸宽大[02:47.910]你不忘调侃自己[02:51.359]不够好却总是有人[02:54.913]为你牵挂[02:59.278]我又被回忆波及[03:02.879]心怎会这样不强壮[03:09.597]落下 同一颗太阳[03:14.778]有什么特别的吗[03:21.993]你还不是一样[03:26.262]温暖却停在远方[03:33.379]对峙着不可能的爱情[03:37.793]也该像悬日那样[03:44.460]让它落下[03:50.260]让它落下[03:56.111]让我放下[04:01.812]我没放下[04:07.894]我想放下[04:18.826]制作人 Producer：陈建骐 George Chen[04:19.427]木吉他 Acoustic Guitar：董运昌 Yun-Chang Dong、柯宏升 Keke Ke[04:19.943]钢琴 Piano：陈建骐 George Chen[04:20.576]和声编写 Backing Vocal Arrangement：田晓梅 Brandy[04:21.211]和声 Backing Vocal：田馥甄 Hebe Tien[04:21.811]弦乐编写和监制 Strings Arrangement and Producer：罗恩妮 Annie Lo[04:22.278]弦乐 Strings：曜爆甘音乐工作室 Just Busy Music Studio[04:22.795]第一小提琴 First Violin：蔡曜宇 Shuon Tsai[04:23.276]第二小提琴 Second Violin：陈奕勇 Yi-Yung Chen[04:23.743]中提琴 Viola：甘威鹏 Weapon Gan[04:24.175]大提琴 Cello：刘涵 Hang Liu（隐分子）[04:24.611]录音师 Recording Engineer：庄钧智 Thomas Chuang、林尚伯 Shang-Po Lin[04:25.098]录音室 Recording Studio：完美声音录音室 Perfect Sound Studio、强力录音室 Mega Force Studios[04:25.559]混音师 Mixing Engineer：林正忠 Cheng Chung Lin[04:25.944]混音录音室 Mixing Studio：白金录音室 Platinum Studio[04:26.376]ISRC：TW-EW7-20-01001',
                        },{
                            name:"假如爱有天意 (Live)",
                            artist:"李健",
                            url:"http://music.163.com/song/media/outer/url?id=31877467.mp3",
                            cover:"http://p2.music.126.net/DprdNIWpRWYZJak4Q-cS-Q==/2891715582273535.jpg?param=106x106",
                            lrc:'[00:30.650]当天边那颗星出现[00:36.530]你可知我又开始想念[00:41.560][00:43.250]有多少爱恋只能遥遥相望[00:49.690]就像月光洒向海面[00:54.430][00:56.710]年少的我们曾以为[01:02.710]相爱的人就能到永远[01:07.730][01:09.270]当我们相信情到深处在一起[01:15.860]听不见风中的叹息[01:20.530][01:21.910]谁知道爱是什么[01:28.930]短暂的相遇却念念不忘[01:34.000][01:34.910]用尽一生的时间[01:42.510]竟学不会遗忘[01:46.730][02:15.340]如今我们已天各一方[02:21.200]生活得像周围人一样[02:26.080][02:27.800]眼前人给我最信任的依赖[02:34.360]但愿你被温柔对待[02:38.810][02:40.340]多少恍惚的时候[02:47.410]仿佛看见你在人海川流[02:52.560][02:53.540]隐约中你已浮现[03:00.240][03:01.030]一转眼又不见[03:05.320][03:29.980]短暂的相遇却念念不忘[03:34.840][03:36.010]多少恍惚的时候[03:43.130]仿佛看见你在人海川流[03:48.460][03:49.070]隐约中你已浮现[03:56.280][04:04.020]一转眼又不见[04:08.450][04:15.170]当天边那颗星出现[04:21.200]你可知我又开始想念[04:26.400][04:28.080]有多少爱恋今生无处安放[04:34.830]冥冥中什么已改变[04:40.030][04:42.670]月光如春风拂面'
                            },
                            {
                                name:'我和我的祖国',
                                artist:'王菲',
                                url:'http://cdn.knowempty.xyz/我和我的祖国.mp3',
                                cover:'http://p2.music.126.net/HeGrAKPiZhKkONiFDxZvmw==/109951164384346866.jpg',
                                lrc:'[00:00.000] 作曲 : 秦咏诚[00:01.000] 作词 : 张藜[00:26.886]我和我的祖国一刻也不能分割[00:35.486]无论我走到哪里都流出一首赞歌[00:44.196]我歌唱每一座高山我歌唱每一条河[00:53.136]袅袅炊烟小小村落路上一道辙[01:04.352]啦……[01:15.141]你用你那母亲的脉搏和我诉说[01:30.514]我的祖国和我像海和浪花一朵[01:39.463]浪是海的赤子海是那浪的依托[01:48.130]每当大海在微笑我就是笑的旋涡[01:56.663]我分担着海的忧愁分享海的欢乐[02:07.830]啦…..[02:18.896]永远给我碧浪清波心中的歌[02:29.830]啦…….[02:40.796]永远给我碧浪清波心中的歌'
                            }
                    ]
                    
        });
        //ap.init();
    </script>
</body>
```

(2)在你的`single.html`中引入这个html文件
```javascript
 {{ partial "music" . }}
```

(3)直接在music.html中添加,歌曲的分布结构如下:
```javascript
music[
	{
		name:' ',
		artists:' ',
		url:' ',
		cover:' '
		lrc:' ',
	},
	{
		name:' ',
		...
	}
]
```
一首歌曲的信息在一对`{ }`中,其中的字段分别是**歌曲名,歌手,歌曲链接,封面,歌词**

歌词可以自己决定是否显示,将`showlrc: true`,改成`false`即可.详细的参数可参考[官方文档](https://aplayer.js.org/#/zh-Hans/)

#### 歌曲外链寻找

你可能会为歌曲的那几个参数为难,推荐[一个网站](http://www.guqiankun.com/tools/music/?source=music163)

将网易云网页版的歌曲链接填入即可生成歌曲外链


<center>·end·</center>

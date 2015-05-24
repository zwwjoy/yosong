<h1 align="center">音乐消除国界，下载废除权限：歌曲地址解析器 yosong</h1>
yangyangwithgnu@yeah.net  
http://yangyangwithgnu.github.io/  
2015-05-24 22:29:16


##谢谢

**捐赠：支付宝 yangyangwithgnu@yeah.net 。支付宝链接 https://shenghuo.alipay.com/send/payment/fill.htm?optEmail=yangyangwithgnu@yeah.net ，支付宝二维码 $_$**
<div align="center">
<img src="https://raw.githubusercontent.com/yangyangwithgnu/yangyangwithgnu.github.io/master/pics/donate_qr.png" alt=""/><br>
</div>

**二手书**：书，我提高开发技能的重要手段之一，随着职业生涯的发展，书籍也在不断增多，对我而言，一本书最多读三遍，再往后，几乎没有什么营养吸收，这部分书对我已基本无用，但对其他人可能仍有价值，所以，为合理利用资源，我决定低价出售这些书，希望达到两个目的：0）用售出的钱购买更多新书（没当过雷锋的朋友 (๑´ڡ`๑)）；1）你低价购得需要的书（虽然二手）。到 http://yangyangwithgnu.ecvps.net/used_books/used_books.htm 看看有无你钟意的。


##公告

**讨论**：任何意见建议 yangyangwithgnu@yeah.net  

**声明**：歌曲有版权，使用需谨慎。


##版本

**[v0.1.2，修正，2015-05-21]**：专辑列表关键字调整 (￣□￣)。  
**[v0.1.1，修正，2015-05-21]**：专辑列表关键字调整。  
**[v0.1.0，新增，2015-05-10]**：发布初始版本。  


##演示

<div align="center">
<img src="https://github.com/yangyangwithgnu/yosong/blob/master/pics/%E6%BC%94%E7%A4%BA.gif" alt=""/><br />
（解析王菲的歌曲地址）
</div>

##背景

那么，现在情况是这个样子的，我又想下歌了。在很久很久以前，百度音乐上的歌曲存有 128kbps、192kbps、320kbps 三种品质的，当时注册一个普通帐号就可以下载任意品质，在懒惰魔的诱惑下，我写了个叫 biabiamiamia 的程序，帮我下载指定歌手的全部歌曲，那时候，喜欢的歌手基本都被拖到硬盘上了。最近，广播里放了几首新人的歌，邓紫棋版的“黑腹美”很是喜欢，好吧，把 biabiamiamia 翻出来看下还能跑不？我勒个去，完全用不起啊。是当个丑男还是当个懒人呢？好吧，一懒到底，必须得有个程序帮我批量下载。  

现在的百度音乐存有普通品质（128kbps）、高品质（192kbps）、超高品质（320kbps）、无损品质（flac 800+kbps）四种，其中，320 的需要 VIP 帐号才能下载，而 flac 的甚至需要白金 VIP 才能下载，程序必须首先解决帐号权限的问题；另外，之前监管不那么严格的时候，百度音乐提供大量歌曲免费供大家下载，后来百度开始收费，那么相应百度自己需要先购买这些歌曲的版权，对于百度买了版权的歌曲，它当然可以通过收费会员机制盈利，但，未购买版权的歌曲，即便服务器上有现成的资源，也不得提供给会员下载，所以，程序还得解决这类因百度自身版权而无法下载的问题，比如，王菲-《醇经典》-誓言（http://music.baidu.com/song/s/75053f8340854da16d5 ）。  

耽误了我一周乒乓球时光，总算找到了可靠方法，剩下的就是编码实现 yosong，除了上述两个功能外，顺带实现了其它几项，基本上，现在的 yosong 具备了以下能力：  
0）绕开白金收费会员才能下载无损品质歌曲的限制；  
1）绕开百度自身版权问题歌曲而无法下载的限制（即便白金收费会员从官方渠道也无该功能）；  
2）绕开非大陆之外区域无法下载的限制；  
3）一键式全站歌曲下载；  
4）绕开高频访问出现验证码的限制。  

虽然我用了"下载"这个词，但 yosong 并不会为你下载任何歌曲，严格地说，它是个百度歌曲最终下载地址解析工具，就我而言，我会先让 yosong 帮我解析出指定歌手的所有歌曲的 320 码率最终下载地址，然后以专辑为单位丢给迅雷帮我批量下载。  

##源码安装

####『linux』
0）唯一依赖 libcurl，请自行安装；  
1）代码采用 C++11 编写，gcc 版本不低于 4.7.1。  
2）命令行下运行：  
```
$ cd yosong/build/
$ cmake .
$ make && sudo make install
```

####『osX』
先将 build/CMakeLists.txt 中的  
```
TARGET_LINK_LIBRARIES(yosong curl pthread)
```
替换成  
```
TARGET_LINK_LIBRARIES(yosong curl pthread iconv)
```
其他同 linux 构建方法。

##命令行选项

yosong 是一个命令行程序，要用好它，你得先了解几个命令行选项的常识：  
0）--option 'argc'，其中，--option 称之为命令行选项，argc 为命令行参数；  
1）某些命令行参数中可能含有对 shell 有特殊含义的字符（如，后台运行的 &、用于分割符的空格），为避免 shell 误解，通常，应该用英文单引号包裹命令行参数。如，--user 'yangyangwithgnu'；  
2）某些命令行选项可以有多个参数，通常，每个参数单独用英文单引号包裹，参数间用空格分割。如，--album '八度空间' '范特西' '我很忙'；  

yosong 典型的用法：  
```
yosong --user 'yangyangwithgnu' --password 'abcd1234' --artist '伍佰'
```
这样，yosong 就会帮你把歌手伍佰的所有歌曲的 320 码率下载地址解析出来，一是输出在屏幕上、一是保存至 ~/伍佰@HHMMSS.txt 中。  

具体而言，yosong 提供了如下命令行选项。

**--help**  
显示帮助信息。该选项优先级最高，出现该选项时忽略其他所有选项。  
可选。  

**--version**  
显示当前版本信息。该选项优先级仅次 --help  
可选。  

**--user**  
指定百度帐号。普通免费帐号即可，无需白金付费会员帐号。  
必填。  
单参数。  
无默认值。  

**--password**  
指定百度帐号密码。  
必填。  
单参数。  
无默认值。  

**--artist**  
指定歌手名。  
必填。  
单参数。  
无默认值。  

**--album**  
指定专辑名。该专辑必须归属 --artist 指定歌手的，否则无法下载。若未指定该选项则默认下载 --artist 指定的歌手的所有专辑、所有歌曲。若有多张专辑，请空格隔开，如，--album '八度空间' '范特西' '我很忙'。  
可选。  
多参数。  
无默认值。  

**--quality**  
指定歌曲品质。百毒音乐上的歌曲有四种品质：标准品质（128kbps）、高品质（192kbps）、超高品质（320kbps）、无损品质（800+kbps），yosong 依次有四种参数与之对应：128、192、320、flac。如果指定品质不存在，那么依次找 320、192、128、flac 等存在的品质，找到即下。  
必填。  
单参数。  
默认值，320。  

**--ignore-size-lower**  
有些歌曲尺寸太小相应音质就不高，若想忽略小尺寸的歌曲，可以通过该选项指定一个以 MB 为单位的尺寸下限，凡低于该尺寸的歌曲均不下载。注意，0）该选项的参数可以指定小数；1）指定时不用带单位，如，--ignore-size-lower 6 而非 --ignore-size-lower 6M；2）如果不在乎歌曲尺寸可以将该选项指定为 0。  
必填。  
单参数。  
默认值，6。  

**--path**  
指定歌曲最终下载地址保存路径，文件命名规则：artistname\@hhmmss.txt。  
必填。  
单参数。  
默认值，~/  

##FQA

**Q0**：yosong 可以解析哪些歌手的歌曲？  
**A0**：http://music.baidu.com/artist

**Q1**：为何我昨天解析出的最终下载地址，今天下载全部失败呢？  
**A1**：最终下载地址是有有效期的，要下载时才解析，不要先解析一大堆等多久才下载，很可能过期滴。

**Q2**：yosong 为何不集成下载工具？  
**A2**：我是个受尽 K.I.S.S. 摧残的人儿，术有专攻，让其他第三方专业下载工具去执行具体下载任务吧。当然，我也是个有爱的人儿，帮你准备了  
```
bool Song::download (const string& path, const string& quality, const unsigned timeout);
```
成员函数，它内部集成 aria2c，适当调整下 main.cpp 中的逻辑即可集成下载。我倒是建议直接用迅雷，以专辑为单位把整个专辑的下载地址拷贝下来，迅雷自动除去非 URL 文本，批量下载，并且还能正确给文件命名。

**Q3**：为何有类似“咖哩鱼蛋(1.1MB too small)”红色报错信息？  
**A3**：有些歌曲尺寸太小相应音质就不高，对于您这样有品味的人，宁可不下载也不要被这些低质声音污染耳朵，所以，你可以通过该选项指定一个以 MB 为单位的尺寸下限，告诉 yosong 忽略小于该尺寸的歌曲。如果你是个接受度很广的人，可以将 --ignore-size-lower 设置为 0。  

**Q4**：为何默认品质是 320 而不是无损的 flac？  
**A4**：尼玛，劳资的车载音响不支持 flac 格式 (ง •̀_•́)ง  

**Q5**：为何迅雷下载回来的歌曲出现类似 96892368400320.mp3 这样的文件名？  
**A5**：yosong 解析出来的最终下载地址类似 http://yinyueshiting.baidu.com/data2/music/51503996/96892368400320.mp3?xcode=0518d0d4beb3be2fea45adb97777a278d990c3a07c5eb44d ，通常来说，下载工具会向资源提供服务端查询文件名，然后再下载，迅雷在这方面做得不错，但如果你向单个资源服务器同时发起大量并行查询，其中某几个可能查询失败，所以就出现迅雷按 URL 中的信息给文件命名的情况。要规避这种情况，你可以减少并行下载任务数量（4 个为宜），或者，对已经下载的文件，右键查看音频属性，那儿会有正确的歌曲名，如下图：
<div align="center">
<img src="https://github.com/yangyangwithgnu/yosong/blob/master/pics/%E9%9F%B3%E9%A2%91%E5%B1%9E%E6%80%A7%E5%90%AB%E6%9C%89%E6%96%87%E4%BB%B6%E5%90%8D.gif" alt=""/><br />
（音频属性中提取真实文件名）
</div>

**Q6**：周杰伦的歌明显不全嘛？  
**A6**：对于百度未收录的歌曲资源，yosong 无能为力。  

**Q7**：yosong 要求输入百毒帐号，安不安全？  
**A7**：不安全。我可能把持不住用你的帐号干各种邪恶、抑郁以及不纯洁的事。为了您一身的英明，建议你注册个小号，明白我的意思了么，亲爱的。  

**Q8**：yosong 是否具备“一键”解析百毒音乐全站歌曲的能力？  
**A8**：哼哼哼，好像、或许、应该、我觉得，是具备的。你知道，只需指定歌手名，yosong 能解析该歌手的所有专辑的所有歌曲，同时，yosong 又能遍历出所有歌手，所以，只需增加八行代码即可，具体是 ...，等下，我接个电话先，010-65232656 打来的 ...  

**Q9**：我指定下载 flac 这种无损品质，为何 yosong 下载回来的是 mp3 格式呢？  
**A9**：百毒音乐上的歌曲含有标准品质（128kbps）、高品质（192kbps）、超高品质（320kbps）、无损品质（800+kbps）等四种品质，前三者为 mp3 格式、最后一种为 flac 格式。大部分歌曲四种品质都有，少部分歌曲缺失某类品质，如果指定品质不存在，那么 yosong 依次查找 320、192、128、flac 等存在的品质，找到即下，所以，如果你指定的是 flac 而下载回来的是 mp3，那肯定是该歌曲缺失 flac 品质。至于说，在指定品质不存在时，查找优先级为何把 flac  排在最后，前面说过了，那是因为劳资的车载音响不支持 flac 格式，基本上，我只下载 320 品质的 mp3，如果某歌曲没有 320 的，我希望下载 192 的，而不是“自作聪明”下 flac 的。  

**Q10**：yosong 最小只能以专辑为单位下载，如果我只想下载单首歌曲，咋办啊？  
**A10**：请在门外帮我把门关上。  

**Q11**：非正常退出 yosong 有无危害？  
**A11**：yosong 通过某些机制绕开百度限制，其中涉及把歌曲加入收藏，收藏夹有收藏歌曲数量的限制（8K），虽然 yosong 会自动清理由它加入收藏的歌曲，但，当非正常退出时，清理这步可能未执行，所以，建议定期到 http://yinyueyun.baidu.com/ 手工清理收藏夹，否则，yosong 无法正常运行。  

##接下来你可以

yosong 不是终点，而是你的起点，基于它你可以：  
0）调用 Song::download() 集成 aria2c 下载工具；  
1）创建 GUI 版本，为害怕 CLI 的亲们带去曙光；  
2）创建网站版本，yosong 在幕后，提供歌曲下载地址解析，类似硕鼠网；  
3）移植 windows 版本。

##最后的一定是最不重要的

根据中华人们共和国映像制品版权法第四章第十六条规定，所有歌曲从下载之日起 128 年内务必删除，否则一切后果自负。钦此！

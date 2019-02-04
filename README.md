網路電台
===

如果需要網路電台來轉播聚會或活動，可以參考本文步驟。

## 需要準備什麼？

* 一台足夠運行 [icecast](https://icecast.org) 的機器。
* 建立、管理 docker 的基本知識（如果沒有後續管理需要，或只是臨時活動，可以直接運行本範例即可）。
* 支援所使用平台的轉播軟體。

## 步驟

1. 選擇一個順手的 icecast docker images，以下這些都可以。（[moul/icecast](https://hub.docker.com/r/moul/icecast)、[infiniteproject/icecast](https://hub.docker.com/r/infiniteproject/icecast)），本範例以 [moul/icecast](https://github.com/moul/docker-icecast) 來說明。（如果你對於技術細節有興趣，可以參考[這裡](https://blog.sylee.tw/play-icecast-and-those-tear)。）
2. 安裝並運行 [docker](https://docs.docker.com/install/)。
3. 執行以下指令啟用 icecast 伺服端，你可能會需要修改的是 **ICECAST_SOURCE_PASSWORD（轉播端的密碼）** 以及 **ICECAST_ADMIN_PASSWORD（管理者密碼）**

```
docker run -p 8000:8000 -e ICECAST_SOURCE_PASSWORD=aaaa -e ICECAST_ADMIN_PASSWORD=bbbb moul/icecast
```

4. 如果你需要修改更多設定，可以參考 [icecast.xml](https://github.com/moul/docker-icecast/blob/master/etc/icecast2/icecast.xml)，並改用以下的指令：

```
docker run -p 8000:8000 -v /local/path/to/icecast.xml:/etc/icecast2/icecast.xml moul/icecast
```

5. 以上，成功運行之後即完成 icecast 伺服端的設定，接著就可以把聚會或活動的音源串流至設定好的 icecast 伺服器位置。
6. 接下來針對自己所使用的平台，選擇一款對應的支援串流的軟體。[icecast 的網站](http://icecast.org/apps/)有一些推薦的軟體可以挑一款順手的軟體來使用。個人推薦 [Audio Hijack]()(For MacOS) 以及 [butt](http://danielnoethen.de/)(For Win)。

**Audio Hijack setting**
可以參考[這篇文章](https://weblog.rogueamoeba.com/2018/06/28/migrating-your-broadcast-from-nicecast-to-audio-hijack/)，把連線改成上面架設好的域名跟帳號即可。
![](https://i.imgur.com/vukR09G.png)

**butt setting**
![butt](https://i.imgur.com/kazeM0i.png)
![butt connection](https://i.imgur.com/rPlpVC7.png)

7. 所有設定已完成，直接用瀏覽器點開廣播的位址（mountpoint）即可。

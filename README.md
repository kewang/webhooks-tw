# webhooks-tw

## 什麼是 WebHooks？

WebHooks 的概念很簡單，其實就是 HTTP 版本的 callback：當某件事發生時，就送出一個 HTTP POST 的請求；也可以稱為是透過 HTTP POST 請求的事件通知簡易版。

在 Web 應用程式上實作 WebHooks，就是當特定事物產生時發送一個 HTTP POST 的請求，裡面會夾帶一個訊息並送到某個特定的網址。當這個應用程式開放使用者註冊他們自己的網址時，這些使用者就可以擴充、客製化及整合這個應用程式到他們自己的擴充服務，甚至是網路上的其他 Web 應用程式。對使用者來說，_當 WebHooks 發生時_，它真的是一個獲得具有價值資訊的方式，而不像以前要持續地透過輪詢的方式來取得資訊，更何況這些資訊在絕大部分時間是沒有價值的。WebHooks 具有極大的潛力，只有你的想像力才有可能限制你自己！(當然，它還沒辦法幫你洗碗。)

WebHooks 意思就是拿來 _做_ 一些事。為了讓 _你_ 的 Web 應用程式更能程式化，下面分成三個較常見的 WebHooks 型式。

### 推送服務：即時取得資料

「推送服務」是用 WebHooks 最簡單的理由之一。如前所述，不用再透過每分鐘輪詢的方式確認是否有新資訊。只要註冊 WebHook 之後，有新資料時就會馬上知道。這不需要花太多工夫，也一點都不麻煩，而且你會發現取得資訊的速度比以前每分鐘用輪詢的方式要快多了。

### 管線服務：取得資料然後送給其他服務

WebHook 不只可以用來傳遞即時資料，也可以用這份資料觸發一些與原本事件無關的動作，這就叫做「管線服務」。比如說可以註冊 WebHook 到相簿網站上，然後當你老媽上傳一張新相片到網站上就發電子郵件通知你。或是當你在你的電商網站新增了一個新商品時，即時透過 Twitter 發一則新訊息推銷出去。

### 外掛程式：處理資料後將資料返回

這就是把整個網路服務變成一個可程式化的平台。可以讓其他使用者用外掛程式來擴充你的應用程式。Facebook Application Platform 及 Google Wave 就是用這種方式來整合他們自己的服務。作法就是將 Web 應用程式的資料透過 WebHooks 送出去，然後把 response 取回來改變自己的資料。以 Facebook 為例，當你要存取 Facebook 上的某個應用程式時，Facebook 會送出一個 WebHook 並且通知應用程式「哈囉，有人要存取你的應用程式囉，我該怎麼做才好？」，應用程式就會請 Facebook 把使用者的資訊顯示在這一頁。而 Google Wave 則是當你在 wave 上面做任何動作時，你所加入的所有機器人協作者都會透過 Webhook 的方式收到通知，而且機器人可以變更這個 wave 的 response。如果你想要允許其他使用者合法地擴充且增加 Web 應用程式時，用「外掛程式」來處理是一個比較好的方式。

## WebHook 的運作方式為何？

Web 應用程式可以讓使用者自行將特定網址關聯到各種事件，當事件發生時應用程式就會將資料使用 POST 的方式傳送給這些特定網址。而現在許多便宜的 PHP 主機甚至可以使用 AppJet 或 Scriptlets 這類腳本語言，讓 POST 資料變的更簡單。你要如何做這些事情一切都由你自己決定，除此之外你也可以完成下列各種動作：

* 透過電子郵件、聊天室產生提醒給你
* 發送資料到另一個應用程式 (即時資料同步)
* 處理資料而且重新用 API 發送這些資料到另一個應用程式
* 驗證且保護這些資料，防止被其他應用程式所使用

## 為什麼我應該要開始在意 WebHook？

我們開始察覺網路也可以做整合，大部分的 Web 應用程式到現在都還是閉門造車，自己玩自己的。再加上 API 的盛行，我們看到許多混搭及互相整合的應用程式。但是我們還沒發現可程式化網路的美景：一個可以讓使用者在 Web 應用程式之間傳送資料的網路，就像是 Unix 命令列模式一樣。有些人說 RSS 就是解答，**但是他們錯了**。RSS 的核心價值沒錯，但是實作方式是錯的。RSS 還是非常有用，但它沒辦法幫我們帶來一個真正的可程式化網路。

我們只需要一個簡便的方式讓使用者能夠很簡單地即時取得他們想要的任何資料。這表示不用輪詢機制、沒有任何內容限制，也不需解析 XML。這表示答案根本就不是 RSS。HTTP 愈來愈簡易使用。PHP 是一個非常受歡迎而且容易取得的程式開發環境，所以非常適合用來撰寫 hooklets，在 PHP 上面從 POST 請求取得資料就像取得 `$_POST['something']` 一樣簡單。而且建立一個請求到使用者的腳本就跟建立一個 HTTP 請求一樣簡單，在大部分的程式開發環境也都已經內建了。事實上，Web hooks 比實作 API 還要簡單。

不過在實作上有了對網路的**輸出**將會與愈來愈多人採納的 API 所提供的**輸入**資料互補。當你有了輸入及輸出的資料時，你就有了所有可以與應用程式互動的東西。這會促進更小、更專注特定功能的應用程式與開啟 webhook 的多樣化應用程式一起協作，這會讓許多令人驚豔且新興的事件發生！

## WebHooks 應該如何實作？

只要你的使用者可以簡易的將他們的網址送到你的應用程式，而且當某個事件發生時可以把資料使用 POST 請求送到這個網址就行了。非常簡單。不必遵循什麼特定的規格。

### 真的沒有規格！？

到目前為止還沒有一個針對 WebHooks 的標準，現在有許多組織正在定義指南，或許有一天這些指南會逐步形成一個標準。這每個標準都應該可以用在不同的需求，或是簡單及廣泛的實作。大家可以看看下面這個對不同建議及實作指南的網頁，而且一定要把你的意見或經驗分享給我們。如果你在使用這些建議有一些不好的體驗，或是你覺得這些建議可以做一些調整的時候，快加入這個對話串一起來改善這份規格吧！

* [RESTful WebHooks](https://webhooks.pbworks.com/w/page/13385128/RESTful%20WebHooks)

## 誰在使用 web hooks？

已經有許多人使用過 web hooks 了。有些是有意識地，有些是出於實用主義。這通常是一個不錯的信號。讓我們一起來加入這個派對加強這個模式吧。

* [Assembla](http://www.assembla.com/spaces/demostuff/webhook_tool) (project tracking)
* [BitBucket](http://www.bitbucket.org/) (mercurial commit notifications)
* [CallMyApp](http://callmyapp.com/) (API-based cron callback service)  
* DevjaVu
* Facebook App Platform (sort of)
* [Femtoo](http://www.femtoo.com/) (content tracking and notification)
* [FreshBooks](http://developers.freshbooks.com/blog/view/keep_in_sync_with_freshbooks_webhooks/) (accounting)
* [GitHub](http://github.com/guides/post-receive-hooks) (git push notification)
* [Google Code](http://code.google.com/p/support/wiki/PostCommitWebHooks)
* Jott
* [IMified](http://new.imified.com/developers/api)
* [LiveDirectory.org](http://livedirectory.org/) (Next generation web - subscription & notification service)
* Mailhook.org, SMTP2Web, Astrotrain
* [Notifixious](http://notifixio.us/)
* [Papertrail](http://papertrailapp.com/) (syslog & app log [events](http://help.papertrailapp.com/kb/how-it-works/web-hooks))
* PayPal ([IPN](https://www.paypal.com/ipn))
* PBwiki
* [ProjectLocker](http://blog.projectlocker.com/articles/2009/11/09/webhooks-land-at-projectlocker) (git/svn commit notification)
* [Shopify](http://wiki.shopify.com/WebHook) (hosted shopping cart)
* [Spinn3r](http://spinn3r.com/)
* [SurveyGizmo](http://www.surveygizmo.com/survey-blog/communicate-external-database-http-post/)
* [Twilio](http://www.twilio.com/) (phone calls)
* [Versionshelf](http://www.versionshelf.com/)
* [Wufoo](http://wufoo.com/2010/02/16/setup-webhooks-in-wufoo-to-get-push-notifications-to-your-apps/) (Web forms)
* [ZenDesk](http://www.zendesk.com/api/targets) (ticketing)
* 你？

### 誰應該使用 web hooks？

* 線上應用程式平台
    * DabbleDB
    * Coghead
    * Salesforce
    * Ning
* 記得訂過的牛奶 (我只是想要擴展我使用的 todo 應用程式)
* Twitter (可以用在任何地方)
* 任何人...

有一些甚至開始嘗試把 webhooks 用在桌面應用程式上了。

## 投影片

* [Web Hooks](http://www.slideshare.net/progrium/web-hooks) - 我在許多地方分享過這個投影片
* [Web Hooks on PBwiki](http://www.slideshare.net/guest7e115a/web-hooks-on-pbwiki) - 南森在 PBwiki 針對如何實作 web hooks 的報告
                    
## 有哪些人流行

* [GetPingd](http://groups.google.com/group/getpingd)
* [Gnip](http://www.gnipcentral.com/)
* [Joshua Schachter](http://joshua.schachter.org/2008/07/beyond-rest.html)

## 進一步閱讀

* [Web hooks](http://blogrium.com/?p=70) - 在 2006 年 8 月最原始關於談論 web hooks 的文章
* [Let's make seeking bliss easier](http://blogrium.com/2006/11/27/lets-make-seeking-bliss-easier/) - 一個大聲嚷嚷說要用 web hooks 及其他點子建置網路的文章
* [Automator for the web](http://blogrium.com/2006/12/27/automator-for-the-web/) - 可以用 WebHooks 帶我們去任何地方的文章

你也可以持續關注 [webhooks.org](http://webhooks.org/) 這個網站，取得更多關於 web hooks 的最新資訊，或是上 [Google Group](http://groups.google.com/group/webhooks) 一起討論吧！

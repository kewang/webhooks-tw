# webhooks-tw

## 什麼是 WebHook？

WebHook 的概念很簡單，其實就是 HTTP 的 callback，當事件發生時，就送出一個 HTTP POST 的 request。

在 Web 應用程式上實作 WebHooks，就是當特定事物產生時發送一個 HTTP POST 的請求，裡面會夾帶一個訊息並送到某個特定的網址。當這個應用程式開放使用者註冊他們自己的網址，這些使用者就可以擴充、客製化及整合這個應用程式到他們自己的擴充服務，甚至是網路上的其他 Web 應用程式。對使用者來說，WebHooks 是一個獲得具有價值資訊的方式，而不像以前要持續地透過輪詢的方式來取得資訊，更何況這些資訊在絕大部分時間是沒有價值的。WebHooks 具有極大的潛力，只有你的想像力可以限制你自己。

WebHooks 意思就是拿來做一些事。為了讓你的 Web 應用程式更能程式化，下面分成三個較常見的 WebHooks 型式。

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

我們只需要一個簡便的方式讓使用者能夠很簡單地即時取得他們想要的任何資料。這表示不用輪詢機制、沒有任何內容限制，也不需解析 XML。這表示答案根本就不是 RSS。HTTP 愈來愈簡易使用。PHP 是一個非常受歡迎而且容易取得的程式開發環境，所以非常適合用來撰寫 hooklets，在 PHP 上面從 POST 請求取得資料就像取得 $_POST['something'] 一樣簡單。而且建立一個請求到使用者的腳本就跟建立一個 HTTP 請求一樣簡單，在大部分的程式開發環境也都已經內建了。事實上，Web hooks 比實作 API 還要簡單。

          We just need a simple way to get data out in real-time to let the user easily do whatever they want with it. That means no polling, no content constraints, and no XML parsing. That means no RSS. Using HTTP is simpler and easier to use. PHP is a very popular and accessible programming environment, so it's likely to be used often for writing hooklets... getting data from a web POST in PHP is as simple as $_POST['something']. And making the request to the user script is as simple as making an HTTP request, something already built-in to most programming environments. In fact, web hooks are easier to implement than an API.

           

           However implemented (although the easier the more likely it will be adopted), having an output for the web will complement the input provided by the rising adoption of API's. When you have both input and output, you have everything you need for apps to easily interact. This will encourage smaller, more focused apps that together with hook-enabled heavier apps will let amazing emergent creations happen!

            

            How do I implement WebHooks?
            Simply provide your users with the ability to submit their own URL, and POST to that URL when something happens. It's that simple. There are no specs you have to follow.

             

             No Specs?!
             While there are currently no standards defined for WebHooks, there are groups working to define guidelines that may one day evolve into standards. Each of these standards should apply to different types of needs, or lighter vs comprehensive implementations. Check out the following pages for various suggestions and implementation guidelines, and be sure to share your opinion/experience with us. If you have a bad experience with one of these suggestions, or you had to tweak your design a bit, then join in the conversation to improve the spec!

              

              RESTful WebHooks
               

               Who is using web hooks?
               A number of people have started using web hooks. Some consciously, some out of pragmatism. And that's a good sign. Let's reinforce this pattern... implement web hooks and join this party.

                

                Assembla (project tracking)
                BitBucket (mercurial commit notifications)
                CallMyApp (API-based cron callback service)  
                DevjaVu
                Facebook App Platform (sort of)
                Femtoo (content tracking and notification)
                FreshBooks (accounting)
                GitHub (git push notification)
                Google Code
                Jott
                IMified
                LiveDirectory.org (Next generation web - subscription & notification service)
                Mailhook.org, SMTP2Web, Astrotrain
                Notifixious
                Papertrail (syslog & app log events)
                PayPal (IPN)
                PBwiki
                ProjectLocker (git/svn commit notification)
                Shopify (hosted shopping cart)
                Spinn3r
                SurveyGizmo
                Twilio (phone calls)
                Versionshelf
                Wufoo (Web forms)
                ZenDesk (ticketing)
                you?
                 

                 Who should be using web hooks?
                 Online application platforms
                 DabbleDB
                 Coghead
                 Salesforce
                 Ning
                 Remember the Milk (I just want to extend the todo app I use)
                 Twitter (wants to anyway)
                 Everybody...
                  

                  Some are even dabbling with implementing webhooks into Desktop applications.

                   

                   Presentations
                   Web Hooks - Slides and notes to a presentation I gave several places
                   Web Hooks on PBwiki - Nathan's report on implementing web hooks on PBwiki
                    

                    People catching on
                    GetPingd
                    Gnip
                    Joshua Schachter
                     

                     Further reading
                     Web hooks - The original post about web hooks in August 2006
                     Let's make seeking bliss easier - A followup rant building on web hooks and other ideas
                     Automator for the web - Where some of this stuff can go
                      

                      Also check out webhooks.org for more up to date information on web hooks or the Google Group for discussion!

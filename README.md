# webhooks-tw

## 什麼是 WebHook？

WebHook 的概念很簡單，其實就是 HTTP 的 callback，當事件發生時，就送出一個 HTTP POST 的 request。

在 Web 應用程式上實作 WebHooks，就是當特定事物產生時發送一個 HTTP POST 的請求，裡面會夾帶一個訊息並送到某個特定的網址。當這個應用程式開放使用者註冊他們自己的網址，這些使用者就可以擴充、客製化及整合這個應用程式到他們自己的擴充服務，甚至是網路上的其他 Web 應用程式。對使用者來說，WebHooks 是一個獲得具有價值資訊的方式，而不像以前要持續地透過輪詢的方式來取得資訊，更何況這些資訊在絕大部分時間是沒有價值的。WebHooks 具有極大的潛力，只有你的想像力可以限制你自己。

WebHooks 意思就是拿來做一些事。為了讓你的 Web 應用程式更能程式化，這裡總共分成三個較常見的 WebHooks 型式：

* 推送服務：即時取得資料

推送服務是用 WebHooks 最簡單的理由之一。如前所述，不用再透過每分鐘輪詢的方式確認是否有新資訊。只要註冊 WebHook 之後，收到資料時你馬上就會知道了。這不需要花太多工夫，也一點都不麻煩，而且你會發現取得資訊的速度比你以前每分鐘用輪詢的方式要快多了。

* 管線服務：取得資料然後送給其他服務

     Pipes: receiving data and passing it on
     A Pipe happens when your WebHook not only receives real-time data, but goes on to do something new and meaningful with it, triggering actions unrelated to the original event. For example, you create a script, register its URL at a photo site, and have it email you when your mother posts a new photo. Or make a script that creates a Twitter message, and have it triggered by a WebHook whenever you add a new product on your commerce website.

      

      Plugins: processing data and giving something in return
      This is where the entire web becomes a programming platform. You can use this form of WebHooks to allow others to extend your application. Facebook's Application Platform uses WebHooks in this way, and so does Google Wave's robot integration. The general idea is that a web application sending out data via WebHooks will also use the response to modify its own data. At Facebook, when you access an app, Facebook sends a WebHook out to your application saying "Hey, someone's accessing your application, what do I do?!" The application responds with, "Show the user this page..." Facebook does so, and the pattern continues in the same manner as you continue to use the application. At Google Wave, when you do something in a wave, any robot you've added as a participant is notified via a WebHook, and the robot has the ability to modify the wave in its http response. Implement WebHooks in this way in your application if you want to allow others to truly extend and enhance the abilities of your application.

       

       How do they work?
       By letting the user specify a URL for various events, the application will POST data to those URLs when the events occur. With the cheap availability of PHP hosting and even easier simple app/script hosting like AppJet or Scriptlets, handling the POST data becomes fairly trivial. How you use it is up to you and whatever you want to accomplish. Among other things, you can:

        

        create notifications to you or anybody via email, IRC, Jabber, ...
        put the data in another app (real-time data synchronization)
        process the data and repost it using the app's API
        validate the data and potentially prevent it from being used by the app
         

         Why should I care?
         As integrated as we perceive the web, most web applications today operate in silos. With the rise of API's we've seen mashups and some degree of integration between applications. However, we have not seen the vision of the programmable web: a web where you as the user can "pipe" data between apps much like the Unix command line. Some say RSS is the answer. They are wrong. The heart is in the right place, but the implementation is wrong. RSS is still useful, but it is not going to bring us the true programmable web.

          

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

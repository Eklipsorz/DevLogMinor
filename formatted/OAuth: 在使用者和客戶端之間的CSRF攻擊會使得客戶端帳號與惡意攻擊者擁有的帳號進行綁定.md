- 
- 
- [@6HGXA7MH](<@6HGXA7MH.md>)
- > 对于 CSRF 的定义，《OAuth 2 in Action》这本书里的解释，是我目前看到的最为贴切的解释：恶意软件让浏览器向 已完成用户身份认证 的网站发起请求，并 执行有害的操作，就是跨站请求伪造攻击。
- 
- >  有一个软件 A，我们让它来扮演攻击者，让它的开发者按照正常的流程使用授权码。当该攻击者授权后，拿到授权码的值 codeA 之后，「立即按下了暂停键」，不继续往下走了。那它想干啥呢，我们继续往下看。
- > 这时，有一个第三方软件 B，比如咱们的 Web 版极客时间，来扮演受害者吧。 当然最终的受害者是用户，这里是用 Web 版极客时间来作为被软件 A 攻击的对象。
- > 极客时间用于接收授权码的回调地址为 https://time.geekbang.org/callback。有一个用户 G 已经在极客时间的平台登录，且对极客时间进行了授权，也就是 用户 G 已经在极客时间平台上有登录态了。
- > 如果此时攻击者软件 A，在自己的网站上构造了一个恶意页面：
- ```html
<html>
  <img src ="https://time.geekbang.org/callback？code=codeA">
</html>```
- 
- > 如果这个时候用户 G 被攻击者软件 A 诱导而点击了这个恶意页面，那结果就是，极客时间使用 codeA 值去继续 OAuth 2.0 的流程了。这其实就走完了一个 CSRF 攻击的过程，如下图所示：
- 
- ![](https://zq99299.github.io/note-book/assets/img/f12446c76ffcbb58b8ce00c3f874f8fe.f12446c7.png)
- 
- > 如果我们将 OAuth 2.0 用于了身份认证，那么就会造成严重的后果，因为用户 G 使用的极客时间的 授权上下文环境 跟攻击者软件 A 的 授权上下文环境 绑定在了一起。为了解释两个上下文环境绑定在一起可能带来的危害，我们还是拿极客时间来举例。
- > 假如，极客时间提供了用户账号和微信账号做绑定的功能，也就是说用户先用自己的极客时间的账号登录，然后可以绑定微信账号，以便后续可以使用微信账号来登录。在绑定微信账号的时候，微信会咨询你是否给极客时间授权，让它获取你在微信上的个人信息。这时候，就需要用到 OAuth 2.0 的授权流程。
- > 如果攻击者软件 A，通过自己的极客时间账号事先做了上面的绑定操作，也就是说攻击者已经可以使用自己的微信账号来登录极客时间了。那有一天，软件 A 想要「搞事情」了，便在发起了一个授权请求后构造了一个攻击页面，里面包含的模拟代码正如我在上面描述的那样，来诱导用户 G 点击。
- > 而用户 G 已经用极客时间的账号登录了极客时间，此时正要去做跟微信账号的绑定。如果这个时候他刚好点击了攻击者 A 「种下」的这个恶意页面，那么后面换取授权的访问令牌 access_token，以及通过 accces_token 获取的信息就都是攻击者软件 A 的了。
- 
- > 这就相当于，用户 G 将自己的极客时间的账号跟攻击者软件 A 的微信账号绑定在了一起。这样一来，后续攻击者软件 A 就能够通过自己的微信账号，来登录用户 G 的极客时间了。这个后果可想而知。
- 
- 
- ---
- [@MEFH42TI](<@MEFH42TI.md>)
- 
- > 让我们来看一个针对OAuth2的CSRF攻击的例子。假设有用户张三，攻击者李四，第三方Web应用Tonr（它集成了第三方社交账号登录，并且允许用户将社交账号和Tonr中的账号进行绑定），以及OAuth2服务提供者Sparklr。
- ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1701175368/blog/OAuth/csrf-example/csrf-example1_yizlsw.png)
- 
- ```javascript
Step 1. 攻击者李四登录Tonr网站，并且选择绑定自己的Sparklr账号
Step 2. Tonr网站将李四重定向到Sparklr，由于他之前已经登录过Sparklr，所以Sparklr直接向他显示是否授权Tonr访问的页面
Step 3. 李四在点击”同意授权“之后，截获Sparklr服务器返回的含有Authorization code参数的HTTP响应
Step 4. 李四精心构造一个Web页面，它会触发Tonr网站向Sparklr发起令牌申请的请求，而这个请求中的Authorization Code参数正是上一步截获到的code
Step 5. 李四将这个Web页面放到互联网上，等待或者诱骗受害者张三来访问
Step 6. 张三之前登录了Tonr网站，只是没有把自己的账号和其他社交账号绑定起来。在张三访问了李四准备的这个Web页面，令牌申请流程在张三的浏览器里被顺利触发，Tonr网站从Sparklr那里获取到access_token，但是这个token以及通过它进一步获取到的用户信息却都是攻击者李四的。
Step 7. Tonr网站将李四的Sparklr账号同张三的Tonr账号关联绑定起来，从此以后，李四就可以用自己的Sparklr账号通过OAuth登录到张三在Tonr网站中的账号，堂而皇之的冒充张三的身份执行各种操作。
```
- 
-  
- ### > 2.2 受害者张三(Resource Owner)视角
    - > 受害者张三访问了一个Web页面，然后，就没有然后了，他在Tonr网站上的账号就和攻击者李四在Sparklr上的账号绑定到了一起。伪造的请求是经过精心构造的，令牌申请这一过程在张三的浏览器里是非常隐蔽的被触发的，换句话讲就是，他根本不知道这背后发生了什么。
- 
- > 2.3 Tonr网站(Client)视角
    - > 从Tonr网站来看，它收到的所有请求看上去都是正常的。首先它收到了一个HTTP请求，其代表着当前用户张三在Sparklr网站上已经做了“同意授权”操作。其内容如下：
    - ```javascript
GET /bindingCallback?code=AUTHORIZATION_CODE```
    - > 不过需要注意的是，URL里的code不是当前受害者张三的Authorization Code，而是攻击者李四的。 当Tonr收到这样的请求时，它以为张三已经同意授权（但实际上这个请求是李四伪造的），于是就发起后续的令牌申请请求，用收到的Authorization Code向Sparklr换取access_token，只不过最后拿到的是攻击者李四的 access_token。
- 
- > 2.4 Sparklr网站(OAuth2服务提供者)视角
    - > Sparklr网站也是一脸茫然的样子，因为在它看来，自己收到的授权请求，以及后续的令牌申请请求都是正常的，或者说它无法得知接收到的这些请求之间的关联关系，而且也无法区别出这些请求到底是来自张三本人，还是由李四伪造出来的。因此只要自己收到的参数是正确有效的，那就提供正常的认证服务，仅此而已。
- 
- > 2.5 攻击者李四视角
    - >  李四伪造了一个用户授权成功的请求，并且将其中的Authorization Code参数替换成了自己提前获取到的code。这样，当受害者的浏览器被欺骗从而发起令牌申请请求时，实际上是在用张三在Tonr网站上的账号和李四在Sparklr网站上的账号做绑定。
    - > 攻击完成后，李四在Tonr网站上可以通过自己在Sparklr网站的账号进行登录，而且登录进入的是张三在Tonr网站上的账号。而张三通过自己在Tonr网站上的账号登录进去之后，看到的是李四在Sparklr网站上的数据。
- 
- >　2.6 上帝视角
- ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1701175764/blog/OAuth/csrf-example/csrf-example-grant-flow_jhlayb.png)
- 
- ---
- 
- 
- 
- 
- 
- 重點:
- 在客戶端和使用者之間的CSRF 攻擊主要是讓瀏覽器向已完成使用者身分驗證的網站發起請求，並執行惡意操作。
- 主要案例為:
- CSRF攻擊會使得客戶端帳號與惡意攻擊者擁有的帳號進行綁定
    - 該攻擊中會有1個Resource Owner、1個Client、1個以上Authorization Server
    - 在這裡Client的帳號認證系統除了自己本身擁有以外，還能從外部認證系統來登入Client，外部認證系統如Google、FB、IG，在這裡Client提供一個功能:能讓自身帳號認證系統的任一帳號與外部認證系統的任一帳號進行綁定，換言之，可以直接使用外部認證系統來連接自身帳號認證系統的帳號所擁有的資料
        - 讓自身帳號認證系統的任一帳號與外部認證系統的任一帳號進行綁定 的實現思路:
            - 當瀏覽器和客戶端(應用程式)間儲存著使用者帳號已登入的認證結果，如客戶端儲存的session id，客戶端(應用程式)端儲存的session 內容-使用者帳密。 
            -  定義用來定義目前帳號要與外部認證系統的任一帳號進行綁定的端點、http動詞、夾帶的參數
                - 格式為: code為外部認證系統所授權同意的回傳結果，bindingCallback表明要做綁定
                - ```html
GET client_uri/bindingCallback?code=codeA```
            - 當瀏覽器和伺服器間儲存著使用者帳號已登入的認證結果，或者說兩邊正儲存著正在登入的狀態，在這情況下，若瀏覽器發出以上請求的話，就會在頒發token的過程讓目前處於登入狀態的帳號與目前外部認證系統頒發的code所對應的帳號進行綁定
    - 在這裡client並沒辦法區分出code是否為惡意攻擊者? 還是合法使用者? 所以只要在瀏覽器保持著客戶端本身有的帳號A登入狀態且該帳號A並未做綁定的情況下，讓瀏覽器發送出以下請求，就會自動將code對應的任一使用者與帳號A進行綁定，即使code是惡意使用者亦是如此。
    - ```html
GET client_uri/bindingCallback?code=codeA```
- ---
- [Test](<Test.md>) OAuth : 發生在客戶端和使用者間的CSRF攻擊主要是甚麼?
    - 攻擊主要是讓瀏覽器向已完成使用者身分驗證的網站發起請求，並執行惡意操作
- [Test](<Test.md>) OAuth: 攻擊主要是讓瀏覽器向已完成使用者身分驗證的網站發起請求，並執行惡意操作，其主要惡意操作的案例會是甚麼?
    - CSRF攻擊會使得客戶端帳號與惡意攻擊者擁有的帳號進行綁定
- 
- [Test](<Test.md>) OAuth CSRF攻擊: 在這裡Client的帳號認證系統除了自己本身擁有以外，還能從外部認證系統來登入Client，外部認證系統如Google、FB、IG，在這裡Client提供一個功能:能讓自身帳號認證系統的任一帳號與外部認證系統的任一帳號進行綁定，那麼CSRF攻擊在這裡會是如何實現?
    - 1). 當瀏覽器和客戶端(應用程式)間儲存著使用者帳號已登入的認證結果，如客戶端儲存的session id，客戶端(應用程式)端儲存的session 內容-使用者帳密.  2). 定義用來定義目前帳號要與外部認證系統的任一帳號進行綁定的端點、http動詞、夾帶的參數.  3). 當瀏覽器和伺服器間儲存著使用者帳號已登入的認證結果，或者說兩邊正儲存著正在登入的狀態，在這情況下，若瀏覽器發出以上請求的話，就會在頒發token的過程讓目前處於登入狀態的帳號與目前外部認證系統頒發的code所對應的帳號進行綁定
- [Test](<Test.md>) OAuth CSRF 攻擊: 假設目前瀏覽器中向Client以內部帳號認證系統進行登入並維持其狀態的使用者為A，且A並未用其他外部認證系統來與帳號進行綁定，假使A在登入狀態下發出 GET client_uri/bindingCallback?code=codeB 該請求，其中CodeB本身就不是源自於A的帳號，請問執行完之後，其結果會是甚麼? 為什麼?
    - 結果是CodeB對應的外部認證帳號會與A所擁有的帳號進行綁定，原因為有兩個: 1. GET client_uri/bindingCallback本身就是以目前處於登入狀態的帳號來綁定Code對應的帳號 2). Client端無法區分出Code所對應的帳號會是合法? 還是非法
- [Test](<Test.md>) OAuth CSRF攻擊: 請問特定Client的帳號要與外部認證系統的帳號進行綁定的話，其請求會是甚麼? 如URL、端點、參數?
    - GET client_uri/bindingCallback?Code=CodeA
- [Test](<Test.md>) OAuth CSRF攻擊: GET client_uri/bindingCallback 與一般Authorization Code Grant Type下的 GET client_uri/Callback 之間有甚麼功能上的差別? 
    - bindingCallback 會與Callback雷同，只是會讓Client索取Token的過程將目前處於登入狀態的內部認證系統帳號與Code對應的外部認證系統帳號進行綁定。 Callback 則是純粹拿著Code來傳送至Client並要求利用Code向Authorization Server索要Token
- 
- [Test](<Test.md>) OAuth CSRF攻擊: 假設張三為受害者，李四為攻擊者，李四製作GET client_uri/bindingCallback?Code=CodeB 請求並放入一個網頁中好讓張三點選，其中CodeB是李四在外部認證系統-Sparklr索或得到的授權碼，而Client則是Tonr，請問當張三點選李四的網頁後，會發生甚麼? 請以時序圖來表示
    - ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1701175764/blog/OAuth/csrf-example/csrf-example-grant-flow_jhlayb.png)
- [Test](<Test.md>) OAuth CSRF攻擊: 假設張三為受害者，李四為攻擊者，李四製作GET client_uri/bindingCallback?Code=CodeB 請求並放入一個網頁中好讓張三點選，其中CodeB是李四在外部認證系統-Sparklr索或得到的授權碼，而Client則是Tonr，請問CodeB一定就是李四沒在Client註冊成功的嗎? 為什麼?
    - 最主要要看Client是否支援將使用者現有帳號所擁有的資料結合至另一個帳號所擁有的資料，若不能，就是以李四未用外部認證系統來註冊的Code來進行；若能的話除了前面所述以外，還有就是可以已註冊但沒登入成功的Code
- 
- ---
- 

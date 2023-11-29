- 
- [@ALLLF49J](<@ALLLF49J.md>)
- 
- > OAuth is all about enabling users to grant limited access to applications. The application first needs to decide which permissions it is requesting, then send the user to a browser to get their permission. To begin the Implicit flow, the application constructs a URL like the following and directs the browser to that URL.
- ```javascript
https://authorization-server.com/auth
 ?response_type=token
 &client_id=29352910282374239857
 &redirect_uri=https%3A%2F%2Fexample-app.com%2Fcallback
 &scope=create+delete
 &state=xcoiv98y3md22vwsuye3kch```
- > Here’s each query parameter explained: 
- ```javascript
- response_type=token - This tells the authorization server that the application is initiating the Implicit flow. Note the difference from the Authorization Code flow where this value is set to code.
  
- client_id - The public identifier for the application, obtained when the developer first registered the application.
- redirect_uri - Tells the authorization server where to send the user back to after they approve the request.
  
- scope - One or more space-separated strings indicating which permissions the application is requesting. The specific OAuth API you’re using will define the scopes that it supports.
  
- state - The application generates a random string and includes it in the request. It should then check that the same value is returned after the user authorizes the app. This is used to prevent CSRF attacks.```
- 
- > When the user visits this URL, the authorization server will present them with a prompt asking if they would like to authorize this application’s request.
- ![](https://developer.okta.com/assets-jekyll/blog/oauth-authorization-code-grant-type/oauth-prompt-48d4b9d76687db5e661fd8f434514d4d4f9136f7a9a7bdc049a93cf8894c653d.png)
- 
- ## Scope 用途
- [@QMCUWFCL](<@QMCUWFCL.md>)
- > The authorization and token endpoints allow the client to specify the
   scope of the access request using the "scope" request parameter.  In
   turn, the authorization server uses the "scope" response parameter to
   inform the client of the scope of the access token issued.
- 
- 
- 細節:
    - 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址格式
        - ```javascript
authorization_server_url/path
?response_type=...
&client_id=...
&redirect_uri=....
&scope=...
&state=...```
    - response_type 主要有兩種用途:
        - 告知Authorization Server 目前Client想使用哪種認證方式
        - Client 要求User從Authorization Server進行授權同意的認證後所要回傳的指定形式
    - scope:
        - 用途1: Client 定義要求甚麼樣的權限
            - Client是可以指定其值並讓User 導向至Authorization Server進行特定權限的認證授權申請
            - Client 可以不用填寫，由使用者或者Authorization Server來決定
        - 用途2: 認證伺服器用來將token擁有的實際權限為何的資訊告知給Client
    - redirect_uri:
        - 用途1: Client指定使用者一旦與Authorization Server完成認證授權後所要導向的端點，通常會是轉送其認證後產物至指定地點
        - 用途2:Client指示使用者哪個地方獲取script，並且該script執行起來會擷取fragment 內容的token並傳遞至client
- 
- 
- ---
- [Test](<Test.md>) 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址格式會是甚麼?
    - ```javascript
authorization_server_url/path
?response_type=...
&client_id=...
&redirect_uri=....
&scope=...
&state=...```
- 
- [Test](<Test.md>) 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址格式中的response_type會有甚麼樣的主要用途?
    - 1. 告知Authorization Server 目前Client想使用哪種認證方式 2. Client 要求User從Authorization Server進行授權同意的認證後所要回傳的指定形式
- 
- [Test](<Test.md>) 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址格式中的scope會有甚麼樣的主要用途?
    - 用途1: Client 定義要求甚麼樣的權限 、用途2: 認證伺服器用來將token擁有的實際權限為何的資訊告知給Client
- [Test](<Test.md>) 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址格式中的redirect_uri會有甚麼樣的主要用途?
    -  Client指定使用者一旦與Authorization Server完成認證授權後所要導向的端點，通常會是轉送其認證後產物至指定地點
- 
- [Test](<Test.md>) 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址格式中的scope寫與沒寫之間的差異為何? 
    - Client是可以指定其值並讓User 導向至Authorization Server進行特定權限的認證授權申請 、Client 可以不用填寫，由使用者或者Authorization Server來決定
- ---
- tags: [OAuth](<OAuth.md>)
- 

# Backlinks
## [OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程](<OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程.md>)
- links: [OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type](<OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type.md>)

## [implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token](<implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token.md>)
- links: [OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type](<OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type.md>)

## [implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client](<implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client.md>)
- links: [OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type](<OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type.md>)


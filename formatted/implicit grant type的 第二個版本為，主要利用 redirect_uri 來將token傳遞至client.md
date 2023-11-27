- [@ALLLF49J](<@ALLLF49J.md>)
- > the flow has the following steps:
 - The application opens a browser to send the user to the OAuth server
 - The user sees the authorization prompt and approves the app’s request
 - The user is redirected back to the application with an access token in the URL fragment```
- 
- 
- > OAuth is all about enabling users to grant limited access to applications. The application first needs to decide which permissions it is requesting, then send the user to a browser to get their permission. To begin the Implicit flow, the application constructs a URL like the following and directs the browser to that URL.
- ```javascript
https://authorization-server.com/auth
 ?response_type=token
 &client_id=29352910282374239857
 &redirect_uri=https%3A%2F%2Fexample-app.com%2Fcallback
 &scope=create+delete
 &state=xcoiv98y3md22vwsuye3kch```
- 
- 
- 
- 
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
- ## Redirect Back to the Application
- 
- > If the user approves the request, the authorization server will redirect the browser back to the redirect_uri specified by the application, adding a token and state to the fragment part of the URL.
- > For example, the user will be redirected back to a URL such as
- ```javascript
https://example-app.com/redirect
  [access_token](<access_token.md>)=g0ZGZmNj4mOWIjNTk2Pw1Tk4ZTYyZGI3
  &token_type=Bearer
  &expires_in=600
  &state=xcoVv98y2kd44vuqwye3kcq```
- 
- > Note the two major differences between this and the Authorization Code flow: the access token is returned instead of the temporary code, and both values are returned in the URL fragment (after the #) instead of in the query string. By doing this, the server ensures that the app will be able to access the value from the URL, but the browser won’t send the access token in the HTTP request back to the server.
- > The state value will be the same value that the application initially set in the request. The application is expected to check that the state in the redirect matches the state it originally set. This protects against CSRF and other related attacks.
- > The server will also indicate the lifetime of the access token before it expires. This is usually a very short amount of time, along the lines of 5 to 10 minutes, because of the additional risk in returning the token in the URL itself.
- > This token is ready to go! There is no additional step before the app can start using it!
- 
- 
- ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679229338/blog/OAuth/OAuth-implicit-version2_euhcgr.png)
- 
- 
- 
- 重點：
- 此為implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client
- 主要流程為：
    - A. 使用者訪問客戶端
    - B. 客戶端將使用者導向認證伺服器進行身份認證、授權詢問
    - C. 使用者同意授權並發送至認證伺服器
    - D. 認證伺服器向使用者發送一個導向URI以及Token
    - E. 使用者藉由導向URI發送token至Client
    - F. Client 透過Token來向資源伺服器索要資源
- ---
- [Test](<Test.md>) redirect_uri 是用來接收token的地點： implicit grant type 在OAuth上的流程為何？ 
    -  `	- A. 使用者訪問客戶端 - B. 客戶端將使用者導向認證伺服器進行身份認證、授權詢問 - C. 使用者同意授權並發送至認證伺服器 - D. 認證伺服器向使用者發送一個導向URI以及Token - E. 使用者藉由導向URI發送token至Client - F. Client 透過Token來向資源伺服器索要資源 - G. 資源伺服器回傳資源至Client`
- 
- [Test](<Test.md>)  redirect_uri 是用來接收token的地點： implicit grant type 在OAuth上的流程為何？ 請畫圖來表示
    -  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679229338/blog/OAuth/OAuth-implicit-version2_euhcgr.png)
- 
-  [Test](<Test.md>) OAuth 2.0 Implicit Grant Type:在直接將token回傳至客戶端的版本下，使用者授權同意之後，伺服器會傳送甚麼樣的URL導向內容來引導使用者至客戶端? 請舉例
    - redirect_uri/redirect[access_token](<access_token.md>)=.....&token_type=....&expires_in=....&state=......
- 
- 
- 
- ---
- tags: [OAuth](<OAuth.md>) [Authorization](<Authorization.md>)
- links: [OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type](<OAuth: 當Client將使用者導向至認證用伺服器進行授權同意的申請時所用到的網址細節 - scope、redirect_uri、response_type.md>)

# Backlinks
## [implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token](<implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token.md>)
- [implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client](<implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client.md>)


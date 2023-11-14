- > ### Implicit Flow
- > The following diagram shows the flow for the Implict grant type:

- 
- > The flow of the Implicit grant type is:
- > 1.  **Access Application**: The user accesses the app and triggers authentication and authorization.
- > 2.  **Authentication and Request Authorization**: The app prompts the user for their username and password. The first time the user goes through this flow for the app, the user sees an approval page. On this page, the user can choose permissions to authorize the app to access resources on their behalf.
- > 3.  **Authentication and Grant Authorization**: The authorization server receives the authentication and authorization grant.
- > 4.  **Issue Access Token**: The authorization server validates the authorization code and returns an access token with the redirect URL.
- > 5.  **Request Resource w/ Access Token in**: The app attempts to access the resource from the resource server by presenting the access token in the URL.
- > 6.  **Return Resource**: If the access token is valid, the resource server returns the resources that the user authorized the app to receive.
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
    - G. 資源伺服器回傳資源至Client
- 
- ---
- [Test](<Test.md>) redirect_uri 是用來接收token的地點： implicit grant type 在OAuth上的流程為何？ 
    -  `	- A. 使用者訪問客戶端 - B. 客戶端將使用者導向認證伺服器進行身份認證、授權詢問 - C. 使用者同意授權並發送至認證伺服器 - D. 認證伺服器向使用者發送一個導向URI以及Token - E. 使用者藉由導向URI發送token至Client - F. Client 透過Token來向資源伺服器索要資源 - G. 資源伺服器回傳資源至Client`
- 
- [Test](<Test.md>)  redirect_uri 是用來接收token的地點： implicit grant type 在OAuth上的流程為何？ 請畫圖來表示
    -  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679229338/blog/OAuth/OAuth-implicit-version2_euhcgr.png)
- 
- ---
- tags: [OAuth](<OAuth.md>) [Authorization](<Authorization.md>)

# Backlinks
## [implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token](<implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token.md>)
- [implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client](<implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client.md>)


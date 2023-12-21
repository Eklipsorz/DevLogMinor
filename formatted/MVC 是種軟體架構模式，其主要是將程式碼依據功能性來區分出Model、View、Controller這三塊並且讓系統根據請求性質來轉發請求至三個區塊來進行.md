- **## MVC (Model-View-Controller)**
- 1. 是一種軟體架構模式之一，將程式碼依照功能性來區分出三塊，分別為Model、View、Controller
- 2. Model負責定義資料以及對資料的處理方法，View負責定義畫面顯示，而Controller則是負責與使用者互動的邏輯，也是應用程式收發 request/response 的核心
- 3. 在JavaScript實現上，會宣告三種物件來封裝/分類相關的程式碼。
- 
- ```javascript
const model = {
   // 和資料有關的程式碼
}
const view = {
   // 和介面有關的程式碼
}
const controller = {
   // 和流程有關的程式碼
}
```
- 
- 原文：
- Model：Model 常譯為「模型」，負責和資料庫溝通
- View：View 常譯為「視圖」，View 所管理的功能層叫作「表現層 (presentation layer)」，顧名思義是負責管理畫面的呈現，也就是 HTML 樣板 (template)。
- Controller：Controller 常譯為「控制器」，它掌握使用者互動邏輯，也是應用程式收發 request/response 的核心。來自路由的 request 會先被送到 Controller，再由 Controller 通知 Model 調度資料，並且把資料傳遞給 View 來產生樣板 (template)，並將呈現資料的 HTML 頁面回傳給客戶端。
- https://railsbook.tw/chapters/10-mvc.html
- 
- 
- # Node實際專案的MVC架構
- 
- 具體會將MVC架構以目錄來區分出，並且每個目錄都會存在功能上一致的程式碼或者程式碼檔案
- 
- controllers
    - 定義應用程式面對請求如何處理、轉發至Model和View來獲取資料和畫面、回應給客戶端
- models
    - 定義應用程式所存在的資料是為何以及如何處理資料
- views
    - 定義應用程式所要展現的畫面
- routes
    - 定義應用程式的路由系統來幫助請求導向至正確的端點
- 
- 
- ## 實際專案案例
- 
- 
- ### Server Side Rendering
- 由伺服器一端負責將使用者的請求來轉換成對應的View，而View形式會是HTML、JS、CSS所構成的網頁畫面，每一次客戶端向伺服器發送請求時，伺服器都會根據請求內容來將資料與模板網頁檔案做結合並轉換成客戶端可直接以視覺呈現的檔案，最後由伺服器將結果檔案回傳給客戶端
- > rendering a client-side or universal app to HTML on the server.
- 簡述流程：
    - 1. 瀏覽器針對特定網址送出請求
    - 2. 伺服器的路由會接收到請求，接著解析請求後，轉接給對應的 controller
    - 3. controller 按照要求，透過 model 拿資料
    - 4. controller 拿到資料後，呼叫 view template，並嵌入資料
    - 5. 把「有資料的 template」轉換成瀏覽器可直接呈現的形式並回傳給瀏覽器
    - 6. 瀏覽器接收檔案並以視覺形式來呈現其畫面。
- ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1633596645/blog/network/ClientAndServer/MVCModel_dgvnhm.png)
- 當Client 從伺服器獲得初始網頁後，便會從該網頁發送其他種類的請求，而伺服器接收到請求就會按照上述流程來產生對應的網頁給客戶端
- ![](https://s3.ap-south-1.amazonaws.com/storage.alfabolt.com/b1e61443-a5b0-4e35-86e2-4f1ad13f657d-min.png)
- 
- 
- ---
- [Design](<Design.md>) 請問MVC軟體架構方式的完整名稱為何?
    - Model-View-Controller
- [Design](<Design.md>) 請問MVC軟體架構方式其會是如何架構?
    - 將程式碼分割成畫面、業務邏輯、資料三種架構
- [Design](<Design.md>) 請問MVC軟體架構方式中的Model會是甚麼?
    - Model 負責定義資料和對資料的處理方法
- 
- [Design](<Design.md>) 請問MVC軟體架構方式中的View會是甚麼?
    -  View負責定義畫面顯示
- 
- [Design](<Design.md>) 請問MVC軟體架構方式中的Controller會是甚麼?
    - Controller則是負責與使用者互動的邏輯，也是應用程式收發 request/response 的核心
- 
- [Design](<Design.md>) 請問MVC軟體架構方式實際在Node專案會是如何? 
    - 具體會將MVC架構以目錄來區分出，並且每個目錄都會存在功能上一致的程式碼或者程式碼檔案，如contollers、models、views，接著會另外定義一個專案用的路由系統來定義路由以及如何導向其MVC
- 
- [Design](<Design.md>) 假設伺服器會提供網頁畫面至客戶端，那麼整體MVC架構在實際客戶端發送請求和請求得到回應之間的過程會是如何? 請畫圖來表示
    - ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1633596645/blog/network/ClientAndServer/MVCModel_dgvnhm.png)
- 
- [Design](<Design.md>) 以下為MVC實際在伺服器和客戶端之間的實現方式，在這裡伺服器會根據客戶端發送的請求來提供網頁畫面給客戶端，請解釋圖中的每個步驟是如何 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1633596645/blog/network/ClientAndServer/MVCModel_dgvnhm.png)
    - 簡述流程：
        - 1. 瀏覽器針對特定網址送出請求
        - 2. 伺服器的路由會接收到請求，接著解析請求後，轉接給對應的 controller
        - 3. controller 按照要求，透過 model 拿資料
        - 4. controller 拿到資料後，呼叫 view template，並嵌入資料
        - 5. 把「有資料的 template」轉換成瀏覽器可直接呈現的形式並回傳給瀏覽器
        - 6. 瀏覽器接收檔案並以視覺形式來呈現其畫面。
- 
- ---
- tags: 
- 
- 

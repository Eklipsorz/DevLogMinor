- **## MVC (Model-View-Controller)**
- 1. 是一種軟體開發方法之一，將程式碼依照功能性來區分出三塊，分別為Model、View、Controller
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

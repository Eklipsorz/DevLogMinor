- 

- 
- [[@ALLLF49J]]
- ```javascript
https://authorization-server.com/auth
 ?response_type=token
 &client_id=29352910282374239857
 &redirect_uri=https%3A%2F%2Fexample-app.com%2Fcallback
 &scope=create+delete
 &state=xcoiv98y3md22vwsuye3kch```
- Here’s each query parameter explained: 
- 
- ```javascript
- state - The application generates a random string and includes it in the request. It should then check that the same value is returned after the user authorizes the app. This is used to prevent CSRF attacks.```

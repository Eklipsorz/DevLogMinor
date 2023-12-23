- cmd
- [@FNF6UB2F](<@FNF6UB2F.md>)
- > I now realize that the "postgres=#" prompt is a fresh prompt waiting for the start of a new command, while the "postgres-#" is the result of hitting enter after typing a command that does not end with a semicolon.
- > The semicolon denotes the end of a command, so pressing enter without a terminating ";" suggests to postgres that you would like to continue writing your command on a new line.
- > Inserting a semicolon at any point and pressing enter will return you to the original prompt.
- 
- > Also a postgres(# indicates you have an open parenthesis, and it will show quoting with postgres'#, postgres"#, and postgres$# prompts. Finally if you were not a superuser your prompt would end in > (like postgres=>).
- 
- 重點:
- =# 表示系統正等待著指令輸入
- -# 表示系統正接收到一個指令但該指令還未以分號結尾
- (# 表示系統正接受到(這個open parenthesis並允許輸入者換行輸入指令 
- 
- ```javascript
postgres=#
postgres-#  
postgres(# ```
- 
- 指定存取特定資料庫
- 
- ```javascript
\c database_name```
- 
- 
- 

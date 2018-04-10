# Line_watchdog

門位監測 + LINE notify

  

## Line Watchdog 流程

1. 註冊，並透過網頁取得 code。 [http://localhost/line_watchdog/auth.html](http://localhost/line_watchdog/auth.html)
```
http://localhost/line_watchdog/auth_OK.html?code=G6ctjoGtuOyhdfwnYrWf8L&state=abcde
```

2. 拿 code 跟 Line 交換 access_token
```
POST https://notify-bot.line.me/oauth/token
```
```
Method POST  
Content-Type application/x-www-form-urlencoded  
-----------------------------------------------------------------------------------  
grant_type Required fixed value Assigns "authorization_code"  
code Required string Assigns a code parameter value generated during redirection  
redirect_uri Required uri Assigns redirect_uri to assigned authorization endpoint API  
client_id Required string Assigns client ID to issued OAuth  
client_secret Required string Assigns secret to issued OAuth
```
```JSON
{  
"status": 200,  
"message": "access_token is issued",  
"access_token": "2RKWZ5enIM9CEu1CDxcFWvv7UhRwJnTsJagQdKsgWdi"  
}
```
3. 傳遞訊息
```
POST https://notify-api.line.me/api/notify
```
```
Method POST  
Content-Type application/x-www-form-urlencoded OR multipart/form-data  
Authorization Bearer <access_token>  
-----------------------------------------------------------------------------------  
message Required String 1000 characters max
```
```
docker run -d -p 3000:3000 \
   -e OPENAI_API_KEY=你的api key \
   -e BASE_URL=https://api.openai.com \
   -e CODE=你的密码 \
   yidadaa/chatgpt-next-web
```



不希望用户输入api key可以添加此项：
```
-e HIDE_USER_API_KEY=1
```


使用代理启动服务可以添加此项：
```
-e PROXY_URL="http://127.0.0.1:7890 user pass"
```



---

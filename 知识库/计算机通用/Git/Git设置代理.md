# Git设置代理

### Git设置代理

`git config --global http.proxy 'socks5://127.0.0.1:1080'`

`git config --global https.proxy 'socks5://127.0.0.1:1080'`

**为github设置代理**  `git config --global http.https://github.com.proxy socks5://127.0.0.1:1080`



### Git查看代理

**查看github的代理** `git config --global --get http.https://github.com.proxy`

`git config --global --get http.proxy`

`git config --global --get https.proxy`





### Git取消代理

**取消github的代理** `git config --global --unset http.https://github.com.proxy`

`git config --global --unset http.proxy`

`git config --global --unset https.proxy`



export http_proxy=[socks5://127.0.0.1:1080](socks5://127.0.0.1:1080)

export http_proxy="http://127.0.0.1:1080"
export https_proxy="http://127.0.0.1:1080"
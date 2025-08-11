# ptt_autologin
PTT 每天自動登入

:x: GitHub Actions 的執行環境無法連線到 ptt.cc 的 telnet 服務（port 23）

- GitHub 的 Ubuntu runner 是跑在雲端資料中心（如 Azure），通常 port 23（Telnet）已被防火牆封鎖
- telnet 屬於過時協議，不安全，雲平台常會預設封鎖

參考 URL : https://tonytonyjan.net/2015/12/08/login-ptt-everyday-automatically/


### 1. 安裝套件
```bash
sudo apt-get install expect
```

### 2. 確認 expect 的路徑，使用以下命令來查找 `expect` 的路徑：
```bash
which expect
```
假設 `expect` 安裝在 `/usr/bin/expect`，那麼腳本的開頭應該是：
`#!/usr/bin/expect -f`

### 3. 為腳本賦予執行權限：
`chmod +x .sh`

### 4. 測試
```bash
./ptt_login.sh "username" "password"
```

### 5. 加入 `crontab` 定時執行

1. 編輯 crontab：

```bash
crontab -e
```

2. 在最後加上這一行（請改成實際的帳號和路徑）： 

```bash
6 6 * * * /bin/bash -c .sh_file_path PTT_ID=你的帳號 PTT_PWD=你的密碼 
```

> 💡 每天早上 6:06 執行一次


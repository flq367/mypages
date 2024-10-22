### 0. 通用指令

* 国内镜像

    ```dockerfile
    docker pull dockerproxy.cn/
    docker pull docker.udayun.com/
    ```
    
* docker安装

    ```dockerfile
    # 安装一些必要的软件包
    apt update
    apt upgrade -y
    apt install curl vim wget gnupg dpkg apt-transport-https lsb-release ca-certificates
    
    # 加入 Docker 的 GPG 公钥和 apt 源
    curl -sSL https://download.docker.com/linux/debian/gpg | gpg --dearmor > /usr/share/keyrings/docker-ce.gpg
    
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-ce.gpg] https://download.docker.com/linux/debian $(lsb_release -sc) stable" > /etc/apt/sources.list.d/docker.list
    
    # 安装 Docker CE 和 Docker Compose 插件
    apt update
    apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```
- 通用指令

  ```dockerfile
  ssh flq367@192.168.1.3
  
  sudo -i
  
  docker ps -a    # 查看所有镜像
  
  docker exec -it 1bda23a292ec bash    # 进入对应容器的 /bin/bash
  
  docker system prune -a    # 清理所有废弃镜像与Build Cache
  
  docker volume prune   # 清理废弃镜像卷组
  
  docker network prune   # 清理废弃镜像网络
  
  docker update --restart=always a2e0f3d47c1d   # 添加restart=always
  
  # 等待缓存锁：无法获得锁
  sudo rm /var/lib/dpkg/lock-frontend
  ```
- 测试与优化
  
  ```dockerfile
  # 融合怪测评脚本
  bash <(wget -qO- ecs.0s.hk)
  
  # IP质量检测
  bash <(wget -qO- bash.spiritlhl.net/ecs-ipcheck)
  
  # 科技lion
  bash <(curl -sL kejilion.sh)
  
  k fd <域名> <iP> <端口>
  #  k fd alist.xy95.top 8.218.68.25 5244
  ```
  
- root直连

  ```dockerfile
  sudo passwd root
  
  su -
  
  cd /etc/ssh
  
  nano sshd_config
  # PermitRootLogin yes
  # PasswordAuthentication yes
  
  systemctl restart sshd.service
  ```

- 更改显示颜色

  ```dockerfile
  ls -a  # 显示隐藏文件
  
  nano .bashrc
  
  #取消下列注释
  # export LS_OPTIONS='--color=auto'
  # eval "$(dircolors)"
  # alias ls='ls $LS_OPTIONS'
  # alias ll='ls $LS_OPTIONS -l'
  # alias l='ls $LS_OPTIONS -lA'
  
  . .bashrc
  ```

* * *

### 1. wifi

- 连接wifi

    ```dockerfile
    nmcli device wifi list 
    nmcli device wifi connect "XY95" password "maogai3678"
    ```

- 断开wif

    ```dockerfile
    nmcli device disconnect wlp2s0
    ```

* * *

### 2. Lucky 

**gdy666/lucky**

- 网络
  Host

- 默认账号密码

   666/666

- dockercompose

   ```dockerfile
   services:
     lucky:
       image: gdy666/lucky
       container_name: lucky
       labels:
         net.unraid.docker.icon: "https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/Lucky/icon.png"
         net.unraid.docker.webui: "http://[IP]:[PORT:16601]"
       volumes:
         - /vol1/1000/Docker/lucky:/goodluck
       network_mode: host
       restart: always
   ```

- 资料
  [完美网络搭建3：进站（公网IP+DDNS+SSL证书+HTTPS反代理）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1cC411Y72K/?vd_source=9f958b5546f50654f79d5b52da1528ca)

  [【教程】Lucky配合Cloudflare更安全的访问局域网服务 ' 岂曰无衣的博客 (ljmeng.site)](https://ljmeng.site/posts/16549/#:~:text=%E6%89%93%E5%BC%80%E3%80%90Web%E6%9C%8D%E5%8A%A1%E3%80%91%EF%BC%8C%E9%80%89%E6%8B%A9%E3%80%90%E6%B7%BB%E5%8A%A0Web%E6%9C%8D%E5%8A%A1%E8%A7%84%E5%88%99%E3%80%91%E9%85%8D%E7%BD%AEweb%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86%E6%9C%8D%E5%8A%A1%EF%BC%8C%E4%B8%BE%E4%BE%8B%E5%A6%82%E4%B8%8B%E5%9B%BE%EF%BC%8C%E5%85%B6%E4%B8%AD%E5%90%8E%E7%AB%AF%E5%9C%B0%E5%9D%80%E6%9B%B4%E6%94%B9%E4%B8%BA%E4%BD%A0%E6%83%B3%E4%BB%A3%E7%90%86%E7%9A%84%E5%B1%80%E5%9F%9F%E7%BD%91%E6%9C%8D%E5%8A%A1%E7%9A%84IP%E5%8A%A0%E7%AB%AF%E5%8F%A3%20%E7%BB%93%E8%AF%AD%20%E6%81%AD%E5%96%9C%E4%BD%A0%EF%BC%8C%E5%88%B0%E6%AD%A4%E5%A4%A7%E5%8A%9F%E5%91%8A%E6%88%90%EF%BC%81%20%E7%9B%B4%E6%8E%A5%E7%94%A8,https%3A%2F%2Fabc.example.com%20%E5%8D%B3%E5%8F%AF%E5%9C%A8%E4%BA%92%E8%81%94%E7%BD%91%E5%8A%A0%E5%AF%86%E8%AE%BF%E9%97%AE%E4%BD%A0%E5%AE%B6%E9%87%8C%E7%9A%84%E5%B1%80%E5%9F%9F%E7%BD%91%E6%9C%8D%E5%8A%A1%E3%80%82%20PS%3A%20%E5%90%8E%E7%BB%AD%E6%83%B3%E6%B7%BB%E5%8A%A0%E5%85%B6%E4%BB%96%E5%B1%80%E5%9F%9F%E7%BD%91%E7%9A%84Web%E6%9C%8D%E5%8A%A1%EF%BC%8C%E5%8F%AA%E9%9C%80%E5%9C%A8Lucky%E7%9A%84%E3%80%90Web%E6%9C%8D%E5%8A%A1%E3%80%91%E9%85%8D%E7%BD%AE%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86%E5%8D%B3%E5%8F%AF)

* * *

### 3. 图床 

**dko0/lsky-pro**

- 查询兰空图床Token

    ```dockerfile
    curl 192.168.1.2:9080/api/v1/tokens -X POST -d 'email=yc0012@qq.com&password=maogai367'
    ```

- 资料
  [用仅ipv6vps自建图床并支持ipv4访问 - 马火星的迷你小屋 (tt2ter.github.io)](https://tt2ter.github.io/post/220904picture-server.html)

- 存储策略
  访问网址：[https://pic.ycsite.us.kg/i](https://pic.ycsite.us.kg/i)

  存储路径：/var/www/html/storage/app/uploads

  总容量：104857600 kb

  最大文件大小：51200 kb

- docker compose

    ```
    version: '3.3'
    services:
      lsky-pro:
        image: dko0/lsky-pro
        container_name: lsky-pro
        restart: always
        volumes:
    
       - /vol1/1000/tools/lsky/html:/var/www/html  #映射到本地
         rts:
            - 9080:80
    ```

* * *

### 4. v2raya 

**mzz2017/v2raya**

- 博客
  [科学上网：利用 Docker 搭建 v2raya 客户端 - LazyPool's Blog (lazypool-blog.netlify.app)](https://lazypool-blog.netlify.app/2024/05/13/docker/)

- 订阅链接
  https://gawrgura.moe/api/v1/client/subscribe?token=d428f95c9e751d049df300ab1b30941f

* * *

### 5. HomeAssistant 

**homeassistant/home-assistant**

- 安装HACS

    ```dockerfile
    wget -O - https://get.hacs.vip ' bash - # hacs-china
    ```

- 网络
  Host 

  port：8123
  
- 资料
  [各种智能家居接入苹果家庭App/HomeKit：超详细30分钟保姆级教程分享_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1mm4y157n1/?vd_source=9f958b5546f50654f79d5b52da1528ca)

  [Home Assistant的初始配置，以及通过HACS添加智能设备_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1kj421m7FK/?vd_source=9f958b5546f50654f79d5b52da1528ca)

* * *

### 6. sun-panel 

**hslr/sun-panel**

- 默认账号密码

  账号：**admin@sun.cc**

  密码：**12345678**
  
- dockercompose

  ```dockerfile
  version: "3.2"
  services:
    sun-panel:
      image: "hslr/sun-panel:latest"
      container_name: sun-panel
      volumes:
        - /vol1/1000/Docker/sun-panel/conf:/app/conf
        - /vol1/1000/Docker/sun-panel/run/docker.sock:/var/run/docker.sock
      ports:
        - 3002:3002
      restart: always
  ```

  

* * *

### 7. reader

**hectorqin/reader**

- docker compose
    ```
    version: '3.1'
    services:
      reader:
        image: hectorqin/reader
        container_name: reader
        restart: always
        ports:
          - 4396:8080
        networks:
          - share_net
        volumes:
          - /vol1/1000/tools/reader/logs:/logs
          - /vol1/1000/tools/reader/storage:/storage
        environment:
          - SPRING_PROFILES_ACTIVE=prod
          - READER_APP_USERLIMIT=50 #用户上限,默认50
          - READER_APP_USERBOOKLIMIT=200 #用户书籍上限,默认200
          - READER_APP_CACHECHAPTERCONTENT=true #开启缓存章节内容 V2.0
          - READER_APP_SECURE=true #开启登录鉴权，开启后将支持多用户模式
          - READER_APP_SECUREKEY=adminpwd  #管理员密码  建议修改
          - READER_APP_INVITECODE=yc #注册邀请码 建议修改,如不需要可注释或删除
        networks:
          - reader-net
    
    networks:
      reader-net:
        driver: bridge
    ```
* * *

### 8. Alist

**xhofe/alist**

- docker compose

    ```
    version: '3.3'
    services:
      alist:
        image: 'xhofe/alist:latest'
        container_name: alist
        volumes:
          - '/vol1/1000/Docker/alist/data:/opt/alist/data'
        ports:
          - '5244:5244'
        environment:
          - PUID=0
          - PGID=0
          - UMASK=022
        restart: always
        networks:
          - alist-net
    
    networks:
      alist-net:
        driver: bridge
    ```
* * *

### 9. wordpress

- php.ini

    `cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini `

​	`435 memory_limit = 500M `

​	`703 post_max_size = 200M `

​	`855 upload_max_filesize = 200M`

- 主题
  argon

​	[https://images.hdqwalls.com/wallpapers/anime-landscape-waterfall-cloud-5k-mq.jpg](https://images.hdqwalls.com/wallpapers/anime-landscape-waterfall-cloud-5k-mq.jpg)

​	[https://images.hdqwalls.com/wallpapers/kakashi-hatake-naruto-uzumaki-sakura-haruno-sasuke-uchiha-uf.jpg](https://images.hdqwalls.com/wallpapers/kakashi-hatake-naruto-uzumaki-sakura-haruno-sasuke-uchiha-uf.jpg)

- docker compose

    ```
    version: '3.3'           
    services:
       db:
         container_name: mysql-wp
         image: mysql:8.0    
         volumes:
           - /vol1/1000/tools/mysql/wordpress:/var/lib/mysql   
         restart: always     
         environment:        
           MYSQL_ROOT_PASSWORD: 1
           MYSQL_DATABASE: wpdb
           MYSQL_USER: flq367
           MYSQL_PASSWORD: maogai367
    
       wordpress:
         depends_on:
           - db
         container_name: wordpress
         image: wordpress:latest
         volumes:
           - /vol1/1000/tools/wordpress/html:/var/www/html
         ports:
           - "8181:80"
         restart: always
         environment:
           WORDPRESS_DB_HOST: db:3306
           WORDPRESS_DB_USER: flq367
           WORDPRESS_DB_PASSWORD: maogai367
           WORDPRESS_DB_NAME: wpdb
    volumes:
        db_data: {}
    ```

---

### 10.watchtower

**containrrr/watchtower**

- docker compose

    ```
    version: '3.1'
    services:
      watchtower:
        image: containrrr/watchtower
        container_name: watchtower
        restart: always
        environment:
            - TZ=Asia/Shanghai
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
        command: reader watchtower --cleanup --schedule "0 0 4 * * *"
        networks:
          - watchtower-net
    
    networks:
      watchtower-net:
        driver: bridge
    ```

---

### 11.portainer
6053537/portainer-ce

```dockerfile
docker run -d --restart=always --name="portainer" -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock 6053537/portainer-ce
```

---

### 12.x-ui

```dockerfile
bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/master/install.sh)

bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/master/install.sh)

sudo x-ui
```

---
### 13. tls证书申请

```dockerfile
#安装证书工具：
curl https://get.acme.sh | sh; apt install socat -y || yum install socat -y; ~/.acme.sh/acme.sh --set-default-ca --server letsencrypt

#三种方式任选其中一种，申请失败则更换方式
#申请证书方式1： 
~/.acme.sh/acme.sh  --issue -d 35-209-246-70.nip.io --standalone -k ec-256 --force --insecure
#申请证书方式2： 
~/.acme.sh/acme.sh --register-account -m "${RANDOM}@chacuo.net" --server buypass --force --insecure && ~/.acme.sh/acme.sh  --issue -d 你的域名 --standalone -k ec-256 --force --insecure --server buypass
#申请证书方式3： 
~/.acme.sh/acme.sh --register-account -m "${RANDOM}@chacuo.net" --server zerossl --force --insecure && ~/.acme.sh/acme.sh  --issue -d 你的域名 --standalone -k ec-256 --force --insecure --server zerossl

#安装证书：
~/.acme.sh/acme.sh --install-cert -d 35-209-246-70.nip.io --ecc --key-file /etc/x-ui/server.key --fullchain-file /etc/x-ui/server.crt
```

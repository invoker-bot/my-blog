---
layout: post
title:  "Headless Chrome SeleniumSetup"
date:   2023-12-08 19:00:07 +0800
categories: selenium
---

# 在Linux上安装Google Chrome及使用Selenium启动无桌面浏览器

本教程将指导您如何在CentOS和Ubuntu系统上安装Google Chrome，并使用Selenium以无桌面（headless）模式启动Chrome浏览器。

## 安装Google Chrome

### CentOS

1. 添加Chrome仓库：
   ```bash
   sudo sh -c 'echo -e "[google-chrome]\nname=google-chrome\nbaseurl=http://dl.google.com/linux/chrome/rpm/stable/\$basearch\nenabled=1\ngpgcheck=1\ngpgkey=https://dl.google.com/linux/linux_signing_key.pub" > /etc/yum.repos.d/google-chrome.repo'
   ```

2. 安装Chrome：
   ```bash
   sudo yum install google-chrome-stable -y
   ```

### Ubuntu

1. 下载Google Chrome的最新稳定版本：
   ```bash
   wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   ```

2. 安装包：
   ```bash
   sudo dpkg -i google-chrome-stable_current_amd64.deb
   ```

3. 如果出现依赖问题，运行：
   ```bash
   sudo apt-get install -f
   ```

## 测试Google Chrome是否成功运行

* 以无桌面形式运行检查是否能访问测试网站
  ```bash
  google-chrome --disable-dev-shm-usage --headless --no-sandbox --disable-gpu --dump-dom https://www.example.com
  ```

## 使用Selenium启动Headless Chrome

1. 首先，确保安装了Python和pip。

2. 安装Selenium和webdriver_manager：
   ```bash
   pip install selenium webdriver_manager
   ```

3. 编写Python脚本以启动Headless Chrome：
   ```python
   from selenium import webdriver
   from selenium.webdriver.chrome.options import Options
   from selenium.webdriver.chrome.service import Service as ChromeService
   from webdriver_manager.chrome import ChromeDriverManager

   chrome_driver_version = None  # 替换为想要的版本号 "X.X.XXX"

   # 设置Chrome选项
   chrome_options = Options()
   options.add_argument("--headless")  # 启用无头模式
   options.add_argument("--no-sandbox")  # 禁用沙盒模式
   options.add_argument("--disable-dev-shm-usage")  # 避免共享内存问题
   options.add_argument("--disable-gpu")  # 禁用GPU加速


   driver = webdriver.Chrome(
       service=ChromeService(ChromeDriverManager(chrome_driver_version).install()),
       options=chrome_options
   )
   ```

4. 运行脚本，Chrome将以无桌面模式启动。

以上步骤将帮助您在CentOS和Ubuntu系统上安装Google Chrome，并使用Selenium以无桌面模式运行Chrome，这对于服务器环境和自动化测试非常有用。


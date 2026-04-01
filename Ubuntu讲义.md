# Ubuntu Linux 系统讲义

---

# 目录

- [第1章 Ubuntu概述](#第1章-ubuntu概述)
- [第2章 系统安装](#第2章-系统安装)
- [第3章 命令行基础](#第3章-命令行基础)
- [第4章 文件系统管理](#第4章-文件系统管理)
- [第5章 用户与权限管理](#第5章-用户与权限管理)
- [第6章 软件包管理](#第6章-软件包管理)
- [第7章 网络配置与管理](#第7章-网络配置与管理)
- [第8章 进程与服务管理](#第8章-进程与服务管理)
- [第9章 磁盘管理](#第9章-磁盘管理)
- [第10章 计划任务](#第10章-计划任务)
- [第11章 SSH远程登录](#第11章-ssh远程登录)
- [第12章 系统安全](#第12章-系统安全)
- [第13章 Vim编辑器](#第13章-vim编辑器)
- [第14章 开机启动与运行级别](#第14章-开机启动与运行级别)

---

# 第1章 Ubuntu概述

## 1.1 Ubuntu简介

Ubuntu（乌班图）是一个基于Debian Linux的开源操作系统，以其易用性、稳定性安全性而闻名。Ubuntu由Canonical公司赞助，每两年发布一个LTS（长期支持）版本，提供至少5年的安全更新。

**官方网站**：
- https://ubuntu.com
- https://cn.ubuntu.com

## 1.2 Ubuntu版本介绍

### 1.2.1 官方桌面版本

| 版本 | 桌面环境 | 特点 |
|------|----------|------|
| Ubuntu | GNOME | 官方默认桌面，现代简洁 |
| Kubuntu | KDE | 功能丰富，可定制性强 |
| Lubuntu | LXDE/LXQt | 轻量级，适合老旧硬件 |
| Xubuntu | Xfce | 轻量级，低资源占用 |
| Ubuntu Budgie | Budgie | 现代美观，简洁高效 |
| Ubuntu Mate | MATE | 传统桌面，平衡之选 |
| Mythbuntu | - | 多媒体中心专用 |

### 1.2.2 Ubuntu版本号命名规则

Ubuntu版本号由年份和月份组成：
- Ubuntu 22.04：2022年4月发布的LTS版本
- Ubuntu 24.04：2024年4月发布的LTS版本

LTS版本每两年发布一次，适合服务器和长期项目使用。

## 1.3 Ubuntu与Windows的主要区别

| 特性 | Ubuntu | Windows |
|------|--------|---------|
| 授权方式 | 开源免费 | 商业授权 |
| 价格 | 免费 | 付费 |
| 驱动支持 | 需要手动安装 | 自动安装 |
| 软件安装 | APT包管理器 | 应用商店/官网下载 |
| 文件系统 | ext4 | NTFS |
| 系统更新 | 安全更新持续提供 | 大版本更新 |
| 命令行 | 原生支持 | 需要PowerShell/CMD |

## 1.4 系统基本配置

### 1.4.1 图形化管理工具

Ubuntu提供了多个图形化配置工具：

| 工具 | 用途 |
|------|------|
| unity-tweak-tool | Unity桌面配置 |
| gnome-tweaks | GNOME桌面配置 |
| 软件中心 | 安装/卸载软件 |
| 系统设置 | 网络、电源、显示等 |

### 1.4.2 常用快捷键

| 快捷键 | 功能 |
|--------|------|
| Ctrl + Alt + T | 打开终端 |
| Ctrl + A | 光标移到行首 |
| Ctrl + E | 光标移到行尾 |
| Ctrl + L | 清屏 |
| Ctrl + U | 删除光标到行首的内容 |
| Ctrl + K | 删除光标到行尾的内容 |
| Ctrl + Shift + = | 放大终端字体 |
| Ctrl + - | 缩小终端字体 |

### 1.4.3 终端字体大小调整

```
Ctrl + Shift + +  或  Ctrl + =    # 放大
Ctrl + -                        # 缩小
```

---

# 第2章 系统安装

## 2.1 系统要求

### 2.1.1 硬件要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 1 GHz | 2 GHz 双核 |
| 内存 | 1 GB | 4 GB 或更多 |
| 硬盘 | 10 GB | 25 GB 或更多 |
| 显卡 | VGA 640×480 | 支持3D加速 |

### 2.1.2 下载镜像

**官方镜像源**：
- http://releases.ubuntu.com/
- http://mirrors.163.com/ubuntu-releases/
- https://mirrors.tuna.tsinghua.edu.cn/（清华源）

## 2.2 安装过程详解

### 2.2.1 安装步骤

**步骤1**：从U盘或光盘启动，选择第一项"Install Ubuntu"

**步骤2**：选择语言，建议选择"中文（简体）"或"English"

**步骤3**：键盘布局选择默认（English US 或 Chinese）

**步骤4**：选择安装类型
- 最小安装：只安装基础组件，适合服务器
- 正常安装：包含办公软件、浏览器等
- 高级选项：自定义分区

**步骤5**：选择"其他选项"进行手动分区（推荐）

### 2.2.2 分区方案建议

对于桌面用户，建议创建以下分区：

| 分区 | 大小 | 文件系统 | 挂载点 | 说明 |
|------|------|----------|--------|------|
| /boot | 500MB-1GB | ext4 | /boot | 引导分区 |
| swap | 内存大小 | swap | - | 交换分区 |
| / | 20-50GB | ext4 | / | 根分区 |
| /home | 余下空间 | ext4 | /home | 用户数据 |

## 2.3 安装后配置

### 2.3.1 设置软件自动更新

```bash
# 安装更新管理器
sudo apt install update-manager

# 检查更新
sudo apt update && sudo apt upgrade
```

### 2.3.2 切换中文输入法

```bash
# 安装中文输入法
sudo apt install ibus-pinyin
# 或
sudo apt install fcitx5 fcitx5-chinese-addons
```

### 2.3.3 配置中文语言支持

```bash
# 安装语言包
sudo apt install language-pack-zh-hans

# 重新配置语言环境
sudo dpkg-reconfigure locales
```

## 2.4 进入命令行与图形界面

### 2.4.1 虚拟控制台

| 快捷键 | 功能 |
|--------|------|
| Ctrl + Alt + F1 | 图形化用户选择界面 |
| Ctrl + Alt + F2 | 图形化登录界面 |
| Ctrl + Alt + F3-F6 | 命令行界面（TTY3-6） |
| Ctrl + Alt + F7 | 返回图形桌面 |

### 2.4.2 命令行与图形界面切换

```bash
# 设置开机直接进入命令行
sudo systemctl set-default multi-user.target
echo "false" | sudo tee /etc/X11/default-display-manager

# 设置开机进入图形桌面
sudo systemctl set-default graphical.target
echo "/usr/sbin/gdm" | sudo tee /etc/X11/default-display-manager

# 在命令行模式返回图形桌面
startx
```

---

# 第3章 命令行基础

## 3.1 基本命令

### 3.1.1 查看当前用户

```bash
# 查看当前用户名
whoami

# 查看所有登录用户
who

# 查看当前用户详细信息
w
```

### 3.1.2 查看主机信息

```bash
# 查看主机名
hostname

# 查看网络地址
hostname -I

# 查看详细主机信息
hostnamectl
```

### 3.1.3 查看当前目录

```bash
# 显示当前目录路径
pwd

# 查看当前目录内容
ls

# 详细列表显示
ls -l

# 显示所有文件（包括隐藏）
ls -a

# 显示文件大小（人类可读）
ls -lh

# 按时间排序
ls -lt

# 递归显示子目录
ls -R
```

### 3.1.4 切换目录

```bash
# 进入指定目录
cd /path/to/directory

# 返回上级目录
cd ..

# 返回上上级目录
cd ../..

# 返回用户主目录
cd ~

# 返回上一次所在目录
cd -

# 进入当前目录
cd .
```

### 3.1.5 查看帮助

```bash
# 查看命令手册
man command_name

# 查看简洁帮助
command_name --help

# 查看shell内置命令帮助
help command_name

# 查看命令位置
which command_name

# 显示命令类型
type command_name
```

## 3.2 命令格式

### 3.2.1 命令基本语法

```
命令 [选项] [参数]
```

**示例**：
```bash
ls -la /home          # 列出/home目录的详细信息
cp -r /src /dst       # 递归复制目录
rm -f file.txt        # 强制删除文件
```

### 3.2.2 常用选项说明

| 选项 | 说明 |
|------|------|
| -a | 显示所有文件（包括隐藏） |
| -l | 详细信息列表 |
| -r | 递归处理 |
| -f | 强制执行 |
| -i | 交互式确认 |
| -h | 人类可读格式 |
| -v | 显示详细过程 |
| -n | 显示行号 |

## 3.3 历史命令

```bash
# 查看命令历史
history

# 执行上一条命令
!!

# 执行指定编号的历史命令
!123

# 执行最近以ls开头的命令
!ls

# 搜索历史命令
Ctrl + R
```

## 3.4 输入输出重定向

### 3.4.1 输出重定向

```bash
# 将输出覆盖写入文件
command > file.txt

# 将输出追加写入文件
command >> file.txt

# 将错误输出写入文件
command 2> error.txt

# 将所有输出写入文件
command > all.txt 2>&1
```

### 3.4.2 输入重定向

```bash
# 从文件读取输入
command < input.txt

# Here Document
cat << EOF > file.txt
这是文件内容
EOF
```

### 3.4.3 管道符

```bash
# 将前一个命令的输出作为后一个命令的输入
ls -l | grep "pattern"

# 统计行数
ls | wc -l

# 排序
cat file.txt | sort | uniq
```

## 3.5 通配符

| 通配符 | 说明 | 示例 |
|--------|------|------|
| * | 匹配任意字符 | *.txt 匹配所有txt文件 |
| ? | 匹配单个字符 | file?.txt 匹配file1.txt |
| [] | 匹配括号内字符 | [abc] 匹配a、b或c |
| [!] | 匹配不在括号内字符 | [!abc] 除abc外的字符 |

---

# 第4章 文件系统管理

## 4.1 文件系统结构

### 4.1.1 目录结构

```
/                   # 根目录，所有文件的起点
├── bin/            # 常用命令二进制文件
├── boot/           # 启动文件、内核
├── dev/            # 设备文件
├── etc/            # 系统配置文件
├── home/           # 用户主目录
│   └── username/    # 用户目录
├── lib/            # 共享库文件
├── media/          # 可移动媒体
├── mnt/            # 临时挂载点
├── opt/            # 可选应用软件
├── proc/           # 进程信息（虚拟）
├── root/           # root用户主目录
├── run/            # 运行时数据
├── sbin/           # 系统管理命令
├── srv/            # 服务数据
├── sys/            # 系统信息（虚拟）
├── tmp/            # 临时文件
├── usr/            # 用户程序
└── var/            # 可变数据（日志等）
```

### 4.1.2 重要目录说明

| 目录 | 用途 |
|------|------|
| /etc | 系统配置文件目录 |
| /var/log | 系统日志文件 |
| /var/www | Web服务器目录 |
| /home | 普通用户主目录 |
| /root | root用户主目录 |
| /tmp | 临时文件目录 |
| /usr/local | 本地安装软件 |

## 4.2 文件类型

### 4.2.1 Linux文件类型

| 类型标识 | 说明 |
|----------|------|
| - | 普通文件 |
| d | 目录 |
| l | 符号链接 |
| c | 字符设备 |
| b | 块设备 |
| p | 管道 |
| s | 套接字 |

### 4.2.2 文件属性

使用 `ls -l` 查看文件属性：

```
-rwxr-xr-x 1 user group 4096 Jan 1 10:00 example.txt
```

| 字段 | 说明 |
|------|------|
| -rwxr-xr-x | 文件类型和权限 |
| 1 | 链接数 |
| user | 所有者 |
| group | 所属组 |
| 4096 | 文件大小 |
| Jan 1 10:00 | 修改时间 |
| example.txt | 文件名 |

## 4.3 文件操作命令

### 4.3.1 创建文件

```bash
# 创建空文件
touch filename.txt

# 创建带有内容的文件
echo "content" > filename.txt

# 使用cat创建
cat > filename.txt
content here
Ctrl+D

# 使用heredoc
cat << EOF > filename.txt
content
EOF
```

### 4.3.2 查看文件内容

```bash
# 显示整个文件内容
cat filename.txt

# 显示文件并显示行号
cat -n filename.txt

# 分页查看文件
more filename.txt
less filename.txt

# 查看文件前几行
head -n 10 filename.txt

# 查看文件后几行
tail -n 10 filename.txt

# 实时追踪文件更新
tail -f /var/log/syslog
```

### 4.3.3 复制文件

```bash
# 复制文件
cp source.txt destination.txt

# 复制并改名
cp source.txt /path/to/new_name.txt

# 递归复制目录
cp -r source_dir/ destination_dir/

# 复制时保留属性
cp -p source.txt destination.txt

# 复制时显示详细信息
cp -v source.txt destination.txt
```

### 4.3.4 移动/重命名文件

```bash
# 移动文件
mv source.txt /path/to/destination/

# 重命名文件
mv old_name.txt new_name.txt

# 移动并改名
mv source.txt /path/to/new_name.txt

# 移动多个文件
mv file1.txt file2.txt /destination/
```

### 4.3.5 删除文件

```bash
# 删除文件（需确认）
rm filename.txt

# 强制删除文件
rm -f filename.txt

# 删除空目录
rmdir directory/

# 递归删除目录及其内容
rm -rf directory/

# 删除前询问
rm -ri directory/
```

### 4.3.6 创建目录

```bash
# 创建单个目录
mkdir directory_name

# 创建多级目录
mkdir -p /path/to/nested/directory

# 创建目录并设置权限
mkdir -m 755 directory_name
```

### 4.3.7 创建链接

```bash
# 创建软链接（符号链接）
ln -s target_file link_name

# 创建硬链接
ln target_file link_name

# 示例
ln -s /etc/passwd passwd_link
```

## 4.4 文件查找

### 4.4.1 find命令

```bash
# 按名称查找
find /path -name "filename.txt"

# 按类型查找
find /path -type d          # 查找目录
find /path -type f          # 查找文件
find /path -type l          # 查找链接

# 按大小查找
find /path -size +100M      # 大于100MB
find /path -size -1k        # 小于1KB

# 按时间查找
find /path -mtime -7       # 7天内修改
find /path -atime +30      # 30天前访问

# 按权限查找
find /path -perm 755

# 执行操作
find /path -name "*.tmp" -delete
find /path -name "*.log" -exec rm {} \;
```

### 4.4.2 grep命令

```bash
# 在文件中查找字符串
grep "pattern" filename.txt

# 查找并显示行号
grep -n "pattern" filename.txt

# 递归查找
grep -r "pattern" /path/

# 忽略大小写
grep -i "pattern" filename.txt

# 只显示匹配的部分
grep -o "pattern" filename.txt

# 反向查找（不包含pattern的行）
grep -v "pattern" filename.txt

# 使用扩展正则表达式
grep -E "pattern1|pattern2" filename.txt
```

## 4.5 文件压缩与解压

### 4.5.1 gzip/gunzip

```bash
# 压缩文件
gzip filename.txt

# 解压缩
gunzip filename.txt.gz

# 压缩保留原文件
gzip -c filename.txt > filename.txt.gz

# 解压缩保留原压缩文件
gunzip -c filename.txt.gz > filename.txt
```

### 4.5.2 tar打包

```bash
# 打包（不压缩）
tar -cvf archive.tar /path/to/dir

# 解包
tar -xvf archive.tar

# 打包并压缩（gzip）
tar -zcvf archive.tar.gz /path/to/dir

# 解压并解包（gzip）
tar -zxvf archive.tar.gz

# 打包并压缩（bzip2）
tar -jcvf archive.tar.bz2 /path/to/dir

# 解压并解包（bzip2）
tar -jxvf archive.tar.bz2

# 解压到指定目录
tar -zxvf archive.tar.gz -C /destination/

# 查看压缩包内容
tar -tvf archive.tar.gz
```

### 4.5.3 zip/unzip

```bash
# 压缩文件和目录
zip -r archive.zip /path/to/dir

# 解压缩
unzip archive.zip

# 解压到指定目录
unzip archive.zip -d /destination/

# 列出压缩包内容
unzip -l archive.zip
```

---

# 第5章 用户与权限管理

## 5.1 用户系统基础

### 5.1.1 用户分类

| 用户类型 | UID范围 | 说明 |
|----------|---------|------|
| root | 0 | 超级管理员 |
| 系统用户 | 1-999 | 系统服务账户 |
| 普通用户 | 1000+ | 普通登录账户 |

### 5.1.2 用户相关文件

| 文件 | 说明 |
|------|------|
| /etc/passwd | 用户账户信息 |
| /etc/shadow | 用户密码（加密） |
| /etc/group | 用户组信息 |

**/etc/passwd格式**：
```
username:password:UID:GID:comment:home_directory:shell
```

**/etc/shadow格式**：
```
username:encrypted_password:last_change:min_days:max_days:warn_days:inactive:expire
```

## 5.2 用户管理命令

### 5.2.1 添加用户

```bash
# 基本添加用户
sudo useradd username

# 创建用户并指定主组
sudo useradd -g groupname username

# 创建用户并指定附加组
sudo useradd -G group1,group2 username

# 创建用户并创建家目录
sudo useradd -m username

# 完整示例
sudo useradd -m -g shehui -G qianrushi xiaochen
```

### 5.2.2 设置用户密码

```bash
# 为当前用户设置密码
passwd

# 为指定用户设置密码（需要root权限）
sudo passwd username
```

### 5.2.3 查看用户信息

```bash
# 查看用户是否存在
id username

# 查看用户详细信息
cat /etc/passwd

# 查看用户所属组
groups username

# 查看登录用户
who

# 查看详细登录信息
w
```

### 5.2.4 修改用户

```bash
# 修改用户名
sudo usermod -l new_username old_username

# 修改用户家目录
sudo usermod -d /home/new_home -m username

# 添加用户到组
sudo usermod -aG groupname username

# 修改用户主组
sudo usermod -g groupname username
```

### 5.2.5 删除用户

```bash
# 删除用户但保留家目录
sudo userdel username

# 删除用户及家目录
sudo userdel -r username
```

## 5.3 组管理命令

### 5.3.1 组操作

```bash
# 添加组
sudo groupadd groupname

# 删除组
sudo groupdel groupname

# 修改组名
sudo groupmod -n new_name old_name

# 查看所有组
cat /etc/group
```

### 5.3.2 用户组管理

```bash
# 添加用户到组
sudo gpasswd -a username groupname

# 从组中删除用户
sudo gpasswd -d username groupname

# 设置组管理员
sudo gpasswd -A username groupname
```

## 5.4 权限管理

### 5.4.1 权限表示

```
rwxr-xr-x
├──┼─┤├──┼─┤
│  │  │  │
│  │  │  └── 其他用户权限
│  │  └───── 组用户权限
│  └───────── 所有者权限
└──────────── 文件类型
```

**权限数值**：
| 权限 | 数值 |
|------|------|
| r（读） | 4 |
| w（写） | 2 |
| x（执行） | 1 |
| -（无权限） | 0 |

**常用权限组合**：
| 权限 | 数值 | 说明 |
|------|------|------|
| rwx | 7 | 读、写、执行 |
| rw- | 6 | 读、写 |
| r-x | 5 | 读、执行 |
| r-- | 4 | 只读 |
| --- | 0 | 无权限 |

### 5.4.2 chmod - 修改权限

```bash
# 使用数字设置权限
chmod 755 filename
chmod 644 filename
chmod 600 filename

# 使用符号设置权限
# u=所有者 g=组 o=其他 a=所有
chmod u+x filename          # 添加执行权限
chmod u-x filename          # 移除执行权限
chmod u=rw filename         # 设置读写权限
chmod g+rw filename         # 组添加读写
chmod o=r filename          # 其他设置只读
chmod a+x filename          # 所有用户添加执行

# 递归修改目录权限
chmod -R 755 directory/

# 常见示例
chmod 777 filename          # 所有用户可读写执行
chmod 755 filename          # 所有者全部，其他人读执行
chmod 644 filename          # 所有者读写，其他人只读
chmod 600 filename          # 仅所有者读写
```

### 5.4.3 chown - 修改所有者

```bash
# 修改文件所有者
sudo chown username filename

# 修改所有者和组
sudo chown username:groupname filename

# 递归修改
sudo chown -R username:groupname directory/

# 只修改组
sudo chgrp groupname filename
```

### 5.4.4 权限对文件和目录的意义

**对文件**：
| 权限 | 含义 |
|------|------|
| r | 可以读取文件内容 |
| w | 可以修改文件内容 |
| x | 可以执行文件（脚本/程序） |

**对目录**：
| 权限 | 含义 |
|------|------|
| r | 可以列出目录内容（ls） |
| w | 可以在目录中创建/删除文件 |
| x | 可以进入目录（cd） |

## 5.5 sudo权限配置

### 5.5.1 让用户使用sudo无需密码

```bash
# 编辑sudoers文件
sudo visudo

# 添加以下行（允许sudo组成员无需密码）
%sudo ALL=(ALL) NOPASSWD: ALL
```

### 5.5.2 添加用户到sudo组

```bash
# 将用户添加到sudo组
sudo usermod -aG sudo username

# 验证
groups username
```

## 5.6 su命令 - 切换用户

```bash
# 切换到指定用户
su username

# 切换到指定用户并加载其环境
su - username

# 切换到root用户
su -

# 切换到root（需要输入root密码）
sudo su -
```

---

# 第6章 软件包管理

## 6.1 APT包管理系统

### 6.1.1 APT简介

APT（Advanced Packaging Tool）是Debian/Ubuntu的包管理工具，自动处理依赖关系，简化软件安装、更新和删除过程。

### 6.1.2 源列表配置

**源文件位置**：
- /etc/apt/sources.list
- /etc/apt/sources.list.d/*.list

**sources.list格式**：
```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
```

**常用镜像源**：
| 镜像 | 地址 |
|------|------|
| 阿里云 | mirrors.aliyun.com |
| 清华 | mirrors.tuna.tsinghua.edu.cn |
| 中科大 | mirrors.ustc.edu.cn |
| 网易 | mirrors.163.com |

### 6.1.3 换源步骤

```bash
# 1. 备份原源列表
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

# 2. 编辑源列表
sudo nano /etc/apt/sources.list

# 3. 更新软件包列表
sudo apt update

# 4. 升级所有软件包
sudo apt upgrade
```

## 6.2 常用APT命令

### 6.2.1 更新与安装

```bash
# 更新软件包列表
sudo apt update

# 安装软件包
sudo apt install package_name

# 重新安装软件包
sudo apt reinstall package_name

# 安装时自动删除不需要的包
sudo apt install package_name --auto-remove
```

### 6.2.2 升级

```bash
# 升级所有可升级的软件包
sudo apt upgrade

# 升级系统（包括处理依赖变化）
sudo apt full-upgrade

# 列出可升级的包
apt list --upgradable
```

### 6.2.3 删除

```bash
# 删除软件包（保留配置）
sudo apt remove package_name

# 删除软件包及配置
sudo apt purge package_name

# 自动删除不需要的依赖包
sudo apt autoremove

# 删除缓存的安装包
sudo apt clean
```

### 6.2.4 查询

```bash
# 搜索软件包
apt search package_name

# 显示软件包信息
apt show package_name

# 查看软件包是否已安装
apt list --installed

# 查看软件包版本
apt-cache policy package_name
```

### 6.2.5 查看已安装软件

```bash
# 列出所有已安装包
dpkg -l

# 只显示包名
dpkg -l | awk '{print $2}'

# 使用apt
apt list --installed

# 查看特定包的文件列表
dpkg -L package_name

# 查找文件属于哪个包
dpkg -S /path/to/file
```

## 6.3 dpkg命令

dpkg是APT的底层包管理工具，直接处理.deb文件。

```bash
# 安装.deb包
sudo dpkg -i package.deb

# 卸载包
sudo dpkg -r package_name

# 完全卸载（包括配置）
sudo dpkg -P package_name

# 查看包信息
dpkg -s package_name

# 查看包文件列表
dpkg -L package_name

# 修复损坏的包
sudo dpkg --configure -a

# 列出所有已安装包
dpkg -l
```

## 6.4 常用软件安装示例

```bash
# 安装开发工具
sudo apt install build-essential

# 安装网络工具
sudo apt install net-tools
sudo apt install openssh-client

# 安装常用工具
sudo apt install vim curl wget git

# 安装Python
sudo apt install python3 python3-pip

# 安装数据库
sudo apt install mysql-server
sudo apt install postgresql

# 安装Web服务器
sudo apt install apache2 nginx
```

## 6.5 添加第三方仓库

```bash
# 添加PPA仓库（个人软件包存档）
sudo add-apt-repository ppa:repository-name
sudo apt update
sudo apt install package_name

# 添加仓库并导入密钥
wget -qO - https://example.com/key.gpg | sudo apt-key add -
echo "deb https://repo.example.com/ stable main" | sudo tee /etc/apt/sources.list.d/repo.list
sudo apt update
```

## 6.6 wget下载工具

```bash
# 基本下载
wget http://example.com/file.zip

# 指定输出文件名
wget -O output.zip http://example.com/file.zip

# 指定下载目录
wget -P /path/to/dir http://example.com/file.zip

# 断点续传
wget -c http://example.com/largefile.zip

# 后台下载
wget -b http://example.com/file.zip

# 复制网站
wget -r -np -nH --cut-dirs=2 http://example.com/path/
```

---

# 第7章 网络配置与管理

## 7.1 网络基础

### 7.1.1 查看网络信息

```bash
# 查看所有网络接口
ip a
# 或
ifconfig

# 查看特定接口
ip a show eth0

# 查看路由表
ip route

# 查看DNS配置
cat /etc/resolv.conf

# 测试网络连通性
ping -c 4 8.8.8.8

# 追踪路由
traceroute example.com
```

### 7.1.2 网络诊断工具

```bash
# 查看端口监听
sudo netstat -tlnp
# 或
sudo ss -tlnp

# 查看网络连接
netstat -an
# 或
ss -an

# 查看特定进程的网络连接
netstat -anp | grep process_name

# 查看端口占用
lsof -i :80
```

## 7.2 网络配置

### 7.2.1 Netplan配置（Ubuntu 18.04+）

**配置文件位置**：/etc/netplan/*.yaml

**配置示例**（DHCP自动获取）：
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: yes
```

**配置示例**（静态IP）：
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
```

**应用配置**：
```bash
sudo netplan apply
```

### 7.2.2 NetworkManager配置

```bash
# 查看网络连接状态
nmcli device status

# 开启/关闭网络接口
nmcli device set eth0 managed yes
nmcli device set eth0 managed no

# 查看连接列表
nmcli connection show

# 激活连接
nmcli connection up connection_name

# 关闭连接
nmcli connection down connection_name

# 创建新连接（静态IP）
nmcli connection add type ethernet con-name "static_eth0" ifname eth0
nmcli connection modify "static_eth0" ipv4.addresses 192.168.1.100/24
nmcli connection modify "static_eth0" ipv4.gateway 192.168.1.1
nmcli connection modify "static_eth0" ipv4.dns "8.8.8.8,8.8.4.4"
nmcli connection modify "static_eth0" ipv4.method manual
nmcli connection up "static_eth0"
```

### 7.2.3 旧式/etc/network/interfaces配置

```bash
# 编辑网络配置文件
sudo nano /etc/network/interfaces

# 添加以下内容
auto eth0
iface eth0 inet static
address 192.168.1.100
netmask 255.255.255.0
gateway 192.168.1.1
dns-nameservers 8.8.8.8 8.8.4.4

# 重启网络服务
sudo systemctl restart networking
```

## 7.3 网络服务管理

```bash
# 查看服务状态
systemctl status NetworkManager

# 重启网络服务
sudo systemctl restart NetworkManager

# 设置开机启动
sudo systemctl enable NetworkManager

# 禁用开机启动
sudo systemctl disable NetworkManager
```

---

# 第8章 进程与服务管理

## 8.1 进程基础

### 8.1.1 进程与程序的区别

- **程序**：存储在磁盘上的可执行文件
- **进程**：正在运行的程序的实例，拥有独立的内存空间

### 8.1.2 进程相关文件

| 文件 | 说明 |
|------|------|
| /proc/PID/status | 进程状态 |
| /proc/PID/maps | 进程内存映射 |
| /proc/PID/fd | 进程打开的文件 |

## 8.2 进程查看

### 8.2.1 ps命令

```bash
# 查看当前终端的进程
ps

# 查看所有进程
ps -ef

# 查看所有进程（BSD格式）
ps aux

# 查看特定用户进程
ps -u username

# 查看进程树
pstree

# 查看特定进程
ps -ef | grep process_name
```

**ps aux输出说明**：
| 列 | 说明 |
|----|------|
| USER | 进程用户 |
| PID | 进程ID |
| %CPU | CPU占用率 |
| %MEM | 内存占用率 |
| VSZ | 虚拟内存大小 |
| RSS | 实际内存大小 |
| TTY | 终端 |
| STAT | 进程状态 |
| START | 启动时间 |
| COMMAND | 命令 |

### 8.2.2 top命令

```bash
# 启动top
top

# 交互命令
# q - 退出
# h - 帮助
# k - 终止进程
# r - 修改nice值
# M - 按内存排序
# P - 按CPU排序
# 1 - 显示所有CPU核心
```

**top输出说明**：
| 行 | 说明 |
|----|------|
| 第一行 | 系统时间、运行时间、用户数、负载均值 |
| 第二行 | 任务（进程）统计 |
| 第三行 | CPU使用情况 |
| 第四行 | 物理内存使用 |
| 第五行 | 交换分区使用 |
| 进程列表 | 各进程资源占用详情 |

### 8.2.3 其他查看命令

```bash
# 查看内存使用
free -h

# 查看磁盘IO
iostat

# 查看进程实时资源
htop
```

## 8.3 进程控制

### 8.3.1 kill命令

```bash
# 终止进程（默认SIGTERM）
kill PID

# 强制终止进程（SIGKILL）
kill -9 PID

# 列出所有信号
kill -l

# 终止进程组
kill -9 -PGID

# 常见信号
# 1 - SIGHUP  挂起
# 9 - SIGKILL 强制终止
# 15 - SIGTERM 正常终止（默认）
```

### 8.3.2 killall命令

```bash
# 按进程名终止
killall process_name

# 强制终止
killall -9 process_name

# 终止所有匹配进程
killall -9 nginx
```

### 8.3.3 pkill命令

```bash
# 按名称终止进程
pkill process_name

# 终止特定用户的进程
pkill -u username process_name
```

## 8.4 服务管理

### 8.4.1 systemd服务

```bash
# 查看服务状态
systemctl status service_name

# 启动服务
sudo systemctl start service_name

# 停止服务
sudo systemctl stop service_name

# 重启服务
sudo systemctl restart service_name

# 重新加载配置
sudo systemctl reload service_name

# 设置开机启动
sudo systemctl enable service_name

# 禁用开机启动
sudo systemctl disable service_name

# 查看所有服务
systemctl list-units --type=service

# 查看服务是否开机启动
systemctl is-enabled service_name

# 查看失败的服务
systemctl --failed --type=service
```

### 8.4.2 服务配置文件

**位置**：/lib/systemd/system/

**示例服务文件**（nginx.service）：
```ini
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=network.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID

[Install]
WantedBy=multi-user.target
```

### 8.4.3 journalctl日志查看

```bash
# 查看服务日志
sudo journalctl -u service_name

# 实时查看日志
sudo journalctl -u service_name -f

# 查看最近日志
sudo journalctl -u service_name --no-pager -n 50

# 按时间查看
sudo journalctl -u service_name --since "2024-01-01"
```

---

# 第9章 磁盘管理

## 9.1 磁盘基础

### 9.1.1 磁盘相关概念

| 概念 | 说明 |
|------|------|
| 磁道(Track) | 磁盘表面的同心圆 |
| 扇区(Sector) | 磁道上的扇形区域，512B或4KB |
| 柱面(Cylinder) | 不同盘片同一半径的磁道组合 |
| 分区(Partition) | 逻辑上划分的存储区域 |

### 9.1.2 分区类型

| 类型 | 说明 |
|------|------|
| 主分区(Primary) | 最多4个，可启动 |
| 扩展分区(Extended) | 最多1个，不能直接使用 |
| 逻辑分区(Logical) | 在扩展分区内创建，无数量限制 |

### 9.1.3 分区表类型

**MBR分区表**：
- 最多4个主分区或3主分区+1扩展分区
- 最大支持2TB磁盘
- 使用CHS寻址

**GPT分区表**：
- 最多128个分区
- 支持超大磁盘（>2TB）
- 使用LBA寻址
- UEFI启动必需

## 9.2 分区管理工具

### 9.2.1 fdisk命令

```bash
# 查看磁盘分区
sudo fdisk -l
sudo fdisk -l /dev/sda

# 进入交互式分区编辑器
sudo fdisk /dev/sdb

# 交互命令
# m - 帮助
# p - 显示分区表
# n - 新建分区
# d - 删除分区
# t - 更改分区类型
# w - 保存退出
# q - 不保存退出
```

**创建新分区示例**：
```bash
sudo fdisk /dev/sdb
# 输入 n 新建分区
# 选择分区号
# 选择起始扇区
# 选择结束扇区或大小（如 +100M）
# 输入 w 保存退出
```

### 9.2.2 parted命令

```bash
# 启动parted
sudo parted /dev/sdb

# 交互命令
# mklabel gpt      创建GPT分区表
# mkpart primary ext4 0% 100%   创建占满整个磁盘的分区
# print            显示分区表
# rm 1            删除分区1
# quit            退出
```

## 9.3 格式化文件系统

```bash
# 格式化为ext4
sudo mkfs.ext4 /dev/sdb1

# 格式化为xfs
sudo mkfs.xfs /dev/sdb1

# 格式化为vfat
sudo mkfs.vfat /dev/sdb1

# 格式化为ntfs
sudo mkfs.ntfs /dev/sdb1

# 创建swap分区
sudo mkswap /dev/sdb2
sudo swapon /dev/sdb2
```

## 9.4 挂载管理

### 9.4.1 挂载命令

```bash
# 挂载
sudo mount /dev/sdb1 /mnt

# 卸载
sudo umount /mnt

# 强制卸载
sudo umount -f /mnt

# 查看挂载情况
df -h

# 查看所有挂载
mount
```

### 9.4.2 挂载选项

```bash
# 常用挂载选项
mount -o ro /dev/sdb1 /mnt      # 只读
mount -o rw /dev/sdb1 /mnt      # 读写
mount -o noexec /dev/sdb1 /mnt  # 禁止执行
mount -o loop file.iso /mnt      # 挂载镜像
```

### 9.4.3 /etc/fstab配置

```
# 格式：<device> <mount_point> <type> <options> <dump> <pass>
UUID=xxxx-xxxx  /boot  ext4  defaults  0  2
/dev/sdb1       /data  ext4  defaults  0  2
```

**获取UUID**：
```bash
sudo blkid
```

## 9.5 磁盘使用查看

```bash
# 查看磁盘使用
df -h

# 查看特定目录大小
du -sh /path/to/dir

# 查看目录详细大小
du -h --max-depth=1 /path/to/dir

# 查看磁盘IO
iostat -x 1

# 查看磁盘读写速度
hdparm -t /dev/sda
```

---

# 第10章 计划任务

## 10.1 crontab计划任务

### 10.1.1 crontab基本格式

```
*  *  *  *  *  command
│  │  │  │  │
│  │  │  │  └─── 星期 (0-7, 0和7都是周日)
│  │  │  └────── 月份 (1-12)
│  │  └───────── 日期 (1-31)
│  └──────────── 小时 (0-23)
└──────────────── 分钟 (0-59)
```

### 10.1.2 特殊字符

| 符号 | 说明 |
|------|------|
| * | 任意值 |
| , | 枚举，如1,3,5 |
| - | 范围，如1-5 |
| / | 步长，如*/5表示每5个单位 |

### 10.1.3 常用crontab示例

```bash
# 每分钟执行
* * * * * /path/to/command

# 每天凌晨2点执行
0 2 * * * /path/to/command

# 每周一早上6点执行
0 6 * * 1 /path/to/command

# 每月1日凌晨3点执行
0 3 1 * * /path/to/command

# 每5分钟执行
*/5 * * * * /path/to/command

# 每天8点到18点每半小时执行
*/30 8-18 * * * /path/to/command

# 每周一到周五每小时执行
0 * * * 1-5 /path/to/command
```

### 10.1.4 crontab命令

```bash
# 编辑crontab
crontab -e

# 查看crontab
crontab -l

# 删除crontab
crontab -r

# 以指定用户身份编辑
sudo crontab -u username -e

# 系统级crontab（推荐方式）
sudo nano /etc/crontab
```

### 10.1.5 注意事项

1. **环境变量**：crontab中可能没有PATH，建议使用绝对路径
2. **输出重定向**：默认发邮件，建议重定向到文件或/dev/null
3. **时间错误**：使用24小时制

**示例**：
```bash
# 将输出重定向到日志
0 2 * * * /path/to/script.sh >> /var/log/script.log 2>&1

# 不输出任何内容
0 2 * * * /path/to/script.sh > /dev/null 2>&1
```

## 10.2 at一次性任务

```bash
# 在指定时间执行
at 10:00
at> touch /tmp/test
at> <EOT>

# 明天10点执行
at 10:00 tomorrow

# 3天后执行
at 10:00 + 3 days

# 查看待执行任务
atq

# 删除任务
atrm job_number
```

## 10.3 系统定时任务目录

```bash
# 系统定时任务目录
/etc/cron.d/
/etc/cron.daily/    # 每天执行
/etc/cron.hourly/    # 每小时执行
/etc/cron.weekly/    # 每周执行
/etc/cron.monthly/   # 每月执行

# 禁止执行的脚本
/etc/cron.deny
```

---

# 第11章 SSH远程登录

## 11.1 SSH简介

SSH（Secure Shell）是一种加密的网络协议，用于安全地远程登录和操作服务器。

## 11.2 安装SSH服务

```bash
# Ubuntu客户端已预装ssh命令
# 安装SSH服务器
sudo apt install openssh-server

# 启动SSH服务
sudo systemctl start ssh

# 设置开机启动
sudo systemctl enable ssh

# 查看状态
sudo systemctl status ssh
```

## 11.3 SSH配置文件

**主配置文件**：/etc/ssh/sshd_config

**常用配置项**：
```
Port 22                    # 监听端口
PermitRootLogin no          # 禁止root登录
PasswordAuthentication yes  # 允许密码认证
PubkeyAuthentication yes    # 允许公钥认证
```

## 11.4 SSH客户端使用

### 11.4.1 基本连接

```bash
# 连接远程服务器
ssh username@server_ip

# 指定端口
ssh -p 2222 username@server_ip

# 首次连接（不验证密钥）
ssh -o StrictHostKeyChecking=no username@server_ip
```

### 11.4.2 SSH密钥登录

**1. 生成密钥对**：
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**2. 上传公钥到服务器**：
```bash
ssh-copy-id username@server_ip
```

**3. 配置服务器启用公钥认证**：
```bash
sudo nano /etc/ssh/sshd_config
# 确保以下配置
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

sudo systemctl restart ssh
```

## 11.5 SSH高级用法

### 11.5.1 SSH配置文件

**客户端配置**：~/.ssh/config
```
Host alias
    HostName server_ip
    User username
    Port 22
    IdentityFile ~/.ssh/id_rsa
```

### 11.5.2 SSH隧道

```bash
# 本地端口转发
ssh -L 8080:localhost:80 username@server_ip

# 远程端口转发
ssh -R 8080:localhost:80 username@server_ip

# 动态端口转发（SOCKS代理）
ssh -D 1080 username@server_ip
```

### 11.5.3 SCP文件传输

```bash
# 上传文件
scp local_file username@server_ip:/path/

# 下载文件
scp username@server_ip:/path/file local_path/

# 上传目录
scp -r local_dir username@server_ip:/path/

# 指定端口
scp -P 2222 local_file username@server_ip:/path/
```

## 11.6 启用root远程登录

```bash
# 1. 设置root密码
sudo passwd root

# 2. 编辑SSH配置
sudo nano /etc/ssh/sshd_config
# 添加或修改
PermitRootLogin yes

# 3. 重启SSH服务
sudo systemctl restart ssh
```

---

# 第12章 系统安全

## 12.1 防火墙UFW

### 12.1.1 UFW基本命令

```bash
# 查看状态
sudo ufw status

# 查看详细状态
sudo ufw status verbose

# 启用防火墙
sudo ufw enable

# 禁用防火墙
sudo ufw disable

# 重置防火墙
sudo ufw reset
```

### 12.1.2 规则管理

```bash
# 允许端口
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# 拒绝端口
sudo ufw deny 3306/tcp

# 删除规则
sudo ufw delete allow 80/tcp

# 允许特定IP
sudo ufw allow from 192.168.1.100

# 允许特定IP访问特定端口
sudo ufw allow from 192.168.1.100 to any port 22

# 限制IP访问（防止暴力破解）
sudo ufw limit 22/tcp
```

### 12.1.3 应用配置

```bash
# 查看可用应用配置
sudo ufw app list

# 查看应用详情
sudo ufw app info 'Nginx Full'

# 允许应用
sudo ufw allow 'Nginx Full'
```

## 12.2 fail2ban防暴力破解

```bash
# 安装
sudo apt install fail2ban

# 启动并设置开机启动
sudo systemctl enable fail2ban
sudo systemctl start fail2ban

# 查看状态
sudo fail2ban-client status

# 查看特定 jail 状态
sudo fail2ban-client status sshd
```

## 12.3 系统更新

```bash
# 检查更新
sudo apt update

# 升级所有包
sudo apt upgrade

# 完整升级（处理依赖变化）
sudo apt full-upgrade

# 自动安全更新
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
```

## 12.4 SELinux/AppArmor

Ubuntu使用AppArmor作为安全模块：

```bash
# 查看AppArmor状态
sudo apparmor_status

# 查看程序配置文件
ls /etc/apparmor.d/
```

---

# 第13章 Vim编辑器

## 13.1 Vim三种模式

### 13.1.1 模式转换

```
        ┌─────────────────┐
        │  正常模式        │
        │ (按 i 进入)     │
        └────────┬────────┘
                 │
        ┌────────▼────────┐
        │  插入模式        │
        │ (按 Esc 返回)   │
        └────────┬────────┘
                 │
        ┌────────▼────────┐
        │  命令行模式      │
        │ (按 : 进入)     │
        └─────────────────┘
```

### 13.1.2 各模式功能

| 模式 | 功能 |
|------|------|
| 正常模式 | 光标移动、删除、复制、粘贴 |
| 插入模式 | 输入文本 |
| 命令行模式 | 保存、退出、搜索、替换 |

## 13.2 正常模式操作

### 13.2.1 光标移动

| 按键 | 功能 |
|------|------|
| h | 左移 |
| j | 下移 |
| k | 上移 |
| l | 右移 |
| w | 下一个单词开头 |
| b | 上一个单词开头 |
| 0 | 行首 |
| $ | 行尾 |
| gg | 文件开头 |
| G | 文件结尾 |
| :n | 跳转到第n行 |

### 13.2.2 文本操作

| 按键 | 功能 |
|------|------|
| x | 删除当前字符 |
| dd | 删除当前行 |
| dw | 删除到单词末尾 |
| d$ | 删除到行尾 |
| d0 | 删除到行首 |
| yy | 复制当前行 |
| yw | 复制到单词末尾 |
| p | 粘贴到光标后 |
| P | 粘贴到光标前 |
| u | 撤销 |
| Ctrl + r | 重做 |
| . | 重复上次操作 |

### 13.2.3 可视模式

| 按键 | 功能 |
|------|------|
| v | 进入字符可视模式 |
| V | 进入行可视模式 |
| Ctrl + v | 进入块可视模式 |

## 13.3 插入模式操作

| 按键 | 功能 |
|------|------|
| i | 在光标前插入 |
| a | 在光标后插入 |
| I | 在行首插入 |
| A | 在行尾插入 |
| o | 在下行插入新行 |
| O | 在上行插入新行 |

## 13.4 命令行模式

### 13.4.1 基本命令

| 命令 | 功能 |
|------|------|
| :w | 保存 |
| :q | 退出 |
| :wq | 保存并退出 |
| :q! | 强制退出（不保存） |
| :x | 保存并退出 |
| :w filename | 另存为 |
| :e filename | 打开文件 |

### 13.4.2 搜索与替换

| 命令 | 功能 |
|------|------|
| /pattern | 向下搜索 |
| ?pattern | 向上搜索 |
| n | 下一个匹配 |
| N | 上一个匹配 |
| :s/old/new | 替换当前行第一个 |
| :s/old/new/g | 替换当前行所有 |
| :%s/old/new/g | 替换文件所有 |

### 13.4.3 其他命令

| 命令 | 功能 |
|------|------|
| :set nu | 显示行号 |
| :set nonu | 隐藏行号 |
| :set hlsearch | 高亮搜索 |
| :nohlsearch | 取消高亮 |
| :set tabstop=4 | 设置Tab宽度 |

## 13.5 Vim配置

### 13.5.1 用户配置文件

创建 ~/.vimrc：
```vim
" 显示行号
set number

" 显示相对行号
set relativenumber

" 语法高亮
syntax on

" 设置缩进
set tabstop=4
set shiftwidth=4
set expandtab

" 自动缩进
set autoindent

" 搜索设置
set incsearch
set hlsearch

" 显示当前行
set cursorline

" 设置编码
set encoding=utf-8
```

---

# 第14章 开机启动与运行级别

## 14.1 systemd与运行级别

### 14.1.1 Ubuntu运行级别

| 级别 | 名称 | 说明 |
|------|------|------|
| 0 | 关机 | 系统关机 |
| 1 | 单用户 | 恢复模式/安全模式 |
| 2-5 | 多用户 | 正常启动（2无GUI，5有GUI） |
| 6 | 重启 | 系统重启 |

### 14.1.2 systemd目标

| 目标 | 说明 |
|------|------|
| multi-user.target | 多用户，无GUI |
| graphical.target | 多用户，有GUI |
| rescue.target | 救援模式 |
| emergency.target | 紧急模式 |

### 14.1.3 切换运行级别

```bash
# 查看当前目标
systemctl get-default

# 设置默认目标
sudo systemctl set-default multi-user.target   # 命令行
sudo systemctl set-default graphical.target     # 图形界面

# 临时切换
sudo systemctl isolate multi-user.target
sudo systemctl isolate graphical.target
```

## 14.2 开机启动管理

### 14.2.1 rc.local（传统方式）

```bash
# 创建rc.local
sudo nano /etc/rc.local

# 添加内容
#!/bin/bash
echo "Hello" > /tmp/hello.log
exit 0

# 设置执行权限
sudo chmod +x /etc/rc.local
```

### 14.2.2 systemd服务方式

```bash
# 创建服务文件
sudo nano /etc/systemd/system/myservice.service

# 内容
[Unit]
Description=My Service
After=network.target

[Service]
Type=oneshot
ExecStart=/path/to/script.sh
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

# 启用服务
sudo systemctl enable myservice.service
```

### 14.2.3 cron @reboot

```bash
# 编辑crontab
crontab -e

# 添加
@reboot /path/to/script.sh
```

## 14.3 GRUB引导管理器

### 14.3.1 GRUB配置文件

**位置**：/boot/grub/grub.cfg

### 14.3.2 修改默认启动项

```bash
# 查看启动项
grep menuentry /boot/grub/grub.cfg

# 设置默认启动项（从0开始）
sudo nano /etc/default/grub
GRUB_DEFAULT=0

# 更新GRUB
sudo update-grub
```

### 14.3.3 恢复GRUB

```bash
# 从Live USB启动后
sudo mount /dev/sda1 /mnt
sudo grub-install --root-directory=/mnt /dev/sda
sudo update-grub
```

## 14.4 关机与重启

```bash
# 立即关机
sudo shutdown -h now

# 定时关机（1分钟后）
sudo shutdown -h 1

# 取消关机
sudo shutdown -c

# 立即重启
sudo reboot
# 或
sudo shutdown -r now

# 关机（halt）
sudo halt

# 同步数据到磁盘
sync
```

**注意事项**：
1. 关机或重启前先执行sync同步数据
2. 远程操作时注意通知用户

---

# 附录

## 附录A 常用命令速查表

### 文件操作
| 命令 | 说明 |
|------|------|
| ls | 列出目录 |
| cd | 切换目录 |
| pwd | 显示当前目录 |
| mkdir | 创建目录 |
| rm | 删除文件/目录 |
| cp | 复制 |
| mv | 移动/重命名 |
| touch | 创建文件 |
| cat | 查看文件 |
| chmod | 修改权限 |
| chown | 修改所有者 |

### 系统管理
| 命令 | 说明 |
|------|------|
| sudo | 超级权限 |
| apt | 包管理 |
| systemctl | 服务管理 |
| ps | 进程查看 |
| top | 任务管理器 |
| kill | 终止进程 |
| df | 磁盘使用 |
| du | 目录大小 |
| free | 内存使用 |

### 网络
| 命令 | 说明 |
|------|------|
| ip | 网络配置 |
| ping | 测试连通 |
| ssh | 远程登录 |
| scp | 远程复制 |
| wget | 下载文件 |
| curl | HTTP请求 |
| netstat | 网络状态 |
| ss | 套接字统计 |

## 附录B 环境变量

### 常见环境变量

| 变量 | 说明 |
|------|------|
| HOME | 用户主目录 |
| PATH | 命令搜索路径 |
| USER | 当前用户 |
| SHELL | 默认Shell |
| PWD | 当前目录 |
| LANG | 语言设置 |

### 操作环境变量

```bash
# 查看所有环境变量
env

# 查看单个变量
echo $PATH

# 设置临时变量
export PATH=/new/path:$PATH

# 设置永久变量（用户级）
echo 'export PATH=/new/path:$PATH' >> ~/.bashrc

# 设置永久变量（系统级）
sudo nano /etc/environment
```

---

*本讲义基于Ubuntu 22.04/24.04 LTS版本编写，适合Linux初学者学习使用。*

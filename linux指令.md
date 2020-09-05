# linux指令



## ls

- -a 显示隐藏文件，以点开头

- -lh 以列表显示，h用于更好的表示内存

- '*' '?' '[A-z]' 等正则表达式

- ```
  ls -lh
  ```

- | 目录 | 拥有者权限 | 组权限 | 其他用户权限 | 硬链接数 | 用户 |  组  |
  | :--: | :--------: | :----: | :----------: | :------: | :--: | :--: |
  |  d   |    rwx     |  r-x   |     r-x      |    3     | zxc  | zxc  |

## cd

- 直接cd返回家目录
- cd ‘-’ 返回上一次的目录
- cd ~ 用户目录

## mkdir

- -p 递归创建目录

- ```
  mkdir -p a/b/c/d
  ```

## touch

- 如果文件不存在，则创建，如果存在，则修改文件的末次修改日期

## rm

- 美好的rm -rf *，这表示rm也支持正则

## tree

- ```
  sudo apt install tree
  ```

- -d 只展示目录

## cp

- -i 覆盖提示
- -r 递归复制

## mv

- -i 覆盖提示

## cat

- -b 显示非空行的行数
- -n 显示所有行的行数

## more

- 空格 enter 
- b back
- f forward
- q quit

## grep

- -n 显示行数

- -v 匹配行取反

- -i 不区分大小写

- 匹配支持正则

- ```
  grep -n '^[a-zA-Z]*;' linux_learning/demo.txt
  ```

## 重定向

- echo

- '>' 覆盖

- '>>' 追加

- 可以直接生成新文件

- ```
  tree >> linux_learning/demo.txt
  cat linux_learning/demo.txt
  ```

## 管道

- 左边的结果作为输入，输入到右边，右边进行处理，进行输出

- ```
  ls -lha ~ | more
  ls -lha ~ | grep '\.[a-zA-Z]*a'
  ```

## shutdown

- 默认1分钟
- -c 取消关机
- -r 重新启动
- 需要sudo权限

## ifconfig

- 结合管道和grep
- ping ip地址
- time越小网速越快

## 硬链接

- 绝对路径

- 当前目录'.'

- 各个子目录的父亲'..'(多个) 

- 当给某文件建立硬链接后，删除源文件，硬链接不会受到影响

- > 在linux中，文件名和文件数据是分开存储的，文件名和硬链接都可以访问文件数据

## chmod

- -x 则不能执行常用指令

- -r 无法读取，一些指令受限

- -w 无法写入/修改，包括创建等指令

- -R 递归修改目录权限，大写

- ```
  ls -l Documents/front_end/
  chmod -R 755 Documents/front_end/test.html
  ```

## group

- ```
  sudo groupadd dev
  sudo groupdel dev
  cat /etc/group
  ```

- ```
  chgrp -R dev demo
  ```

  - -R 递归修改目录，大写

## user

- ```
  sudo useradd -mg dev ddd
  sudo passwd ddd
  ```

  - -m 自动创建用户目录
  - -g 指定组名

- ```
  sudo userdel -r ddd
  cat -n /etc/passwd
  ```

  - -r 自动删除用户目录


## id

- ```
  id zxc
  等价于
  cat -n /etc/passwd | grep zxc
  cat -n /etc/group | grep zxc
  ```

- /etc/passwd含有一些信息：用户名：密码：uid：gid：全名：家目录：终端

## 主组、附加组

- -g 修改主组

- -G 添加附加组

- -s 修改shell

- 修改后需要重新登陆

- gpasswd -d USER GROUP 移除某用户

- ```
  sudo usermod -G sudo ddd
  cat -n /etc/shells
  sudo usermod -s /bin/bash ddd
  ```

## which

- 用于查看指令所处的文件
- 无法找到cd，因为它在内核里

## su

- su - ddd切换到ddd，且目录变为ddd的家目录
- 不加'-'则不会切换目录
- sudo su -切换到root
- exit退出

## 系统信息

- ```
  date
  cal
  ```

- df -h 显示整个磁盘剩余空间

- du-h 显示当前目录内存使用情况

- -h 同上

## 进程

- ```
  ps aux
  ```

- 不加参数，只显示自己用户的终端进程

- a 显示所有用户的终端进程

- u 显示详细状态

- x 显示所有的进程，包括非终端启动的

- ```
  top
  ```

- 按q退出

- ```
  kill -9 9117
  ```

- kill后接pid，可用ps au查看

- -9 强制执行

## find

- ```
  find -name "*.txt"
  find Desktop/ -name "*mo.*"
  ```

- -name 后加双引号，里面支持正则

- find后可直接加目录，默认是当前目录

## 软连接

- ```
  ln -s 文件绝对路径 软连接路径
  ```

- -s 软连接，不加则是硬链接

- 一定要写绝对路径，方便软连接的后期移动

- > 通过软连接可以找到文件名或硬链接

## tar

- -c 创建tar包，支持正则

- -x 解开tar包，解开时必须在tar包所在的父目录下

- -v 显示详细过程

- -f 一定是.tar文件

- -z gzip压缩，.gz格式

- -j bzip2压缩，.bz2格式

- -C 解压路径必须存在

- ```
  tar -zcvf Desktop/t1.tar.gz Documents/
  cd Desktop/
  tar -zxvf Desktop/t1.tar.gz -C Desktop/
  ```

## apt

- ```
  sudo apt install ...
  sudo apt remove ...
  sudo apt upgrade
  sudo apt update
  ```

- 
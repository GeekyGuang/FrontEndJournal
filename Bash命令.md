# Bash命令

### 英文缩写
| 英文 | 缩写 | 英文 | 缩写 |
| --- | --- | --- | --- |
| file |  | link | ln |
| make | mk | find | find |
| move | mv | echo | echo |
| remove | rm | touch | touch |
| copy | cp | change | cd中的c |
| list | ls | directory | cd中的d |
| recursive |  | force |  |

### 命令
| 命令 | 作用 | 备注 |
| --- | --- | --- |
| ctrl + C | 中断操作(救命键) |  |
| cd ~ | 进到用户目录 | ~ 是用户目录 |
| pwd | 显示当前目录 | print working directory |
| ls | 显示当前目录内容 | 不会显示 .开头的文件 |
| ls 路径 | 显示指定目录内容 |  |
| ls -l  | 显示详细信息 |  |
| ll | 是ls -l的别名，ubuntu默认不支持ll | 打开 ~/.bashrc
找到 #alias ll=’ls -l’，去掉前面的#就可以了。 |
|  |  |  |
| cat 路径 | 查看文件所有内容 |  |
| head 路径 | 查看文件内容，默认前10行 |  |
| head 路径 -n 14 | 最后数字自定义显示的行数 |  |
| tail 路径 | 查看文件内容，默认后10行 |  |
| tail 路径 -n 15 | 最后数字自定义显示的行数 |  |
| less 路径 | 滚动方式显示 | q 退出 |
|  |  |  |
| touch 1.txt | 新建空文件 |  |
| touch 1.txt 2.js 3.css | 同时创建多个文件 |  |
| echo hello | 将hello输出到终端 |  |
| echo hello > 1.txt | 将hello写入到文件(覆盖) |  |
| echo hello >> 1.txt | 写入文件(追加) |  |
| echo "1\n2" > 1.txt | 写入多行 | \n 换行符 |
|  |  |  |
| mkdir a | 创建文件夹a |  |
| mkdir a b | 同时创建多个文件夹 |  |
| mkdir ./a/b/c | 在文件夹b里创建c |  |
| mkdir -p a/b/c/d/e | 创建多层目录a/b/c/d/e | mkdir -p ./c/h/g |
|  |  |  |
| cp 1.txt 2.txt | 将文件1复制为2 | 如果2已存在则会被替换 |
| cp 1.txt a | 如果a是已存在的文件夹，则将1复制到a里，如果a不存在，则将1复制为a文件 |  |
| cp -r a b | 如果b文件夹存在，则将a文件夹复制到b里，否则将a复制为b | 如果b是已存在的文件，则复制失败 |
|  |  |  |
| rm 1.txt | 删除文件 |  |
| rm -r a | 删除文件夹 | r 代表 recursive |
| rm -rf a | 强制删除 | f 代表 force |
| rm -rf / | 清空根目录 | / 代表根目录 |
|  |  |  |
| code 1.txt | 用vscode打开 |  |
| start 1.txt | 用默认软件打开 |  |
| echo '' > 1.txt | 清空文件内容 |  |
| mv 1.txt d | 把1.txt移动到文件夹d |  |
| mv d/1.txt . | 把d里的1.txt移到当前目录 | . 代表当前目录 |
| mv 1.txt 2.txt | 重命名 |  |
| touch 1.txt | 更新文件的最后更新时间 |  |
|  |  |  |
| Alt + .  | 上一次的参数 |  |
| 上下方向键 | 上一次的命令 |  |

### tldr
安装tldr查看命令行工具(too long, didn't read)
npm i -g tldr 或 yarn global add tldr
示例： tldr ls
### 路径
cd /d/software/  或 cd ~/a/b   从根目录(/)开始的路径(绝对路径)
cd a/b/c 或 cd ./a/b/c  从当前目录开始的路径(相对路径)


### 脚本
每条命令执行完都会有返回值，`echo $?`查看
用&&执行多条命令, 上一条成功才执行下一条： `rm 1.txt && touch 2.txt && echo 成功`
用;执行多条命令，每条都执行：`rm 1.txt; touch 2.txt; echo 成功`


新建一个脚本文件(不需要后缀)
`touch onekey`
`code onekey` 编辑文件
输入内容(回车代替 ; 结尾)：
`mkdir a`
`cd a`
`touch 1.txt`
`echo "hello\nagain" >> 1.txt`
运行脚本(必须用绝对路径)：
`./onekey`
如果是mac系统要先给可执行权限：
`chmod +x  ./onekey`
给脚本传参数($1)：
`mkdir $1`
`cd $1`
`touch 1.txt`
`echo "hello\nagain" >> 1.txt`
执行时传参数：
`./onekey aaa`


sh + 文件名 执行(sh是bash的缩写)：
`sh onekey`
添加shebang指定脚本解释器(略)
`#!/usr/bin/env sh`


添加path，直接输文件名就能执行
命令行的本质是可执行脚本文件
path路径在上面的先执行(exe文件优先)







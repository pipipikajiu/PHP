## 1 . 分布式版本控制系统:
- 1 . Git为了提高效率，对于没有被修改的文件，不会重复存储，而是创建一个 链接 指向之前存储过的文件.
## 2. 使用Git服务程序:
- 1 . Git的三种重要模式:
    - 1.1 . 已提交(committed):表示数据文件已经顺利提交到Git数据库中。
    - 1.2 . 已修改(modified):表示数据文件已经被修改，但未被保存到Git数据库中。
    - 1.3 . 已暂存(staged):表示数据文件已经被修改，并会在下次提交时提交到Git数据库中。
    - 1.4 . 执行yum命令来安装Git服务程序：
        - 1.4.1 . yum install -y git
        - 1.4.2 . 首次安装Git服务程序后需要设置下用户名称、邮件信息和编辑器，这些信息会随着文件每次都提交到Git数据库中，用于记录提交者的信息，而Git服务程序的配置文档通常会有三份，针对 当前用户 和 指定仓库 的配置文件优先级最高：
                /etc/gitconfig	保存着系统中每个用户及仓库通用配置信息。
                /.gitconfig
                /.config/git/config	针对于当前用户的配置信息。
        - 1.4.3 . 设置用户名:
                           ``````git
                            git config --global user.name "Liu Chuan" 
                           ``````
                 设置密码:git config --global user.email "root@linuxprobe.com"
                 设置vim为默认的文本编辑器：git config --global core.editor vim

                 查看配置的Git工作环境信息：git config --list

- 2 .  提交数据:
    - 2.1 . 创建本地的工作目录 : mkdir linuxprobe
    - 2.2 . 将该目录初始化转成Git的工作目录 ：git init
    - 2.3 . 尝试往里面写入一个新文件 : echo "Initialization Git repository" > readme.txt
    - 2.4 . 将该文件添加到暂存区：git add readme.txt (add文件后,如果再次修改文件,必须 再次进行 add操作)
    - 2.5 . 将暂存区的文件提交到Git版本仓库:git commit -m "add the readme file"
    - 2.6 . 查看当前工作目录的状态:git status
    - 2.7 . 查看当前文件内容与Git版本数据库中的差别：git diff readme.txt
    - 2.8 . 设置要忽略上传的文件(写入到"工作目录/.gitignore"文件中,方法:vim .gitignore):
        忽略所有以.a为后缀的文件
            *.a
        但是lib.a这个文件除外，依然会被提交。
            !lib.a
        忽略build目录内的所有文件。
            build/
        忽略build目录内以txt为后缀的文件。
            build/*.txt
        指定忽略名字为git.c的文件。
            git.c
- 3 . 移除数据
    - 3.1 . 将该文件从Git暂存区域的追踪列表中移除（并不会删除当前工作目录内的数据文件）：
        git rm --cached database
    - 3.2 . 直接删除暂存区内的追踪信息及工作目录内的数据文件 
        git rm -f database
- 4 . 移动数据
    - 4.1 . 修改文件名称 
        git mv readme.txt introduction.txt
- 5 . 历史记录
    - 5.1 . 可以用git log命令来查看提交历史记录;
    - 5.2 . 只想看最近几条记录: git log -2;
    - 5.3 . 显示每次提交的内容差异: git log -p -2
    - 5.4 . 显示数据增改行数: git log --stat -2 
    - 5.4 . 根据不同的格式为我们展示提交的历史信息:
            比如每行显示一条提交记录: git log --pretty=oneline
            以更详细的模式输出最近两次的历史记录：git log --pretty=fuller -2
            可以使用format参数来指定具体的输出格式:git log --pretty=format:"%h %cn"d97dd0b Liu Chuan
               %s  +              | 提交说明                        
               %cd               |  提交日期                        
               %an               |  作者的名字                      
               %cn               |  提交者的姓名                         
               %ce	              |  提交者的电子邮件                    
               %H                |  提交对象的完整SHA-1哈希字串         
               %h                |  提交对象的简短SHA-1哈希字串         
               %T                |  树对象的完整SHA-1哈希字串           
               %t                |  树对象的简短SHA-1哈希字串           
               %P                |  父对象的完整SHA-1哈希字串           
               %p                |  父对象的简短SHA-1哈希字串           
               %ad               |  作者的修订时间                    
- 6 . 还原数据
    - 6.1 . git reset --hard HEAD^:
            还原版本,上一个提交版本会叫HEAD^，上上一个提交版本叫做HEAD^^，HEAD~5往上数第五个提交版本.
    - 6.2 . git reflog:
            查看所有的历史记录,包括未提交的,查出之后,再用 git reset --hard (历史还原点的SHA-1值),还原版本.
    - 6.3 . git checkout -- readme.txt:
            还原文件内容.
- 7 . 管理标签
    - 7.1 . git tag v1.0
            创建标签
    - 7.2 . git tag
            查看所有的已有标签
    - 7.3 . git show v1.0
            查看此标签的详细信息
    - 7.4 . git tag v1.1 -m "version 1.1 released" d316fb
            创建带有说明的标签，用-a指定标签名，-m指定说明文字：
    - 7.5 . git tag -d v1.0
            标签删除
- 8 . 管理分支结构
    - 8.1 . 创建分支:git branch linuxprobe
            切换分支:git checkout linuxprobe
            查看当前分支的情况（会列出该仓库中所有的分支，当前的分支前有＊号）：git branch
    - 8.2 . 合并分支:git merge linuxprobe
            删除分支:git branch -d linuxprobe
- 9 . 内容冲突
    - 9.1 . 创建分支并切换到该分支命令：git checkout -b 分支名称 
    - 9.2 . vim 冲突文件,手动删除冲突部分
    - 9.3 . 查看Git历史提交记录(可以看到分支的变化)：git log --graph --pretty=oneline --abbrev-commit

- 10 . 部署Git服务器
- 11 . Github托管服务
    
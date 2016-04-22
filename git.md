git config --global user.name "jack"
git config --global user.email "jackluo@xxx.com"
Create a new repository
mkdir fromai_cn
cd fromai_cn
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin git@git.xxx.cn:develper/xxx_cn.git
git push -u origin master
Push an existing Git repository
cd existing_git_repo
git remote add origin git@git.xxxx.cn:develper/xxx_cn.git
git push -u origin master

1. ssh-keygen -t rsa -C jackluo@xxxx.com
2. ssh -T git@git.oschina.net

2. git remote -v
3. 新建远程分支(本地必须有分支) git push origin payment:payment
4. 删除远程分支 git branch -r -d origin/payment git push origin :payment

5. http://git-scm.com/downloads
6. git config --global user.name "你的名字" git config --global user.email "你的Email"
7. git clone http://git.oschina.net/xxxxxx/xxxxxx.git
8. git checkout -b $feature_name
9. git commit -am "My feature is ready"
10. git push origin $feature_name

11. git clone --bare  https://github.com/bartaz/impress.js.git
12. cd impress.js.git
    git push --mirror git@git.oschina.net:username/impress-js.git
    
13. git filter-branch --tree-filter 'rm -f path/to/large/files' --tag-name-filter cat -- --all
    git push origin --tags --force
    git push origin --all --force
    
14. 1）创建git配置文件，或者叫库文件
    使用命令：git init
    完成以后，可以在HRString文件夹里面看到一个.git文件，默认是隐藏文件。
    
    2）把当前所有文件加入到本地git库中
    使用命令： git add .
    3）确认加入文件到本地git库
    使用命令：git commit -m '写一些注释'
    4）把本地项目与远程git库关联
    使用命令：git remote add origin git@github.com:henryrao/HRString.git
    5)提交本地库中的文件到远程git库中
    使用命令：git push -u origin master
    git push -f origin master
    
15. 如果希望保留生产服务器上所做的改动,仅仅并入新配置项, 处理方法如下:
    git stash
    git pull
    git stash pop
    然后可以使用git diff -w +文件名 来确认代码自动合并的情况.
    
16. 2.2 添加提交信息
    
       　　如果直接运行 git commit (-a) 则会默认使用 vi 添加描述。也可以使用 git config --global core.editor 命令更改为你喜欢的编辑器。还有一个方法就是使用 -m 选项直接添加提交信息。
    
       $git commit -a -m "commit info"
     
17. git branch -a
17. 或者使用-t参数，它默认会在本地建立一个和远程分支名字一样的分支
    折叠展开复制代码
    
    $ git checkout -t origin/python_mail.skin
    
18. git不再监视指定文件
    git rm --cached test.txt
    add test.txt to .gitignore file
    git commit -m 'i all ignore my some files' -a
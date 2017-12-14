# Git 与 Github 的配合使用



## 如何生成SSH公钥

1. 运行`git bash`，然后输入以下命令，切换到本机的用户目录下面的`.ssh`目录：

```

cd ~/.ssh
```

2. 如果提示`No such file or directory`，则表示之前没有配置过`ssh公钥`；如果没有提示相关错误消息，则表示之前配置过`ssh 公钥`

3. 如果之前没有配置过`ssh 公钥`，则在`~/`目录中执行以下命令：

```

ssh-keygen -t rsa -C "xxxxx@xxxxx.com"
```

其中需要指定一个邮箱，最好是注册github的邮箱地址，执行命令之后，会有三次信息提示，直接输入三次回车即可在`用户根目录`中生成一个`.ssh`文件夹，下面存放着`ssh key`相关文件



## 将生成的ssh key添加到GitHub

1. 登录GitHub，点击右上角头像，点击`settings` -> `SSH and GPG keys` -> `New SSH key`，会显示一个输入`Title`和`Key`的输入框组

2. `Title`中根据需要随意填写即可

3. `Key`中需要把刚生成的`ssh key`内容粘贴进去，可以进入`用户根目录`，找到`.ssh`文件夹，用记事本打开`id_rsa.pub`文件，这个文件中存放的就是刚才生成的`ssh key`；把文件中所有的字符串复制，粘贴到GitHub中保存即可



## 配置Git提交时候的账户

1. 在Git Bash中运行以下两条配置命令，将用户名和Github注册邮箱配置为全局账户：

```

$ git config --global user.name "your_username"  #设置用户名

$ git config --global user.email "your_registered_github_Email"  #设置邮箱地址(建议用注册giuhub的邮箱)
```

2. 运行以下命令，测试`ssh key`是否设置成功：

```

$ ssh -T git@github.com
```

 + 这时候会提示`Are you sure you want to continue connecting (yes/no)?`，意思是`#确认你是否继续连接`，输入`yes`并点击回车；

 + 如果生成ssh key的时候密码不为空，则会看到类似于这样的提示：`Enter passphrase for key '/c/Users/xxxx_000/.ssh/id_rsa':`，意思是`#生成ssh kye是密码为空则无此项，若设置有密码则有此项且`，输入生成ssh key时设置的密码即可；

 + 如果能看到类似于**Hi XXXX! You've successfully authenticated, but GitHub does not provide shell access.**这样的提示，则表示`ssh key`配置成功！



## 将本地项目通过SSH push到GitHub

1. 在Github中创建一个新仓储

2. 复制新仓储的ssh地址

3. 创建本地项目，并在根目录中运行`git init`初始化

4. 在项目根目录中使用`touch ***`创建`README.md`和`.gitignore`文件

5. 运行`git add .`

6. 运行`git commit -m "init git files"`

7. 运行`git remote add origin "粘贴复制test ssh key的ssh路径"`

8. ```
   例如 git remote add origin git@github.com:butterflyflyaway123/js-.git
   ```

9. 运行`git push -u origin master`

   报错

   添加远程github仓库的时候提示错误：fatal: remote origin already exists. 

   (1)、先删除远程 Git 仓库

   > $ git remote rm origin

   (2)、再添加远程 Git 仓库

   > $ git remote add origin git@github.com:FBing/java-code-generator

   (3)如果执行 git remote rm origin 报错的话，我们可以手动修改gitconfig文件的内容

   > $ vi .git/config
   >
   > 把 [remote “origin”] 那一行删掉就好了。



## 在Github中直接创建新仓储并clone到本地

1. 在Github上创建有`LICENSE`和`README.md`的文件

2. 使用`git clone ssh仓储地址`直接将项目克隆到本地
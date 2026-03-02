# Git : 常用远程指令大全
	```bash
	//创建版本库
	git init                                                  # 初始化本地git仓库（创建新仓库）
	git clone <仓库URL>											# clone远程仓库

	//修改和提交
	git add .                                                 # 跟踪所有改动的文件
	git commit -m "commit message"                            # 跟踪所有改动的文件

	//远程操作
	git remote -v                                             # 查看远程版本库信息
	git remote add <远程仓库别名> <仓库URL>                   # 添加远程仓库
	git remote set-url <远程仓库别名> <新URL>                 # 修改远程仓库 URL
	git pull                                                  # 拉取远程 main 的更新（前提是已设置上游）
	git push                                                  # 推送本地 main 的提交

	//配置
	git config --list                                         # 获取默认配置
	git config --global user.name "xxx"                       # 配置用户名
	git config --global user.email "xxx@xxx.com"              # 配置邮件
	```        
# Git : SSH 协议

- 使用 SSH 协议可以与远程仓库（如 GitHub、GitLab、Gitee 等）进行安全的免密通信<br>
- 客户端拥有两个文件：公钥和私钥。公钥放入远程仓库，像一把锁，每次进行仓库操作时，仓库会对比公钥，一致才允许操作<br>
- 优势：优势：免密操作——配置一次后，推送和拉取代码无需重复输入用户名和密码，且通信内容加密<br>

## 配置步骤
1. 检查是否已有 SSH 密钥
打开终端，执行以下命令查看 C:/Users/ <__你的电脑用户名__> /.ssh 目录下是否存在密钥文件：  

	```bash  
	ls -al ~/.ssh
	```  
2. 生成新的 SSH 密钥（如果没有）
使用以下命令生成新的 SSH 密钥对（推荐使用 ED25519 算法，更安全且高效）： 

	```bash  
	ssh-keygen -t ed25519 -C "your_email@example.com"
	```  
&emsp;&emsp;按提示设置密钥保存路径（默认 ~/.ssh/id_ed25519）和密码短语（可留空，一直按Enter键）。在C:/Users/ <__你的电脑用户名__> /.ssh 目录下会生成以下两个文件：<br>
&emsp;&emsp;- 私钥：id_ed25519（自己保存，切勿泄露）<br>
&emsp;&emsp;- ==公钥：id_ed25519.pub（需添加到 Git 服务器）==

3. 将公钥添加到 Git 服务器
以 GitHub 为例（其他平台操作类似）：
以记事本打开公钥文件全选并复制。
登录 ==GitHub → 点击头像 → Settings → SSH and GPG keys → New SSH key==，粘贴公钥，填写标题，保存。

4. 测试 SSH 连接
执行以下命令验证是否配置成功：
	```bash  
	ssh -T git@github.com
	```  
&emsp;&emsp;若看到类似 Hi username! You've successfully authenticated... 的提示，说明连接正常。

5. 使用 SSH 协议操作 Git 仓库

	```bash  
	# 查看当前远程 URL
	git remote -v

	# 修改为 SSH 地址
	git remote set-url origin git@github.com:user/repo.git

	# 也可以使用ssh协议Clone
	git clone git@github.com:user/repo.git
	```  

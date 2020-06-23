## GIT
-基本

	- git status
	- git add.
	- git commit -m "完成了登录功能"  
	- git brangch
	- git push -u origin 分支名字  在github创建分支并上传
	- git checkout master 切换主分支
	- git merge 分支   合并到主分支
	- git push 上传
	
- 创建分支git checkout -b login
- git branch  查看分支
- git status  查看状态
- 



创建新分支
- git branch
- git checkout -b 新分支名字
- git push -u origin 新分支名字

- git add.
- git commit -m "开发描述" 
- git push
- git checkout master 
- git merge 分支名字
- git push


## 项目优化

	- babel-plugin-transform-remove-console 去除console
	- 解决ESlint语法命令 只在 bulid 发布阶段移除所有的console(babel.config.js)
	- 生成打包报告
	- 配置webpack生成两个入口，修改默认打包入口（需配置vue.config.js）
	- 通过externals加载外部CDN资源
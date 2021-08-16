<!--
 * @Author: tangdaoyong
 * @Date: 2021-08-16 17:49:02
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-08-16 17:55:25
 * @Description: ESLint
-->
# ESLint

## git commit 提交时，只检测暂存区的文件

[ssh脚本实现](https://www.jianshu.com/p/de90ffbd53e9)
[目前的工具实现](https://blog.csdn.net/mrhaoxiaojun/article/details/109637369)
[git hooks](https://blog.csdn.net/qq624202120/article/details/107443295)

### git hook 介绍

想到了hooks，每次git commit的时，git会主动调用 .git/hooks/pre-commit 这个脚本(默认的*.sample不执行)，脚本可以是shell、python、ruby等可执行脚本，只要是 以非零状态 退出会导致中止，就commit失败。

类型	触发命令(相同命令按顺序执行)	钩子	用途
客户端	git commit	pre-commit	提交之前运行，用于检查代码等，非零可以中止过程。加--no-verify可跳过
客户端	git commit	prepare-commit-msg	提交信息编辑器之前，信息被创建之后运行。可以动态插入信息。
客户端	git commit	commit-msg	接受一个消息参数，可以自动生成提交的消息模版。
客户端	git commit	post-commit	完成后运行，一般用于通知之类的事情。
客户端	git rebase	pre-rebase	运行git rebase之前，默认的pre-rebase是用来禁止已经推送的提交进行git rebase。
客户端	git checkout	post-checkout	运行完成后调用，用于放入大的二进制文件、自动生成文档等。
客户端	git merge	pre-push	验证git控制之外的文件是否存在，可以复制进工作区。
客户端	git gc --auto	pre-auto-gc	根据业务是否要中断回收。
客户端	替换提交记录的命令触发(git commit --amend、git rebase等)	post-rewrite	从标准输入中接受重写提交记录。
邮件工作流	git am	applypatch-msg	确保提交信息符合格式。
邮件工作流	git am	post-applypatch	提交产生后，用于通知，但无法停止打补丁。
服务器端	收到客户端的push后	pre-receive	可以用来阻止非快进(non-fast-forward)的更新。
服务器端	收到客户端的receive后	update	类似pre-receive，不同于会在每个准备更新的分支各运行一次。
服务器端	收到客户端的receive后	post-receive	完成运行后，用来通知管理员、CI等。
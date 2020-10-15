# 问题记录

## Github 提交没有小绿框的显示

```
#使用查看log的命令发现有些提交的日志中没有指明作者的邮箱地址
git log

# 使用以下命令对作者的邮箱进行配置
#如果只想修改这一个仓库的邮箱：
git config user.email "your_email@example.com"

#可以使用如下命令确认修改是否成功：
git config user.email

#就会显示你目前的邮箱。

#如果想对所有的仓库生效，避免在别的仓库继续出现这个情况，则输入：
#git config --global user.email "your_email@example.com"

#同样可以查看确认一下：
git config --global user.email

```

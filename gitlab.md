# 1.安装依赖
```shell
yum install -y curl openssh-server openssh-clients postfix cronie git
```
# 2.启动postfix
```shell
service postfix start
chkconfig postfix on
```
# 3.安装gitlab
```shell
yum -y localinstall gitlab-ce-8.8.8-ce.0.el6.x86_64.rpm
```
# 4.配置(/etc/gitlab/gitlab.rb)
```conf
#配置gitlab的ip或域名
external_url 'http://10.0.10.55'
###配置邮箱###################################
gitlab_rails['time_zone'] = 'Asia/Shanghai'
gitlab_rails['gitlab_email_enabled'] = true
gitlab_rails['gitlab_email_from'] = 'test@test.com'
gitlab_rails['gitlab_email_reply_to'] = 'test@test.com'
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = 'smtp.test.com'
gitlab_rails['smtp_port'] = 465
gitlab_rails['smtp_user_name'] = 'test@test.com'
gitlab_rails['smtp_password'] = 'password'
gitlab_rails['smtp_domain'] = 'test.com'
gitlab_rails['smtp_authentication'] = 'login'
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = true
user['git_user_email'] = 'test@test.com'
###################################################################
#配置gitlab备份路径
gitlab_rails['backup_path'] = "/data/git-backup"
#配置数据存储路径
git_data_dir "/data/git-data"	
#配置ssh端口
gitlab_rails['gitlab_shell_ssh_port'] = 8242
#配置数据库存储路径
postgresql['data_dir'] = "/data/postgresql"
```
# 5.配置生效
```shell
gitlab-ctl reconfigure
```
# 6.汉化
```shell
cd /opt/gitlab/embedded/service/gitlab-rails
gitlab-ctl stop
git apply ~/8.8.diff
```

# 7.登录修改密码

![iamge](img/01.png)

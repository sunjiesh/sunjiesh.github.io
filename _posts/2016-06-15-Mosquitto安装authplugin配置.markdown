---
layout: post
title:  "Mosquitto安装authplugin配置"
date:   2016-06-15 21:00:00 +0800
categories: Linux
---

集成authplugin的mosquitto配置，根据不同监听端口来进行不同的安全验证
1、仅证书
2、证书+用户名密码（该证书中的用户名可与实际的用户名不同，mosquitto以-u参数的用户名为准）。

<pre>
autosave_interval 1800
persistence true
persistence_file mosquitto.db
persistence_location /tmp/
connection_messages true
log_timestamp true
log_dest stderr

#log_type error
#log_type warning
#log_type notice
#log_type information
#log_type all
log_type debug

listener 1883
cafile /etc/mosquitto/ca_certificates/mqtt_chain_ca.crt
certfile /etc/mosquitto/certs/mosquitto_server.crt
keyfile /etc/mosquitto/certs/mosquitto_server_nopwd.key
require_certificate true
use_identity_as_username true
allow_anonymous false
acl_file /etc/mosquitto/mosquitto_aclfile


listener 1884
#
#   __  __       ____   ___  _     
#  |  \/  |_   _/ ___| / _ \| |    
#  | |\/| | | | \___ \| | | | |    
#  | |  | | |_| |___) | |_| | |___ 
#  |_|  |_|\__, |____/ \__\_\_____|
#          |___/                   
#  
#                     

auth_plugin /etc/mosquitto/auth-plug.so
auth_opt_backends mysql
auth_opt_cdbname pwdb.cdb
auth_opt_host localhost
auth_opt_port 3306
auth_opt_dbname test
auth_opt_user root
auth_opt_pass password
auth_opt_userquery SELECT pw FROM users WHERE username = '%s'
auth_opt_superquery SELECT IFNULL(COUNT(*), 0) FROM users WHERE username = '%s' AND super = 1
#auth_opt_aclquery SELECT topic FROM acls WHERE username = '%s'   
auth_opt_aclquery SELECT topic FROM acls WHERE (username = '%s') AND (rw >= %d)

# Usernames with this fnmatch(3) (a.k.a glob(3))  pattern are exempt from the
# module's ACL checking
auth_opt_superusers S*


cafile /etc/mosquitto/ca_certificates/mqtt_chain_ca.crt
certfile /etc/mosquitto/certs/mosquitto_server.crt
keyfile /etc/mosquitto/certs/mosquitto_server_nopwd.key
require_certificate true
use_identity_as_username false
allow_anonymous false

</pre>
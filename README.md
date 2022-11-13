# ldap
基于centos系统openldap镜像，默认密码test123123 ，欢迎访问https://aqzt.com

使用方法，启动命令(获取更多技术资料，欢迎访问https://aqzt.com/)
```
docker pull opcache/ldap:v2.6.3
docker run -d  --net=host --name  ldaptest    opcache/ldap:v2.6.3
```
创建1个管理员账号
```
vim test.ldif
dn: dc=sys,dc=com
objectclass: dcObject
objectclass: organization
o: SYS.Inc
dc: sys

dn: cn=admin,dc=sys,dc=com
objectclass: organizationalRole
cn: admin
```
插入数据库
```
ldapadd -x -D "cn=admin,dc=sys,dc=com" -W -f test.ldif
Enter LDAP Password   test123123
```
验证
```
ldapsearch -x -b 'dc=sys,dc=com' '(objectClass=*)'
```
创建1个具有部门属性的员工
```
 vim test2.ldif 

dn: ou=it,dc=sys,dc=com
ou: it
objectClass: organizationalUnit

dn: cn=test1,ou=it,dc=sys,dc=com
ou: it
cn: test1
sn: t1
objectClass: inetOrgPerson
objectClass: organizationalPerson
```
插入数据库
```
ldapadd -x -D "cn=admin,dc=sys,dc=com" -W -f test2.ldif
```
验证
```
ldapsearch -x -b 'dc=sys,dc=com' '(objectClass=*)'
```

##iam scene-imaicloud 使用说明

###1. 租户注册

使用iam的注册页面，注册时用户需要提供邮箱和设置密码，注册成功后会得到一个租户key，请保存好这个key，以便在登录时使用。

###2. 生成apiKeys

**通过控制台**

登录后，在头像菜单中，点击“生成apiKeys”，将得到一个包含apiKey id和secret的文件。

**通过api**

Create An apiKeys

POST /api/v1/account/$ACCOUNT_ID/apiKeys

$ACCOUNT_ID为账号内码，可以在登录后从头像菜单中查看。

```
curl -H 'Content-Type: application/json' \
-u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
-X POST https://dev.imaicloud.com/iam/api/v1/accounts/sqHezdzpS_e_bPbmjV6zYw/apiKeys \
-d "{}"
```

``
 说明* 
``

REST API的认证使用Authorization请求头，值为apiKey的id和secret的base64编码（ base64($ID:$SECRET) ）。

使用linux curl测试，可设置变量$IAM_APIKEY_ID、$IAM_APIKEY_SECRET，值分别apiKeys的id和secret。


###3. Retrieve A Tenant

GET /api/v1/tenants/current

```
curl -u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
https://dev.imaicloud.com/iam/api/v1/tenants/current
```

###4. 查询租户下的目录

GET /api/v1/tenants/$TENANT_ID/directories

###5. 创建目录

POST /api/v1/directories

```
curl -H 'Content-Type: application/json' \
-u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
-X POST https://dev.imaicloud.com/iam/api/v1/directories \
-d '{"description": "customer directory", "type": "cloud", "status": "enabled", "name": "customer"}'
```

###6. 查询目录下的账号

GET /api/v1/directories/$DIRECTORY_ID/accounts

```
curl -u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
https://dev.imaicloud.com/iam/api/v1/directories/AsSYqRLrTrWsrbJiSIzqmA/accounts
```

###7. 在目录下创建账号

POST api/v1/directories/$DIRECTORY_ID/accounts

```
curl -H 'Content-Type: application/json' \
-u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
-X POST https://dev.imaicloud.com/iam/api/v1/directories/AsSYqRLrTrWsrbJiSIzqmA/accounts \
-d '{ \
"email": "demo@qq.com", \
"password": "$apr1$1Nc6ANA.$UjRKo27AQzrsWf7aEi5811", \
"status": "enabled", \
"username": "demo" \
}'
```


###8. 查询目录下的组

GET /api/v1/directories/$DIRECTORY_ID/groups

```
curl -u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
https://dev.imaicloud.com/iam/api/v1/directories/AsSYqRLrTrWsrbJiSIzqmA/groups
```

###9. 在目录下创建组

```
curl -H 'Content-Type: application/json' \
-u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
-X POST https://dev.imaicloud.com/iam/api/v1/directories/AsSYqRLrTrWsrbJiSIzqmA/groups \
-d '{"name": "demo group"}'
```

###10. 组成员

账号和组通过组成员连接。

**创建组成员**

POST /api/v1/groupMemberships

```
curl -H 'Content-Type: application/json' \
-u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
-X POST https://dev.imaicloud.com/iam/api/v1/groupMemberships \
-d "{\"account\": \"HVVhTp-uTQSdrLKRN2-y8A\", \"group\":\"M39wjYP-ToOkpkrULL2LZg\"}"
```

**查询账号所在的组**

GET /api/v1/accounts/$ACCOUNT_ID/groups

```
curl -u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
https://dev.imaicloud.com/iam/api/v1/accounts/HVVhTp-uTQSdrLKRN2-y8A/groups
```

###11. 定制数据

GET /v1/$RESOURCE_TYPE/$RESOURCE_ID/customData

POST /v1/$RESOURCE_TYPE/$RESOURCE_ID/customData

**访问Account的customData**

GET /api/v1/accounts/$ACCOUNT_ID/customData

```
curl -u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
https://dev.imaicloud.com/iam/api/v1/accounts/KySQo1c7TTKoFzniA3VLbA/customData
```

**设置定制数据**

POST /api/v1/accounts/$ACCOUNT_ID/customData

```
curl -H 'Content-Type: application/json' \
-u $IAM_APIKEY_ID:$IAM_APIKEY_SECRET \
-X POST https://dev.imaicloud.com/iam/api/v1/accounts/06xbdFbrSYug82YrA7hroQ/customData \
-d '{"domain": "demo.imaicloud.com"}'
```






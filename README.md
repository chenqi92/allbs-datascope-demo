# 系统权限
## 说明

- 功能权限（就是常用的RBAC那一套，登录->控制到按钮级别的权限系统）
- 数据权限 (根据不用用户，如一个园区分为多家企业，每家企业看到的数据内容不同，园区内不同领导分管不同的多家企业)

## 程序运行说明

application-dev中需要修改redis和mysql的连接配置。可以修改本地环境变量也可以直接在修改yml中环境变量后面的内容。
![](https://nas.allbs.cn:9006/cloudpic/2023/07/e38f9d3411a2fe2ed534fb13a11900ad.png)

## 数据权限使用说明
以数据权限为例，功能权限就不单独说明了，可以看 https://www.allbs.cn/posts/36543/

## 运行程序开始测试
使用本项目中的文件generated-requests.http

### 登陆并复制token
![](https://nas.allbs.cn:9006/cloudpic/2023/07/99a48bd5c41b9c222df26ea72a94a1ef.png)
![](https://nas.allbs.cn:9006/cloudpic/2023/07/0b1180762f2aae34aa4a216eb2444206.png)

### 使用token测试权限过滤功能
将旧token替换为新生成的token
![](https://nas.allbs.cn:9006/cloudpic/2023/07/56d7ad4e8755bd9efabad1e71ed57f7b.png)

### 在需要进行过滤的类或方法上添加注解`@DataScope`，这个注解可以指定需要过滤字段的名称，指定忽略的表名等
![](https://nas.allbs.cn:9006/cloudpic/2023/07/9cf784220634fd35971b2a6ae1f6ba38.png)
或者
![](https://nas.allbs.cn:9006/cloudpic/2023/07/40221626702f67219d6b6c9e239bc835.png)
使用效果，会自动将该用户所具备的ent_id拼进筛选条件中
![](https://nas.allbs.cn:9006/cloudpic/2023/07/31830875bee1e3f6f4cab8b95e3e8455.png)
插入的方法，如果不在当前用户的权限范围内会直接报错
![](https://nas.allbs.cn:9006/cloudpic/2023/07/817a2f29787b051bf026c4c18d2cc9d1.png)
更新的方法，也会自动将过滤条件拼进去，使更新不会生效
![](https://nas.allbs.cn:9006/cloudpic/2023/07/9cded398161803bdacdd3d1f5a98fedd.png)

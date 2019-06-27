# API设计
### 微信小程序使用云开发设计
<a href="https://developers.weixin.qq.com/miniprogram/dev/api/"> 微信小程序官方API文档</a><br>
<a href="https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/"> 小程序端 API 文档</a><br>

云开发为开发者提供完整的原生云端支持和微信服务支持，弱化后端和运维概念，无需搭建服务器，使用平台提供的 API 进行核心业务开发，即可实现快速上线和迭代，同时这一能力，同开发者已经使用的云服务相互兼容，并不互斥。
### 在小程序端可调用 Collection.get  获取集合数据
```
db.collection('users').where({
        _openid: app.globalData.userInfo.openid
      }).get().then(res => {
        this.setData({
          'detail.type': res.data[0].type,
          'detail.sid': res.data[0].sid,
          'detail.name': res.data[0].name,
          'detail.age': res.data[0].age,
          'detail.gender': res.data[0].gender,
          'detail.grade': res.data[0].grade,
          'detail.pro': res.data[0].pro
        })
      })
```

### 可以用Collection.add在集合上新增记录
```
// 新用户，添加到数据库
      if (res.total == 0) {
        if (this.data.userType == 'student') {
          db.collection('users').add({
            // data 字段表示需新增的 JSON 数据
            data: {
              // _id: 'todo-identifiant-aleatoire', // 可选自定义 _id，在此处场景下用数据库自动分配的就可以了
              avatarUrl: e.detail.userInfo.avatarUrl,
              nickName: e.detail.userInfo.nickName,
              wallet: new Number(0),
              type: this.data.userType,
              sid: '',
              name: '',
              age: '',
              gender: '',
              grade: '',
              pro: ''
            }
```

### 可以通过 Document.update 更新一条记录
```
db.collection('users').doc(app.globalData.userInfo.id).update({
        // data 传入需要局部更新的数据
        data: {
          sid: e.detail.value.sid,
          name: e.detail.value.name,
          age: e.detail.value.age,
          gender: e.detail.value.gender,
          grade: e.detail.value.grade,
          pro: e.detail.value.pro
        }
      })
})
```
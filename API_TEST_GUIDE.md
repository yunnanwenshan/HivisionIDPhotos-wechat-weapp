# 🧪 API接口测试指南

## 📋 项目信息
- **服务地址**: `http://localhost:8010`
- **认证方式**: Sa-Token (需要在请求头中携带token)
- **响应格式**: JSON

## 🔐 认证说明
大部分接口都需要用户登录后才能访问，需要先获取token后才能调用其他接口。

---

## 📱 1. 用户相关接口 (`/user`)

### 1.1 用户登录 (无需认证)
```bash
# 使用curl测试
curl -X GET "http://localhost:8010/user/login?code=test_code"

# 使用Postman/Apifox
GET http://localhost:8010/user/login?code=test_code
```

### 1.2 获取用户信息 (需要认证)
```bash
# 使用curl测试 (需要替换YOUR_TOKEN)
curl -X GET "http://localhost:8010/user/userInfo" \
  -H "token: YOUR_TOKEN"

# 使用Postman/Apifox
GET http://localhost:8010/user/userInfo
Headers: token: YOUR_TOKEN
```

### 1.3 更新用户信息 (需要认证)
```bash
# 使用curl测试
curl -X POST "http://localhost:8010/user/updateUserInfo" \
  -H "token: YOUR_TOKEN" \
  -F "nickname=测试用户"

# 使用Postman/Apifox
POST http://localhost:8010/user/updateUserInfo
Headers: token: YOUR_TOKEN
Body (form-data):
- nickname: 测试用户
- file: [选择文件]
```

---

## 🎨 2. 核心API接口 (`/api`)

### 2.1 获取视频单元 (可能无需认证)
```bash
# 使用curl测试
curl -X POST "http://localhost:8010/api/getvideoUnit"

# 使用Postman/Apifox
POST http://localhost:8010/api/getvideoUnit
```

### 2.2 创建证件照 (需要认证)
```bash
# 使用curl测试
curl -X POST "http://localhost:8010/api/createIdPhoto" \
  -H "Content-Type: application/json" \
  -H "token: YOUR_TOKEN" \
  -d '{
    "image": "base64_image_data",
    "size": "一寸",
    "color": "白色"
  }'

# 使用Postman/Apifox
POST http://localhost:8010/api/createIdPhoto
Headers: 
- Content-Type: application/json
- token: YOUR_TOKEN
Body (JSON):
{
  "image": "base64_image_data",
  "size": "一寸", 
  "color": "白色"
}
```

### 2.3 获取网站配置
```bash
# 使用curl测试
curl -X POST "http://localhost:8010/api/getWebGlow"

# 使用Postman/Apifox
POST http://localhost:8010/api/getWebGlow
```

---

## 🚀 3. 其他功能接口 (`/otherApi`)

### 3.1 查看探索统计 (需要认证)
```bash
# 使用curl测试
curl -X GET "http://localhost:8010/otherApi/exploreCount" \
  -H "token: YOUR_TOKEN"

# 使用Postman/Apifox  
GET http://localhost:8010/otherApi/exploreCount
Headers: token: YOUR_TOKEN
```

### 3.2 检查免费配额 (需要认证)
```bash
# 使用curl测试
curl -X GET "http://localhost:8010/otherApi/checkTheFreeQuota?type=1&type2=1" \
  -H "token: YOUR_TOKEN"

# 使用Postman/Apifox
GET http://localhost:8010/otherApi/checkTheFreeQuota?type=1&type2=1
Headers: token: YOUR_TOKEN
```

### 3.3 图片上色 (需要认证)
```bash
# 使用curl测试
curl -X POST "http://localhost:8010/otherApi/colourize" \
  -H "Content-Type: application/json" \
  -H "token: YOUR_TOKEN" \
  -d '{
    "image": "base64_image_data"
  }'

# 使用Postman/Apifox
POST http://localhost:8010/otherApi/colourize
Headers:
- Content-Type: application/json
- token: YOUR_TOKEN
Body (JSON):
{
  "image": "base64_image_data"
}
```

### 3.4 智能抠图 (需要认证)
```bash
# 使用curl测试
curl -X POST "http://localhost:8010/otherApi/matting" \
  -H "Content-Type: application/json" \
  -H "token: YOUR_TOKEN" \
  -d '{
    "image": "base64_image_data"
  }'
```

---

## 🛠️ 测试工具推荐

### 1. **Postman** (推荐)
- 下载: https://www.postman.com/
- 支持保存请求、环境变量、集合等
- 界面友好，功能强大

### 2. **Apifox** (国产，推荐)
- 下载: https://www.apifox.cn/
- 集成了接口文档、调试、Mock等功能
- 中文界面，使用简单

### 3. **curl命令行**
- 系统自带，无需安装
- 适合快速测试和脚本化

### 4. **VS Code插件**
- REST Client插件
- Thunder Client插件

---

## 🔍 快速测试步骤

### 第一步：测试基础连接
```bash
# 测试服务是否正常运行
curl -X POST "http://localhost:8010/api/getvideoUnit"
```

### 第二步：测试无需认证的接口
```bash
# 测试登录接口 (注意：这可能需要有效的微信code)
curl -X GET "http://localhost:8010/user/login?code=test"
```

### 第三步：如果有token，测试需要认证的接口
```bash
# 替换YOUR_TOKEN为实际token
curl -X GET "http://localhost:8010/user/userInfo" \
  -H "token: YOUR_TOKEN"
```

---

## ⚠️ 注意事项

1. **Token获取**: 大部分接口需要先通过登录获取token
2. **微信登录**: 登录接口可能需要真实的微信小程序授权code
3. **图片数据**: 涉及图片的接口需要base64编码的图片数据
4. **Content-Type**: POST请求注意设置正确的Content-Type
5. **错误处理**: 注意查看返回的错误信息和状态码

---

## 📄 响应格式示例

### 成功响应
```json
{
  "status": 200,
  "msg": "success",
  "data": {
    // 具体数据
  }
}
```

### 失败响应
```json
{
  "status": 500,
  "msg": "错误信息",
  "data": null
}
```

---

## 🎯 开始测试！

1. 确保项目正在运行 (http://localhost:8010)
2. 选择合适的测试工具
3. 从无需认证的接口开始测试
4. 逐步测试其他功能接口

Happy Testing! 🚀
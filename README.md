# OpenCode Proxy for Appwrite Cloud Go Runtime

这是专为 **Appwrite Cloud Functions (Go 运行时)** 定制开发的高性能 AI 智能反向代理网关。完全继承了 V4 版本的完整特性，包括：

1. **原汁原味的原生多模态图像识别**（完美兼容 OpenAI Vision 协议，已解决 JSON 长度截断 Bug）
2. **纯净与防护双模型挂载**：
   - `mimo-v2.5`：纯净版，不包含任何额外系统提示词，百分百原生智能。
   - `mimo-v2.5-pro`：人设防护版，自动注入小米大模型人设并进行返回流实时脱敏清洗。
3. **零鉴权泄露安全隔离**：统一通过 `Bearer sk-mimo` / `x-api-key: sk-mimo` 对内提供服务。

---

## ⚡️ 一键部署到 Appwrite Cloud 指引

### 1. 连接仓库与创建函数
1. 登录 [Appwrite Console](https://cloud.appwrite.io/)，进入对应项目 -> 点击左侧导航栏 **Functions**。
2. 点击 **Create function**，选择 **Connected Account (GitHub)**，选中您的 `opencode-appwrite` 仓库。
3. 在部署设置中：
   - **Runtime**: 选择 `Go (1.23)` 或 `Go (1.22)`
   - **Entrypoint**: `main.go`

### 2. 参数与安全配置 (关键!)
进入刚才生成的 Function，点击 **Settings (设置)** 选项卡：
1. **Timeout (超时时间)**：请将该值调整为 **`60` 秒**（默认值较短，大图多模态识别容易超时断开）。
2. **Execute Access (执行权限)**：务必勾选 **`any`**（允许公开 HTTP 请求访问）。
3. **环境变量**（可选）：默认已全部内置在编译中，不需要填写。

配置完毕后，点击顶部的 **Redeploy** (或等待 Git 自动部署通过)。

---

## 🚀 接入使用

在 Appwrite Function 的 Overview 页面可以看到系统分配的 **Domain**，类似：
`https://65a123456789.appwrite.global/`

将其拼接作为各个 AI 客户端的 **Base URL** 即可使用：
- **完整接口地址**: `https://65a123456789.appwrite.global/v1/chat/completions`
- **可用模型名**: `mimo-v2.5` (纯净版) / `mimo-v2.5-pro` (防泄漏版) / `deepseek-v4-flash`
- **API Key**: `sk-mimo`

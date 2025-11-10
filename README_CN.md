# DeepSeek 聊天对话 

这是一个基于 Next.js 的示例项目，演示如何搭建一个以 DeepSeek 为基础的聊天对话应用。

下面的文档包含如何本地运行、配置常用环境变量、项目结构说明以及部署与贡献指南（中文）。

## 快速开始

先安装依赖并启动开发服务器：

```bash
npm install
npm run dev
# 或者
yarn
yarn dev
# 或者 pnpm
pnpm install
pnpm dev
```

打开浏览器并访问 http://localhost:3000 即可查看页面。

页面入口：`app/page.tsx`，修改该文件后页面会自动热重载。

### 环境变量
在项目根目录创建一个 `.env.local` 文件（不要把它提交到版本库），常见变量示例：

```env
# OpenAI API Key（示例名称，根据项目实现可能不同）
OPENAI_API_KEY=your_openai_api_key_here

# 可选：自定义后端配置或数据库连接字符串
# DATABASE_URL=...
```

注意：把密钥保存在环境变量中，避免在客户端代码中泄露敏感信息。

## 功能与实现要点

- 使用 Next.js App Router（`app/`）组织页面与 API 路由。
- 后端 API 路由位于 `app/api/`（例如 `app/api/chat/route.ts` 等），用于处理对话请求与消息持久化。
- 数据库相关代码位于 `db/`（例如 `db/index.ts`, `db/schema.ts`）。

如果要切换或使用高阶模型（例如组织内开通的 gpt-5-mini），请在后端调用处将模型名替换为 OpenAI 指定的模型标识，并确保你的账号/组织已被授权。

示例调用（服务端）：

```javascript
// 伪代码：在服务端调用 OpenAI Chat Completion
const res = await fetch('https://api.openai.com/v1/chat/completions', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${process.env.OPENAI_API_KEY}`,
  },
  body: JSON.stringify({
    model: 'gpt-4o-mini', // 或 'gpt-5-mini'（需组织已开通）
    messages,
    max_tokens: 800,
  }),
});
```

## 项目结构（部分）

- `app/` - Next.js App Router 源码（页面、API 路由、布局等）
  - `app/api/` - 后端路由（聊天、创建会话、获取消息等）
  - `app/chat/[chat_id]/` - 聊天页面
- `src/components/` - 可复用的 UI 组件（例如导航栏、QueryClientProvider）
- `db/` - 数据库与模式定义

## 学习资料

- Next.js 官网文档（中文/英文）：https://nextjs.org/docs
- Next.js 教程：https://nextjs.org/learn

## 部署

推荐使用 Vercel 一键部署（Next.js 官方托管平台）：

1. 在 Vercel 控制台中创建新项目并连接你的代码仓库。
2. 在 Vercel 项目设置中添加必要的环境变量（例如 `OPENAI_API_KEY`）。
3. 部署后，Vercel 会自动构建并上线你的应用。

也可以使用其他平台（Netlify、自托管服务器、Docker 等），只需在部署环境中设置相应环境变量并构建 Next.js 项目。

## 测试与本地检查

- 本仓库使用 TypeScript（如果启用了），请在本地运行类型检查与 lint：

```bash
npm run build   # 进行一次完整构建以发现编译或类型错误
npm run lint
```

（根据项目 package.json 中的 scripts 适当调整命令）

## 贡献

欢迎提交 issue 或 PR：

1. Fork 仓库并新建分支。
2. 提交改变并发起 PR，描述你修改的目的与复现步骤。

## 联系与许可

如需进一步帮助或有商业部署/模型接入需求，请在仓库中创建 issue 或通过项目维护人联系方式联系。

本项目遵循原仓库的许可（如果存在 LICENSE 文件，请参考）。

---

感谢使用本项目！希望它能帮助你快速搭建 DeepSeek 驱动的聊天体验。

# OpenAI API 代理服务

> **声明：** 本项目是对原有项目的修复版本，非原创项目。感谢原作者的开源贡献。

这是一个基于 Vercel Edge Functions 和 Cloudflare Workers 的 OpenAI API 代理服务，可以帮助你解决 OpenAI API 访问限制的问题。

## 主要特性

- 支持所有 OpenAI API 端点
- 自动处理 CORS
- 支持双平台部署（Vercel/Cloudflare）
- 使用 Edge Functions，延迟更低
- TypeScript 支持
- 保持请求头和响应头的一致性

## 部署指南

### Vercel 部署

1. Fork 这个仓库
2. 在 Vercel 控制台中导入你的 Fork 仓库
3. 直接部署，无需其他配置

> 注意：如果你在香港地区，建议使用 Vercel 部署，因为 Cloudflare 在香港的节点不被 OpenAI API 支持。

### Cloudflare 部署

1. 克隆仓库到本地
```bash
git clone <your-fork-url>
cd openai-proxy
```

2. 安装依赖并部署
```bash
pnpm install
pnpm run deploy-cloudflare
```

## 使用方法

部署完成后，你只需要将原本请求 OpenAI API 的地址 `https://api.openai.com` 替换为你的部署域名即可。

示例：
```javascript
const response = await fetch('https://your-deployment-url/v1/chat/completions', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_API_KEY'
  },
  body: JSON.stringify({
    model: 'gpt-3.5-turbo',
    messages: [{ role: 'user', content: 'Hello!' }]
  })
});
```

## 开发

### 本地开发

1. Vercel 开发环境：
```bash
pnpm install
pnpm run dev-next
```

2. Cloudflare 开发环境：
```bash
pnpm install
pnpm run dev-cloudflare
```

## 项目结构

```
├── pages/api/         # Vercel Edge Function
│   └── proxy.ts       # 代理处理程序
├── src/
│   ├── index.ts       # Cloudflare Worker 入口
│   └── handle-request.ts  # 核心请求处理逻辑
```

## 注意事项

- 确保你的 OpenAI API Key 有足够的额度
- 代理服务器仅转发请求，不会存储你的 API Key
- 建议在生产环境中设置适当的访问控制

## License

MIT

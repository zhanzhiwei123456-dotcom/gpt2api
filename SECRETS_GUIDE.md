# GPT2API Secrets 配置指南

## ⚠️ 重要说明

GitHub Secrets **必须在 GitHub 网页端手动配置**，无法通过 API 自动设置。

---

## 需要配置的 Secrets

### 1. JWT_SECRET
JWT 签名密钥，至少 32 字符。

**生成命令：**
```bash
openssl rand -base64 48 | tr -d '=/+' | cut -c1-48
```

### 2. CRYPTO_AES_KEY
AES-256 加密 KEY，必须 64 位 hex（32 字节）。

**生成命令：**
```bash
openssl rand -hex 32
```

### 3. DOCKER_REGISTRY (可选)
如果你使用私有 Docker Registry，需要配置登录信息。

---

## 配置步骤

1. 打开你的 Fork 仓库：https://github.com/zhanzhiwei123456-dotcom/gpt2api

2. 点击 **Settings** → **Secrets and variables** → **Actions**

3. 点击 **New repository secret** 按钮

4. 依次添加：
   - **Name**: `JWT_SECRET`
   - **Secret**: （粘贴生成的随机字符串）

5. 重复步骤 3-4，添加 `CRYPTO_AES_KEY`

---

## 自动设置脚本

你可以使用以下 PowerShell 脚本自动创建 Secrets（需要 GitHub CLI）：

```powershell
# 安装 GitHub CLI
winget install GitHub.cli

# 登录
gh auth login

# 设置 Secrets
gh secret set JWT_SECRET --body "your_jwt_secret_here"
gh secret set CRYPTO_AES_KEY --body "your_aes_key_here"
```

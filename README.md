#  订阅

将多个节点和订阅合并为单一订阅链接,部署到 Cloudflare Pages。

## 部署

### 方式一:一键部署

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/chengege666/sub-c)

1. 点击上方按钮 → Continue with GitHub 授权 → 自动 Fork 并部署
2. 部署后进入 Workers & Pages → 你的 Worker → 设置 → 变量和机密:添加下列变量(`TOKEN`、`SUBAPI` 必填)
3. 可选:如需在线编辑页,在 设置 → 绑定 中添加 KV 命名空间绑定(变量名 `KV`);不绑定时用 `LINK` 变量提供节点
4. 访问 `https://你的Worker域名/{TOKEN}` 获取订阅(TOKEN 为你配置的值;绑定 KV 后浏览器访问为在线编辑页)

### 方式二:Cloudflare Pages 手动部署

1. Fork 或推本仓库到 GitHub
2. Cloudflare Pages → 创建项目 → 连接 Git → 选仓库
3. 框架预设:留空;构建命令:留空;输出目录:留空
4. 部署后,进入项目设置:
   - **函数 → KV 命名空间绑定**:变量名 `KV`,选择你的 KV 命名空间(如未创建,先在 Workers & Pages → KV 中创建)
   - **环境变量**:添加下列变量
5. 绑定自定义域后访问 `https://你的域名/{TOKEN}` 进入编辑页(TOKEN 为你配置的值)

## 变量

| 变量名 | 必填 | 默认值 | 说明 |
|---|---|---|---|
| `TOKEN` | 是 | - | 订阅入口路径,如 `auto`(访问 `/{TOKEN}` 获取订阅) |
| `KV` | 是 | - | KV 命名空间绑定,在「函数 → KV 命名空间绑定」中设置 |
| `SUBAPI` | 是 | - | 订阅转换后端地址,如 `sub.example.com` |
| `SUBCONFIG` | 否 | ACL4SSR_Online_MultiCountry | 转换规则配置文件 URL |
| `SUBNAME` | 否 | `sub` | 订阅文件名 |
| `SUBUPTIME` | 否 | `6` | 订阅更新间隔(小时) |
| `ADMIN_PASSWORD` | 否 | - | 编辑页密码,不配置则不启用 |
| `LINK` | 否 | - | 节点列表(绑定 KV 后失效) |

## 保持同步

本仓库已内置同步脚本(`.github/workflows/sync.yml`)。复刻(Fork)本仓库后:

1. 进入你的 Fork 仓库 → **Actions** 标签页 → 点击启用工作流(如提示需要开启,点击确认即可)
2. 左侧选择 **"同步上游仓库"** → 点击 **Run workflow**,即会同步原仓库最新代码
3. 以后每次需要同步时,重复步骤 2 即可

说明:
- 自动合并以原仓库代码为准,若你修改过同一处代码且发生冲突,该处会以原仓库版本覆盖
- 也可随时在 Actions 页手动触发同步

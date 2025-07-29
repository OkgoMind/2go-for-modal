# Modal 部署指南,会封号，勿用

1. 注册网站：[https://modal.com](https://modal.com)

2. 在个人资料页获取 API Token，例如：modal token set –token-id ak-XVbmGM9PF3TLwiu52 –token-secret as-Wo9a4CUsfGHkFu8q

3. 在 GitHub 仓库的 Settings → Secrets and variables → Actions 中，设置以下两个变量：

- `MODAL_TOKEN_ID`  
  这是你的 Modal Token ID，通常是以 `ak-` 开头的一串字符，比如 `ak-XVbmGM9PF3TLwiu52`。

- `MODAL_TOKEN_SECRET`  
  这是你的 Modal Token Secret，通常是以 `as-` 开头的一串字符，比如 `as-Wo9a4CUsfGHkFu8q7`。

4. 修改app.py里面的变量参数，deploy.py里面的app名字最好还是修改一下，最好让AI再修改一下。启动github action即可。
5.  节点获取说明：  
根据 UUID 和固定隧道域名手动配置，支持 vmess、vless、trojan 三种协议。

---

## 🌍 运行地域（Region）配置说明

在 `deploy.py` 文件中的第十八行：

```python
sandbox = modal.Sandbox.create(app=app, image=image, timeout=86400, region="us-west")
```
你可以根据实际需求修改 region="..." 来选择部署任务运行的地理位置。该参数影响执行延迟、合规性和数据传输速度等

### 🌐 Modal 支持的 Region 列表

| Modal Region 值        | Cloud Provider | 地理位置描述                             |
|------------------------|----------------|------------------------------------------|
| `"us-east"`            | AWS / GCP      | 美国东部（弗吉尼亚、俄亥俄）             |
| `"us-west"`            | AWS / GCP      | 美国西部（加州、俄勒冈）                 |
| `"us-central"`         | GCP            | 美国中部（爱荷华）                       |
| `"eu-west"`            | AWS / GCP      | 欧洲西部（比利时、爱尔兰、法国）         |
| `"eu-north"`           | AWS            | 欧洲北部（斯德哥尔摩）                   |
| `"ap-northeast"`       | AWS / GCP      | 亚太东北（东京、首尔、大阪）             |
| `"ap-southeast"`       | AWS / GCP      | 亚太东南（新加坡、雅加达）               |
| `"ap-south"`           | AWS            | 亚太南部（孟买）                         |

️ 示例：
将 region="us-west" 替换为 region="ap-southeast" 可将任务运行在新加坡或雅加达的数据中心。


## 感谢


特别感谢上游项目作者 eooce 的 py-argo 项目。

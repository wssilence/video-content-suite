# 浏览器操作准则

> ⚠️ **本文件已统一，详细准则请读取公司权威文件**
> 📄 **准则文件路径**: `/root/.openclaw/BROWSER_GUIDELINES.md`
> 🔴 **禁止在本文件自行添加浏览器操作规则，必须经 Leo 批准后更新公司准则文件**

**每次浏览器操作前必须执行**:
```
read({ file: "/root/.openclaw/BROWSER_GUIDELINES.md" })
```

---

## 快速参考

| 场景 | 节点 |
|------|------|
| 默认（未指定） | **Mac Mini** (`node: "macmini"`) |
| Mac Mini不在线 | Linux网关 (`target: "host", profile: "openclaw"`) |
| Leo指定mac节点 | wssMac (`node: "wssMac", profile: "mac"`) |
| Leo指定linux | Linux网关 (`target: "host", profile: "openclaw"`) |
| 需要已登录状态 | Chrome MCP (`target: "host", profile: "user"`) |


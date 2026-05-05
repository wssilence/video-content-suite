# 浏览器操作准则
> **版本**: 2026-04-10 v3（最新权威版本）
> **强制级别**: 🔴 P0
> **冲突处理**: 本文件优先于各员工workspace内的BROWSER_GUIDELINES.md

---

## 一、节点别名（必须记住）

| Leo说的话 | 实际节点 | displayName | 说明 |
|----------|---------|-------------|------|
| `macmini` / `mini` | Mac Mini节点 | `Mac Mini` | **默认浏览器节点**，有独立网关 |
| `mac` / `wssMac` / `mac节点` | Mac节点 | `wssMac` | Leo明确指定时才用 |
| `linux` / `linux浏览器` / `网关` | Linux网关 | — | 备用 |

---

## 二、使用规则（强制）

### 规则1：默认 → Mac Mini（`Mac Mini`）
未指定节点时，所有浏览器操作默认由 Mac Mini 执行。
Mac Mini 有独立网关，Linux 网关把指令路由过去，Mac Mini 本地自主操作浏览器。

```javascript
// ✅ 默认方式
browser({ action: "open", target: "node", node: "Mac Mini", url: "https://..." })
browser({ action: "screenshot", target: "node", node: "Mac Mini" })
browser({ action: "snapshot", target: "node", node: "Mac Mini" })
browser({ action: "act", target: "node", node: "Mac Mini", request: { kind: "click", ref: "..." } })
```

### 规则2：Mac Mini不在线 → Linux网关备用
```javascript
// ✅ 备用
browser({ action: "open", target: "host", profile: "openclaw", url: "https://..." })
browser({ action: "screenshot", target: "host", profile: "openclaw" })
```

### 规则3：Leo指定 mac / wssMac → 两种方式均可

**方式A：扩展中继（`profile: "mac"`）**
前置：Edge/Chrome 已启动，OpenClaw 扩展已附加（badge 显示 ON）
```javascript
browser({ action: "open", target: "node", node: "wssMac", profile: "mac", url: "https://..." })
browser({ action: "screenshot", target: "node", node: "wssMac", profile: "mac", targetId: "..." })
```

**方式B：CDP连接（`profile: "mac-cdp"`）— 推荐用于已登录平台**
前置：Chrome 已启动并开启远程调试（port 19222）
已登录平台：小红书 / 抖音 / B站 / 掘金 / Medium
```javascript
browser({ action: "open", target: "node", node: "wssMac", profile: "mac-cdp", url: "https://..." })
browser({ action: "screenshot", target: "node", node: "wssMac", profile: "mac-cdp", targetId: "..." })
```

### 规则4：Leo指定 linux → Linux网关
```javascript
browser({ action: "open", target: "host", profile: "openclaw", url: "https://..." })
browser({ action: "screenshot", target: "host", profile: "openclaw" })
```

### 规则5：需要已登录状态（Linux Chrome MCP）
Linux网关附加到已运行Chrome，继承登录态：
```javascript
browser({ action: "open", target: "host", profile: "user", url: "https://..." })
browser({ action: "screenshot", target: "host", profile: "user" })
```

---

## 三、场景速查表

| 场景 | 节点 | 关键参数 |
|------|------|---------|
| **默认（未指定）** | Mac Mini | `target: "node", node: "Mac Mini"` |
| **Mac Mini不在线** | Linux备用 | `target: "host", profile: "openclaw"` |
| **mac/wssMac（通用）** | wssMac | `target: "node", node: "wssMac", profile: "mac"` |
| **mac/wssMac（已登录平台）** | wssMac | `target: "node", node: "wssMac", profile: "mac-cdp"` |
| **linux浏览器** | Linux | `target: "host", profile: "openclaw"` |
| **Linux已登录Chrome** | Linux MCP | `target: "host", profile: "user"` |

---

## 四、Mac Mini说明

- **独立网关**：Mac Mini 自带 OpenClaw 网关，浏览器在本地执行，不依赖 Linux 网关
- **路由方式**：Linux 网关配置 `gateway.nodes.browser.node = "Mac Mini"`，自动路由
- **不在线时**：任务降级到 Linux 网关，必须通知 Leo

## 五、wssMac 登录状态

wssMac Chrome 上已保存的登录状态（`mac-cdp`可直接使用）：
- 小红书、抖音、B站、掘金、Medium

---

*最后更新: 2026-04-10 v3 by Sun (CEO)*
*本文件是浏览器操作的唯一权威来源*

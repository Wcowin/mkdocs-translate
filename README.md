# MkDocs Material 智谱清言翻译系统

为 MkDocs Material 网站添加智能网页翻译功能的完整解决方案。基于智谱清言 API，支持 10+ 种语言的实时翻译。

## ✨ 核心特性

- 🚀 **高性能翻译**: 基于 GLM-4-Flash 快速模型，支持批量并发翻译
- 💾 **智能缓存**: 多级缓存策略，避免重复翻译，提升访问速度
- 🎯 **内容智能**: 自动识别并跳过代码、链接等不需翻译的内容
- 🌍 **全局设置**: 支持页面级和全局翻译偏好设置
- 📱 **响应式UI**: 完美适配桌面和移动设备
- 🔧 **零配置**: 开箱即用，配置简单

## 🎬 示例演示

<video src="example.mp4" controls width="600">
  您的浏览器不支持 video 标签。
</video>

## 📁 项目文件说明

```
mkdocs-translate/
├── 📄 README.md                    # 📖 使用教程（本文档）
├── ⚙️ glm-config.js               # 🔧 核心配置文件（需要配置 API 密钥）
└── 🧠 glm-translate.js            # 💻 翻译引擎核心脚本

```

### 文件作用说明

| 文件 | 作用 | 是否必需 |
|------|------|----------|
| `glm-config.js` | 基础配置和 API 密钥设置 | ✅ 必需 |
| `glm-translate.js` | 翻译功能核心实现 | ✅ 必需 |
| `translate-config.js` | 高级性能优化配置 | 🔧 可选 |
| `generate_translate_config.py` | 配置文件生成工具 | 🔧 可选 |

## 🚀 快速部署

### 步骤 1: 获取 API 密钥

1. 访问 [智谱清言开放平台](https://open.bigmodel.cn/)
2. 注册并获取免费 API 密钥（新用户有免费额度）

### 步骤 2: 下载文件

将以下文件下载到您的 MkDocs 项目的 `docs/javascripts/` 目录：

```
docs/javascripts/
├── glm-config.js      # 核心配置文件
└── glm-translate.js   # 翻译脚本
```

### 步骤 3: 配置 mkdocs.yml

在您的 `mkdocs.yml` 文件中添加：

```yaml
# JavaScript 文件引入
extra_javascript:
  - javascripts/glm-config.js
  - javascripts/glm-translate.js

# 语言切换按钮配置(默认中英日)
extra:
  alternate:
    - name: 中文
      link: "javascript:translateTo('chinese_simplified');"
      lang: zh
    - name: English  
      link: "javascript:translateTo('english');"
      lang: en
    - name: 日本語
      link: "javascript:translateTo('japanese');"
      lang: ja
```

### 步骤 4: 设置 API 密钥

编辑 `docs/javascripts/glm-config.js` 文件，找到以下代码并替换您的 API 密钥：

```javascript
const GLM_CONFIG = {
  api: {
    // 替换为您的 API 密钥
    apiKey: 'your-api-key-here',
    
    // 其他配置保持默认即可
    endpoint: 'https://open.bigmodel.cn/api/paas/v4/chat/completions',
    model: 'glm-4-flash'
  }
};
```

### 步骤 5: 启动测试

```bash
# 启动开发服务器
mkdocs serve

# 访问 http://localhost:8000
# 点击右上角的语言切换按钮测试翻译功能
```

完成！您的网站现在已经支持智能翻译了。

## ⚙️ 主要配置

### API 设置
```javascript
// 在 glm-config.js 中配置
const GLM_CONFIG = {
  api: {
    apiKey: 'your-api-key',        // 🔑 您的智谱清言 API 密钥
    model: 'glm-4-flash',          // 🧠 使用快速模型
    timeout: 8000,                 // ⏱️ 请求超时时间(毫秒)
    maxRetries: 3                  // 🔄 失败重试次数
  }
}
```

### 性能调优
```javascript
performance: {
  batchSize: 20,                   // 📦 单次翻译文本数量
  maxConcurrent: 6,                // 🚀 最大并发请求数
  enableCache: true,               // 💾 启用智能缓存
  cacheExpiry: 86400000           // 🕐 缓存有效期(24小时)
}
```

### 支持的语言

| 语言 | 代码标识 | 语言 | 代码标识 |
|------|----------|------|----------|
| 简体中文 | `chinese_simplified` | English | `english` |
| 日本語 | `japanese` | 한국어 | `korean` |
| Français | `french` | Deutsch | `german` |
| Español | `spanish` | Italiano | `italian` |
| Português | `portuguese` | Русский | `russian` |

### 智能特性

#### 🎯 内容识别
系统自动跳过以下内容的翻译：
- 代码块和内联代码
- URL 链接和邮箱地址  
- 数字和纯符号
- 技术术语（如 API、GitHub、JSON 等）

#### 💾 缓存策略
- **页面缓存**: 避免相同页面重复翻译
- **全局缓存**: 相同文本在不同页面间共享
- **持久化存储**: 刷新页面后保持翻译状态

## 🎨 使用指南

### 基本使用

1. **切换语言**: 点击页面右上角的语言按钮
2. **选择范围**: 首次翻译时选择翻译范围
   - **仅当前页面**: 只翻译当前页面
   - **全局翻译**: 翻译当前页面 + 自动翻译其他页面
3. **恢复中文**: 点击"中文"按钮恢复原文

### 翻译范围说明

#### 📄 仅当前页面
- 仅翻译当前访问的页面
- 访问其他页面时显示原文
- 适合偶尔查看外语内容

#### 🌍 全局翻译  
- 翻译当前页面并设置全局偏好
- 访问其他页面时自动翻译
- 适合需要持续阅读外语内容

### 自定义样式

如需自定义翻译按钮和提示的样式，可在您的 CSS 中添加：

```css
/* 翻译进度提示 */
#translate-status {
  position: fixed !important;
  bottom: 20px !important;
  right: 20px !important;
  background: rgba(32, 33, 36, 0.95) !important;
  color: white !important;
  padding: 12px 16px !important;
  border-radius: 8px !important;
  font-size: 13px !important;
  z-index: 10000 !important;
}

/* 语言切换按钮悬停效果 */
.md-header__option:hover {
  transform: translateY(-1px);
  transition: transform 0.2s ease;
}
```

## ❓ 常见问题

### Q1: 翻译按钮不显示怎么办？

**检查步骤**：
1. 确认 `mkdocs.yml` 中已正确配置 `extra_javascript`
2. 检查 JavaScript 文件路径是否正确
3. 按 F12 打开开发者工具，查看 Console 是否有错误信息
4. 确认 API 密钥已正确配置

### Q2: 翻译失败或很慢怎么办？

**解决方案**：
```javascript
// 在 glm-config.js 中调整配置
performance: {
  batchSize: 15,          // 减小批处理大小
  maxConcurrent: 4,       // 减少并发数
  timeout: 10000          // 增加超时时间
}
```

### Q3: 如何清除翻译缓存？

在浏览器控制台执行：
```javascript
// 清除所有翻译缓存
localStorage.removeItem('glm_translate_cache');
localStorage.removeItem('glm_translate_preferences');
location.reload();
```

### Q4: 某些内容不应该被翻译

在 `glm-config.js` 中添加跳过规则：
```javascript
content: {
  skipSelectors: [
    '.no-translate',        // 添加 CSS 类
    '#special-content',     // 特定 ID
    '[data-notranslate]'    // 特定属性
  ],
  preserveTerms: [
    'API', 'GitHub', 'MkDocs'  // 专有名词
  ]
}
```

### Q5: 想要支持更多语言

在 `mkdocs.yml` 中添加语言配置：
```yaml
extra:
  alternate:
    - name: Français
      link: "javascript:translateTo('french');"
      lang: fr
    - name: Deutsch  
      link: "javascript:translateTo('german');"
      lang: de
```

## � 故障排除

### 错误代码说明

| 错误代码 | 含义 | 解决方案 |
|---------|------|----------|
| `401` | API 密钥无效 | 检查并更新 API 密钥 |
| `429` | 请求频率过高 | 降低 `maxConcurrent` 参数 |
| `500` | 服务器错误 | 稍后重试 |
| `TIMEOUT` | 请求超时 | 增加 `timeout` 值 |

### 调试模式

启用详细日志查看问题：
```javascript
// 在 glm-config.js 中启用
debug: {
  enabled: true,
  logLevel: 'debug',
  showStats: true
}
```

### 性能监控

查看翻译性能统计：
- 按 F12 打开开发者工具
- 在 Console 中查看翻译统计信息
- 监控缓存命中率和响应时间

## 🔄 更新记录

### v2.1.0 (最新)
- ✨ 新增腾讯云翻译 API 支持
- ✨ 新增翻译 API 选择器
- 🚀 优化通知显示位置（右下角）
- 🎯 新增正文内容优先翻译
- 🐛 修复中文恢复功能

### v2.0.0
- ✨ 智能缓存系统
- ✨ 批量翻译功能  
- ✨ 连接池管理
- 🚀 性能提升 300%

## 📄 许可协议

本项目基于 **MIT License** 开源协议发布。

## 🙏 感谢

- [智谱清言](https://open.bigmodel.cn/) 提供强大的 AI 翻译能力
- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) 优秀的文档框架

## 📞 获取帮助

遇到问题？获取帮助的方式：

1. 📖 首先查阅本文档的故障排除部分
2. 🔍 搜索 [GitHub Issues](https://github.com/Wcowin/mkdocs-translate/issues)
3. 💬 创建新的 Issue 详细描述问题
4. 📧 联系作者获取技术支持

---

**开始享受mkdocs智能翻译的便利吧！** 🌟

> **提示**: 建议先在测试环境中配置和测试，确保一切正常后再部署到生产环境。
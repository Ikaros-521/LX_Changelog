# LX_Changelog —— 洛曦各软件更新日志

本仓库集中维护洛曦旗下所有软件的更新日志，官方网站（[LX_Official_Website](https://github.com/LuoXi-Project/LX_Official_Website)）通过 **jsDelivr CDN** 实时拉取 `changelog.json`，发布到官网的「更新日志」页面。

> 你只需更新本仓库的 `changelog.json`，官网会在几分钟（jsDelivr 缓存刷新）内自动展示新内容，**无需重新构建官网**。

---

## 数据格式

`changelog.json` 顶层结构：

```jsonc
{
  "products": {
    "<product-id>": {              // product-id 与官网 products 页的 id 一致
      "name": "显示名称",
      "repo": "owner/repo",        // 可选，仅开源产品填写
      "versions": [
        {
          "version": "v2.5.0",     // 版本号
          "date": "2026-07-01",    // 发布日期 YYYY-MM-DD
          "changes": {
            "added":    ["..."],   // 新增功能，页面显示为绿色标签
            "improved": ["..."],   // 优化改进，页面显示为蓝色标签
            "fixed":    ["..."]    // 问题修复，页面显示为橙色标签
          }
        }
      ]
    }
  }
}
```

### 字段说明

| 字段 | 必填 | 说明 |
|---|---|---|
| `name` | ✅ | 产品在官网展示的中文名 |
| `repo` | ❌ | 仅开源产品填写，格式 `owner/repo`，用于页面跳转 GitHub |
| `versions[]` | ✅ | 版本列表，**新的版本加在数组头部**（最前），页面按此顺序展示 |
| `versions[].version` | ✅ | 版本号，如 `v2.5.0` |
| `versions[].date` | ✅ | `YYYY-MM-DD` 格式 |
| `versions[].changes.added` | ❌ | 字符串数组，可省略或为 `[]` |
| `versions[].changes.improved` | ❌ | 同上 |
| `versions[].changes.fixed` | ❌ | 同上 |

### product-id 对照表

`product-id` 必须与官网 `/products` 页面各产品的 `id` 字段一致：

| product-id | 产品 |
|---|---|
| `luoxi-ai` | 洛曦AI |
| `ai-vtuber` | AI Vtuber |
| `digital-human` | 实时语音数字人 |
| `smart-clip` | 洛曦智剪 |
| `LiveBotX` | 直播间智能互动助手 |
| `travel` | 洛曦云旅 |
| `danmu-assistant` | 直播弹幕助手 |
| `printer` | 直播辅助打印机 |
| `bot` | 洛曦Bot |
| `captions` | 洛曦 Web 字幕打印机 |
| `live2d` | 实时语音 Live2D |

---

## 如何发布一条更新日志

1. 编辑 `changelog.json`，在对应产品的 `versions` 数组**最前面**插入一条新版本：
   ```jsonc
   {
     "version": "v2.6.0",
     "date": "2026-07-15",
     "changes": {
       "added":    ["新增 XXX 功能"],
       "improved": ["优化 YYY 体验"],
       "fixed":    ["修复 ZZZ 问题"]
     }
   }
   ```
2. 提交并 push 到 `main` 分支。
3. 等待 jsDelivr 缓存刷新（通常几分钟内），刷新官网「更新日志」页面即可看到。

> 小技巧：想立即强制刷新 jsDelivr 缓存，可访问 `https://purge.jsdelivr.net/gh/Ikaros-521/LX_Changelog@main/changelog.json`。

---

## 本仓库不包含

- 软件源代码（各开源产品在各自仓库）
- 官网代码（见 [LX_Official_Website](https://github.com/LuoXi-Project/LX_Official_Website)）
- 任何构建流程——纯数据仓库，push 即生效

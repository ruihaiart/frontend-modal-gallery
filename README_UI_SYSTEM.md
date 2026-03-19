# GenSpark UI Design System - 完整指南

## 🎯 项目概述

GenSpark UI 设计系统是一套完整的用户界面设计规范，专为 GenSpark 项目定制，包含**按钮组件**和**弹窗组件**的完整设计标准和实现规范。

## 📁 文件结构

```
frontend-modal-gallery/
├── .cursorrules                          # Cursor AI 核心规则文件 ⭐
├── genspark-ui-design-rules.md          # 完整设计系统文档
├── CURSOR_RULES_使用指南.md              # Cursor 使用指南
├── ui-system-test.html                   # 完整 UI 系统测试页面 ⭐
├── button-test-example.html              # 按钮系统测试页面
├── modal-showcase.html                   # 原有弹窗展示页面
└── README_UI_SYSTEM.md                   # 本文档
```

## 🚀 快速开始

### 1. 设置 Cursor AI 规则

将 `.cursorrules` 文件放置在您的项目根目录：

```bash
# 复制规则文件到项目根目录
cp frontend-modal-gallery/.cursorrules /your-project/.cursorrules
```

### 2. 重启 Cursor 编辑器

重启 Cursor 编辑器以确保规则生效。

### 3. 测试 AI 是否遵循规范

在 Cursor 中测试以下命令：

```
请创建一个确认删除的弹窗
```

如果 AI 回复包含正确的弹窗结构和按钮组合，说明规则已生效！

## 📋 设计系统核心规范

### 按钮类型

| 类型 | 使用场景 | 样式特征 |
|------|----------|----------|
| **主按钮（大圆角）** | 引导点击、常规入口 | `#232425` 背景，30px 圆角 |
| **主按钮（小圆角）** | 功能操作、严肃确认 | `#232425` 背景，8px 圆角 |
| **强引导按钮** | 重要功能引导 | `#0F7FFF` 背景，30px 圆角 |
| **线型按钮** | 次要操作、取消 | 透明背景，边框样式 |
| **弱按钮** | 辅助功能、设置 | `#F5F5F5` 背景，12px 圆角 |
| **危险按钮** | 删除等破坏性操作 | `#EF4444` 背景，8px 圆角 |

### 弹窗类型

| 类型 | 使用场景 | 尺寸 | 按钮组合 |
|------|----------|------|----------|
| **确认弹窗** | 删除确认、重要决策 | 400px | 线型-8px（取消）+ 主按钮-8px（确认）**圆角一致** |
| **表单弹窗** | 数据录入、设置配置 | 500px | 线型-12px（取消）+ 主按钮-12px（提交）**圆角一致** |
| **通知弹窗** | 系统通知、功能更新 | 500px | 弱按钮-12px（关闭）+ 强引导-12px（操作）**圆角一致** |
| **预览弹窗** | 图片预览、内容查看 | 700px | 弱按钮-12px（关闭）+ 主按钮-12px（下载）**圆角一致** |
| **设置弹窗** | 系统配置、偏好设置 | 500px | 线型-12px（取消）+ 主按钮-12px（保存）**圆角一致** |

### 🎯 重要的圆角一致性规则

**当弹窗包含两个按钮时，两个按钮必须使用相同的圆角半径以保持视觉一致性：**

- **确认弹窗**: 严肃场景，两个按钮都使用 8px 圆角
- **其他弹窗**: 功能场景，两个按钮都使用 12px 圆角

## 🛠️ 使用方法

### 在 Cursor 中创建按钮

```bash
# 主按钮示例
"请创建一个表单提交按钮"
→ AI 将生成主按钮（大圆角）

# 确认操作按钮
"请创建一个确认删除按钮"  
→ AI 将生成主按钮（小圆角）

# 功能引导按钮
"请创建一个升级引导按钮"
→ AI 将生成强引导按钮
```

### 在 Cursor 中创建弹窗

```bash
# 确认弹窗
"请创建一个确认删除的弹窗"
→ AI 将生成小尺寸确认弹窗 + 正确按钮组合

# 表单弹窗  
"请创建一个编辑用户信息的弹窗"
→ AI 将生成中尺寸表单弹窗 + 正确按钮组合

# 通知弹窗
"请创建一个新功能介绍弹窗"
→ AI 将生成通知弹窗 + 引导按钮组合
```

### 创建组件

```bash
# React 组件
"请创建一个 React 弹窗组件，支持 GenSpark 设计规范"

# Vue 组件
"请创建一个 Vue 按钮组件，遵循 GenSpark 设计系统"

# 完整表单
"请创建一个用户注册表单，包含正确的弹窗和按钮组合"
```

## 🎨 颜色系统

```css
/* 主色调 */
--color-primary: #232425;           /* 主按钮背景色 */
--color-primary-hover: #393A3B;     /* 主按钮悬停态 */

/* 引导色 */
--color-guide: #0F7FFF;             /* 强引导按钮背景色 */
--color-guide-hover: #0E72E5;       /* 强引导按钮悬停态 */

/* 次要色 */
--color-secondary: #F5F5F5;         /* 弱按钮背景色 */
--color-secondary-hover: #E9E9E9;   /* 弱按钮悬停态 */

/* 功能色 */
--color-danger: #EF4444;            /* 危险操作按钮 */
--color-border: #E2E2E2;            /* 边框色 */
```

## 📐 尺寸规范

### 按钮尺寸

```css
/* 大按钮 */
.btn-large { width: 208px; height: 40px; font-size: 16px; }

/* 中按钮 */
.btn-medium { width: 144px; height: 36px; font-size: 16px; }

/* 小按钮 */  
.btn-small { width: 96px; height: 28px; font-size: 16px; }
```

### 弹窗尺寸

```css
/* 小型弹窗 */
.modal-small { width: 400px; max-width: 400px; }

/* 中型弹窗 */
.modal-medium { width: 500px; max-width: 600px; }

/* 大型弹窗 */
.modal-large { width: 700px; max-width: 800px; }
```

### 圆角规范

- **大圆角 (30px)**: 自然、轻松 - 主按钮（大圆角）、强引导按钮
- **中圆角 (16px)**: 标准 - 弹窗、卡片
- **小圆角 (12px)**: 功能性 - 线型按钮、弱按钮
- **紧凑圆角 (8px)**: 严肃 - 主按钮（小圆角）、危险按钮

## 📖 测试页面说明

### ui-system-test.html 
**完整 UI 系统测试页面** ⭐
- 展示所有弹窗类型和对应的按钮组合
- 实际可交互的弹窗示例
- 按钮组合模式说明
- 适合开发者学习和参考

访问：`http://localhost:8000/ui-system-test.html`

### button-test-example.html
**按钮系统专项测试**
- 所有按钮类型的完整展示
- 按钮状态演示（normal, hover, disabled, loading）
- 按钮尺寸对比
- 适合按钮样式开发

### modal-showcase.html
**原有弹窗展示页面**
- GenSpark 项目实际使用的弹窗
- 完整的弹窗代码示例
- 适合了解项目中的实际应用

## 🎯 最佳实践

### 1. 弹窗 + 按钮组合规则

**严格遵循以下组合模式：**

```html
<!-- 确认弹窗：线型-8px + 主按钮-8px（圆角一致） -->
<div class="modal-footer">
  <button class="btn-base btn-outline-8px btn-medium">取消</button>
  <button class="btn-base btn-primary-8px btn-medium">确认</button>
</div>

<!-- 表单弹窗：线型-12px + 主按钮-12px（圆角一致） -->
<div class="modal-footer">
  <button class="btn-base btn-outline-12px btn-medium">取消</button>
  <button class="btn-base btn-primary-12px btn-medium">保存</button>
</div>

<!-- 通知弹窗：弱按钮-12px + 强引导-12px（圆角一致） -->
<div class="modal-footer">
  <button class="btn-base btn-secondary btn-medium" style="border-radius: 12px;">稍后</button>
  <button class="btn-base btn-guide-12px btn-medium">立即体验</button>
</div>
```

### 2. 层级规则

- 每个弹窗只能有一个主按钮
- 强引导按钮谨慎使用，用于关键转化点
- 保持清晰的视觉层级
- 一致的间距和对齐
- **圆角一致性：弹窗中的两个按钮必须使用相同的圆角半径**

### 3. 无障碍要求

- 弹窗必须捕获焦点并在关闭时返回触发元素
- ESC 键关闭弹窗
- 支持键盘导航
- 提供正确的 ARIA 标签

## 🔧 故障排除

### 问题：AI 不遵循设计规范

**解决方案：**
1. 确认 `.cursorrules` 文件在项目根目录
2. 重启 Cursor 编辑器
3. 明确提及："请遵循 GenSpark UI 设计系统规范"

### 问题：按钮组合不正确

**解决方案：**
```
请确保按钮组合符合规范：
- 确认弹窗用线型按钮+主按钮小圆角
- 表单弹窗用线型按钮+主按钮大圆角
- 通知弹窗用弱按钮+强引导按钮
```

### 问题：弹窗尺寸不合适

**解决方案：**
```
请使用正确的弹窗尺寸：
- 确认弹窗：modal-small (400px)
- 表单弹窗：modal-medium (500px)  
- 预览弹窗：modal-large (700px)
```

## 📚 参考文档

| 文档 | 说明 | 用途 |
|------|------|------|
| `.cursorrules` | Cursor AI 核心规则 | 让 AI 遵循设计规范 |
| `genspark-ui-design-rules.md` | 完整设计系统文档 | 开发者参考手册 |
| `CURSOR_RULES_使用指南.md` | Cursor 使用指南 | 学习如何与 AI 对话 |
| `ui-system-test.html` | 完整测试页面 | 实际效果演示 |

## ✅ 质量检查清单

在使用 AI 生成的代码前，请检查：

**弹窗结构检查:**
- [ ] 使用了正确的弹窗结构（overlay → dialog → header/body/footer）
- [ ] 应用了合适的尺寸类（modal-small/medium/large）
- [ ] 包含了关闭按钮和正确的标题
- [ ] 遵循了 16px 圆角规范

**按钮组合检查:**
- [ ] 按钮组合符合弹窗类型规范
- [ ] 使用了正确的按钮变体和尺寸
- [ ] 按钮顺序正确（次要操作在左，主要操作在右）
- [ ] 包含了所有必要的按钮状态
- [ ] **圆角一致性：弹窗中的两个按钮使用相同的圆角半径**

**技术实现检查:**
- [ ] CSS 类名遵循命名规范
- [ ] 使用了 CSS 自定义属性
- [ ] 包含了动画效果
- [ ] TypeScript 类型定义正确（如果使用）

## 🎉 开始使用

1. **复制 `.cursorrules` 文件到您的项目根目录**
2. **重启 Cursor 编辑器**
3. **测试一个简单的弹窗：** `"请创建一个确认删除的弹窗"`
4. **查看测试页面：** 打开 `ui-system-test.html` 了解完整效果
5. **参考使用指南：** 阅读 `CURSOR_RULES_使用指南.md` 学习更多技巧

---

🚀 **现在您的 Cursor AI 已经具备完整的 GenSpark UI 设计系统知识！AI 将始终按照规范生成一致、专业的按钮和弹窗代码。**

有任何问题，请参考使用指南或查看测试页面中的实际示例。 
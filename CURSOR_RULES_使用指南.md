# GenSpark UI Design System - Cursor Rules 使用指南

## 📋 概述

这个指南将帮助您在 Cursor 编辑器中设置和使用 GenSpark UI 设计系统规范，确保 AI 助手始终按照我们的设计标准生成**按钮组件**和**弹窗组件**代码。

## 🚀 快速设置

### 1. 文件放置

将 `.cursorrules` 文件放置在您的项目根目录下：

```
your-project/
├── .cursorrules                  # ← 放在这里
├── package.json
├── src/
└── ...
```

**重要**: 文件名必须是 `.cursorrules`（以点开头），不能是其他名称。

### 2. Cursor 设置验证

1. 打开 Cursor 编辑器
2. 确保您在正确的项目目录中
3. 检查状态栏是否显示 "Rules: Active" 或类似提示
4. 如果没有显示，尝试重启 Cursor

### 3. 验证规则生效

创建一个测试文件，向 AI 询问：

```
请帮我创建一个确认删除的弹窗
```

如果 AI 回复中包含了正确的弹窗结构和按钮组合，说明规则已生效。

## 💬 如何与 AI 对话

### 推荐的提问方式

#### ✅ 好的提问（按钮）：
```
请创建一个主按钮，用于表单提交
请帮我做一个取消操作的按钮
我需要一个功能引导按钮来引导用户升级
```

#### ✅ 好的提问（弹窗）：
```
请创建一个确认删除的弹窗
请做一个编辑个人资料的表单弹窗
我需要一个新功能介绍的通知弹窗
请创建一个图片预览弹窗
```

#### ✅ 好的提问（组合）：
```
请创建一个删除确认对话框，包含正确的按钮组合
请设计一个用户设置弹窗，遵循设计规范
```

#### ❌ 避免的提问：
```
做一个红色的按钮
创建一个很大的弹窗
我要一个圆形的弹窗
```

### 具体使用场景

#### 1. 创建确认弹窗
```
用户: 请创建一个确认删除的弹窗
AI: 根据 .cursorrules，我将创建一个确认弹窗（小尺寸），使用线型按钮（取消）+ 主按钮小圆角（确认）的组合：

<div class="modal-overlay">
  <div class="modal-dialog modal-small">
    <div class="modal-header">
      <h2>确认删除</h2>
      <button class="close-btn">×</button>
    </div>
    <div class="modal-body">
      <p>此操作不可撤销，确定要删除吗？</p>
    </div>
    <div class="modal-footer">
      <button class="btn-base btn-outline btn-medium">取消</button>
      <button class="btn-base btn-primary-small btn-medium">确认删除</button>
    </div>
  </div>
</div>
```

#### 2. 创建表单弹窗
```
用户: 请创建一个编辑用户信息的弹窗
AI: 根据设计规范，表单弹窗使用中等尺寸，按钮组合为线型（取消）+ 主按钮大圆角（提交）：

<div class="modal-overlay">
  <div class="modal-dialog modal-medium">
    <div class="modal-header">
      <h2>编辑用户信息</h2>
      <button class="close-btn">×</button>
    </div>
    <div class="modal-body">
      <form>
        <div class="form-group">
          <label>姓名</label>
          <input type="text" />
        </div>
        <!-- 更多表单字段 -->
      </form>
    </div>
    <div class="modal-footer">
      <button class="btn-base btn-outline btn-medium">取消</button>
      <button class="btn-base btn-primary-large btn-medium">保存更改</button>
    </div>
  </div>
</div>
```

#### 3. 创建完整的 React/Vue 组件
```
用户: 请创建一个支持 GenSpark 设计规范的 React 弹窗组件
AI: 根据 .cursorrules 规范：

interface ModalProps {
  type: 'confirmation' | 'form' | 'notification' | 'preview' | 'settings';
  size: 'small' | 'medium' | 'large';
  show: boolean;
  onClose: () => void;
  title: string;
  children: React.ReactNode;
  footer?: React.ReactNode;
}

const Modal: React.FC<ModalProps> = ({ type, size, show, onClose, title, children, footer }) => {
  // 完整的组件实现...
};
```

## 🎯 弹窗 + 按钮组合规则

### 1. 明确弹窗用途

在提问时说明弹窗的具体用途，AI 会自动选择合适的类型和按钮组合：

- **"确认删除"** → 确认弹窗 + 线型按钮（取消）+ 主按钮小圆角（确认）
- **"编辑资料"** → 表单弹窗 + 线型按钮（取消）+ 主按钮大圆角（保存）
- **"新功能介绍"** → 通知弹窗 + 弱按钮（稍后）+ 强引导按钮（立即体验）
- **"图片预览"** → 预览弹窗 + 弱按钮（关闭）+ 主按钮（下载）
- **"应用设置"** → 设置弹窗 + 线型按钮（取消）+ 主按钮小圆角（保存）

### 2. 检查生成代码

AI 生成弹窗代码后，检查以下要点：

#### ✅ 正确的弹窗结构：
```html
<div class="modal-overlay">
  <div class="modal-dialog modal-medium">  <!-- ✅ 正确的尺寸类 -->
    <div class="modal-header">              <!-- ✅ 包含头部 -->
      <h2 class="modal-title">标题</h2>
      <button class="close-btn">×</button>   <!-- ✅ 关闭按钮 -->
    </div>
    <div class="modal-body">                <!-- ✅ 内容区域 -->
      <!-- 内容 -->
    </div>
    <div class="modal-footer">              <!-- ✅ 按钮区域 -->
      <!-- 正确的按钮组合 -->
    </div>
  </div>
</div>
```

#### ✅ 正确的按钮组合：
```html
<!-- 确认弹窗 -->
<div class="modal-footer">
  <button class="btn-base btn-outline btn-medium">取消</button>        <!-- ✅ 线型按钮 -->
  <button class="btn-base btn-primary-small btn-medium">确认</button>  <!-- ✅ 主按钮小圆角 -->
</div>

<!-- 表单弹窗 -->
<div class="modal-footer">
  <button class="btn-base btn-outline btn-medium">取消</button>        <!-- ✅ 线型按钮 -->
  <button class="btn-base btn-primary-large btn-medium">提交</button>  <!-- ✅ 主按钮大圆角 -->
</div>
```

#### ❌ 需要修正的示例：
```html
<!-- ❌ 错误的弹窗结构 -->
<div class="popup">                        <!-- ❌ 错误的类名 -->
  <div style="width: 300px;">              <!-- ❌ 内联样式，未使用尺寸类 -->
    <h2>标题</h2>                          <!-- ❌ 缺少正确的头部结构 -->
    <p>内容</p>
    <button>确定</button>                   <!-- ❌ 未使用设计系统的按钮类 -->
  </div>
</div>
```

### 3. 要求特定功能

可以要求 AI 包含特定的设计系统功能：

```
请确保弹窗支持 ESC 键关闭
请添加点击外部区域关闭功能
请包含完整的无障碍支持
请添加动画效果
```

## 🔧 故障排除

### 问题 1: AI 未使用正确的弹窗结构

**解决方案：**
```
请使用 GenSpark 弹窗设计规范，包含 modal-overlay、modal-dialog、modal-header、modal-body、modal-footer 结构
```

### 问题 2: 按钮组合不正确

**解决方案：**
```
请确保按钮组合符合规范：确认弹窗用线型按钮+主按钮小圆角，表单弹窗用线型按钮+主按钮大圆角
```

### 问题 3: 弹窗尺寸不合适

**解决方案：**
```
请使用正确的弹窗尺寸：确认弹窗用 modal-small，表单弹窗用 modal-medium，预览弹窗用 modal-large
```

### 问题 4: 缺少无障碍支持

**解决方案：**
```
请添加弹窗的无障碍属性：role="dialog"、aria-labelledby、焦点管理、键盘导航
```

## 📚 实用命令示例

### 创建完整的弹窗系统
```
请根据 GenSpark 设计规范创建完整的弹窗组件系统，包括所有弹窗类型和正确的按钮组合
```

### 修复现有弹窗
```
请将这个弹窗修改为符合 GenSpark 设计规范：
[粘贴现有代码]
```

### 创建特定类型弹窗
```
请创建一个用户注册的表单弹窗，遵循 GenSpark 设计规范
请创建一个文件删除的确认弹窗，包含警告图标
请创建一个新功能介绍的通知弹窗，使用引导按钮
```

### 验证弹窗规范
```
请检查这个弹窗代码是否符合 GenSpark 设计规范：
[粘贴代码]
```

## ⚡ 高级技巧

### 1. 指定弹窗类型和按钮组合
```
请创建一个设置弹窗，使用中等尺寸，包含重置和保存按钮
```

### 2. 复杂弹窗需求
```
请创建一个多步骤的功能引导弹窗，包含上一步、下一步和完成按钮
```

### 3. 响应式弹窗
```
请确保弹窗在移动端也能正常显示，最大宽度不超过 90vw
```

### 4. 弹窗动画效果
```
请添加弹窗的进入和退出动画：scale + fade 效果
```

## 📖 弹窗类型快速参考

| 弹窗类型 | 使用场景 | 尺寸 | 按钮组合 |
|---------|----------|------|----------|
| **确认弹窗** | 删除确认、重要决策 | `modal-small` | 线型-8px（取消）+ 主按钮-8px（确认）**两个按钮都使用8px圆角** |
| **表单弹窗** | 数据录入、设置配置 | `modal-medium` | 线型-12px（取消）+ 主按钮-12px（提交）**两个按钮都使用12px圆角** |
| **通知弹窗** | 系统通知、功能更新 | `modal-medium` | 弱按钮-12px（关闭）+ 强引导-12px（操作）**两个按钮都使用12px圆角** |
| **预览弹窗** | 图片预览、内容查看 | `modal-large` | 弱按钮-12px（关闭）+ 主按钮-12px（下载）**两个按钮都使用12px圆角** |
| **设置弹窗** | 系统配置、偏好设置 | `modal-medium` | 线型-12px（取消）+ 主按钮-12px（保存）**两个按钮都使用12px圆角** |

### 📌 重要圆角一致性规则

**当弹窗包含两个按钮时，两个按钮必须使用相同的圆角半径以保持视觉一致性！**

- **确认弹窗**: 严肃场景，使用 8px 圆角（紧凑感）
- **其他弹窗**: 功能场景，使用 12px 圆角（平衡感）

## ✅ 质量检查清单

在使用 AI 生成的弹窗代码前，请检查：

### 弹窗结构检查
- [ ] 使用了正确的弹窗结构（overlay → dialog → header/body/footer）
- [ ] 应用了合适的尺寸类（modal-small/medium/large）
- [ ] 包含了关闭按钮和正确的标题
- [ ] 遵循了 16px 圆角规范

### 按钮组合检查
- [ ] 按钮组合符合弹窗类型规范
- [ ] 使用了正确的按钮变体和尺寸
- [ ] 按钮顺序正确（次要操作在左，主要操作在右）
- [ ] 包含了所有必要的按钮状态
- [ ] **圆角一致性：弹窗中的两个按钮使用相同的圆角半径**

### 无障碍检查
- [ ] 包含了正确的 ARIA 属性
- [ ] 支持键盘导航（ESC 关闭、Tab 切换）
- [ ] 实现了焦点管理
- [ ] 支持点击外部区域关闭（适当时）

### 技术实现检查
- [ ] CSS 类名遵循命名规范
- [ ] 使用了 CSS 自定义属性
- [ ] 包含了动画效果
- [ ] TypeScript 类型定义正确（如果使用）

## 🎯 最佳实践

1. **明确说明用途** - 告诉 AI 弹窗的具体使用场景
2. **验证按钮组合** - 确保按钮类型和组合符合规范
3. **检查尺寸规范** - 不同类型的弹窗使用对应的尺寸
4. **测试交互功能** - 验证关闭、提交等功能正常
5. **无障碍测试** - 确保键盘导航和屏幕阅读器支持

## 📝 常用提问模板

### 基础弹窗创建
```
"请创建一个[用途]的[类型]弹窗"
例如：请创建一个删除文件的确认弹窗
```

### 带特定功能的弹窗
```
"请创建一个[功能]弹窗，包含[特定要求]"
例如：请创建一个用户注册弹窗，包含表单验证功能
```

### React/Vue 组件
```
"请创建一个 [框架] 弹窗组件，支持 GenSpark 设计规范"
```

### 修复现有代码
```
"请将这个弹窗修改为符合 GenSpark 设计规范：[代码]"
```

---

**提示**: 如果遇到任何问题，可以随时要求 AI "严格遵循 GenSpark UI 设计系统规范" 来获得正确的弹窗和按钮组合实现。现在您的 Cursor AI 已经具备了完整的 UI 设计系统知识！ 🚀 
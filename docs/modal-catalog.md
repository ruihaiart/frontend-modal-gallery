# GenSpark 项目弹窗组件目录

## 概述

本文档记录了 GenSpark 项目中所有弹窗组件的详细信息，包括文件路径、使用场景、技术栈和样式特点。

## 技术栈分布

### 1. Naive UI (n-modal)
主要用于前端用户界面，提供现代化的弹窗体验。

### 2. Element UI (el-dialog)
主要用于管理后台系统，提供稳定的企业级组件。

### 3. 自定义弹窗
针对特殊场景定制的弹窗组件，提供更灵活的实现。

## 弹窗组件详细列表

### Naive UI 弹窗组件

#### 1. OutLimitModal - 使用限制弹窗
- **路径**: `frontend-nuxt/components/fashion/OutLimitModal.vue`
- **用途**: 当用户达到每日使用限制时显示
- **样式特点**:
  - 宽度: APP适配尺寸
  - 圆角: 20px
  - 阴影: 0px 3px 30px 0px rgba(0,0,0,0.08)
  - 按钮颜色: #232425
- **文本内容**:
  - 标题: "每日限额已达上限"
  - 描述: "您今天的使用次数已经达到上限，请明天再试或升级您的套餐以获得更多使用次数。"

#### 2. RevertGlobalCanvasDialog - 恢复画布对话框
- **路径**: `frontend-nuxt/components/agents/RevertGlobalCanvasDialog.vue`
- **用途**: 恢复画布到之前版本的确认对话框
- **样式特点**:
  - 宽度: 540px
  - 圆角: 16px
  - 警告框背景: #fffbee
  - 确认按钮: #232425, 取消按钮: #f5f5f5
- **功能**: 支持加载状态动画

#### 3. OutStorageLimitModal - 存储空间限制弹窗
- **路径**: `frontend-nuxt/components/fashion/OutStorageLimitModal.vue`
- **用途**: 当用户存储空间不足时显示
- **样式**: 与 OutLimitModal 类似

#### 4. PersonalizationDialog - 个性化设置弹窗
- **路径**: `frontend-nuxt/components/personalization_dialog.vue`
- **用途**: 用户个性化设置
- **特点**: mask-closable="false", close-on-esc="false"

#### 5. EditProjectNameModal - 编辑项目名称弹窗
- **路径**: `frontend-nuxt/components/agents/edit_project_name_modal.vue`
- **用途**: 修改项目名称

#### 6. FeedbackDialog - 反馈对话框
- **路径**: `frontend-nuxt/components/feedback_dialog.vue`
- **用途**: 收集用户反馈

#### 7. CreateModel - 创建模型弹窗
- **路径**: `frontend-nuxt/components/fashion/CreateModel.vue`
- **用途**: Fashion 功能中创建新模型

### 自定义弹窗组件

#### 1. DeleteConfirmationModal - 删除确认弹窗
- **路径**: `admin-nuxt/components/fashion_cms/DeleteConfirmationModal.vue`
- **用途**: Fashion CMS 系统中的删除确认
- **样式特点**:
  - 背景遮罩: rgba(0, 0, 0, 0.5)
  - 圆角: 8px
  - 删除按钮: #ff4136
  - 取消按钮: #ccc
- **功能**: 
  - 支持图片预览（主图 + 子图）
  - 键盘导航支持（方向键、Enter、Escape）

#### 2. ChatUpdateModal - 聊天功能更新弹窗
- **路径**: `frontend-nuxt/components/menu/ChatUpdateModal.vue`
- **用途**: 通知 Pro+ 用户的特权功能
- **样式特点**:
  - 圆角: 16px (2xl)
  - 阴影: 0px 3px 30px 0px rgba(0,0,0,0.08)
  - 主按钮: 黑色背景 (#000)
  - 次按钮: 灰色背景 (#F5F5F5)
- **元素**:
  - Emoji 图标: 🎁
  - 关闭按钮位置: top-12px, right-28px

#### 3. SearchResultShareModal - 搜索结果分享弹窗
- **路径**: `frontend-nuxt/components/deep_dive_search_component/search_result_share_modal.vue`
- **用途**: 分享搜索结果，支持图片下载和复制
- **样式特点**:
  - 全屏覆盖
  - 左右分栏布局
  - 左侧预览区背景: #f5f5f5
  - 右侧操作区背景: #fff
- **功能**:
  - 图片生成（html2canvas）
  - 复制到剪贴板
  - 下载为图片
  - 响应式缩放

#### 4. ItemDetailsModal - 项目详情弹窗
- **路径**: `admin-nuxt/components/fashion_cms/ItemDetailsModal.vue`
- **用途**: 显示项目详细信息
- **特点**: 包含确认提交的二次弹窗

#### 5. TrashBinModal - 回收站弹窗
- **路径**: `admin-nuxt/components/fashion_cms/TrashBinModal.vue`
- **用途**: 管理已删除的项目

#### 6. CreateProjectModal - 创建项目弹窗
- **路径**: `admin-nuxt/components/fashion_cms/CreateProjectModal.vue`
- **用途**: 创建新的 Fashion 项目
- **特点**: 包含 URL 验证的加载状态弹窗

### Element UI 弹窗组件

#### 1. Icon Detail Dialog - 图标详情弹窗
- **路径**: `admin-nuxt/components/icon-manager/views/Home.vue`
- **用途**: 显示图标的详细信息
- **样式特点**:
  - 圆角: 4px
  - 阴影: 0 2px 12px 0 rgba(0,0,0,.1)
  - 头部边框: 1px solid #f0f0f0
- **配置**:
  - close-on-click-modal: false
  - 自定义类名: icon-detail-dialog

## 统一设计规范

### 颜色规范
- **主色调**: #232425 (深灰黑色)
- **危险色**: #ff4136 (删除操作)
- **背景色**: #f5f5f5 (浅灰)
- **警告背景**: #fffbee (浅黄)
- **文本色**: #222325, #606366 (次要文本)

### 尺寸规范
- **小型弹窗**: APP适配尺寸
- **中型弹窗**: 500px-540px 宽
- **大型弹窗**: 800px+ 宽
- **圆角**: 4px-20px (根据场景)
- **内边距**: 16px-24px

### 阴影规范
- **标准阴影**: 0px 3px 30px 0px rgba(0,0,0,0.08)
- **轻量阴影**: 0 2px 12px 0 rgba(0,0,0,.1)
- **重型阴影**: 0 4px 20px rgba(0, 0, 0, 0.15)

### 动画规范
- **淡入淡出**: 0.25s ease
- **缩放动画**: scale(0.8) → scale(1)
- **滑动动画**: 抽屉式弹窗从侧边滑入

## 最佳实践

1. **无障碍支持**: 所有弹窗都应支持键盘操作（Escape 关闭、Tab 导航）
2. **响应式设计**: 移动端适配，特别是全屏弹窗
3. **加载状态**: 异步操作时显示加载动画
4. **错误处理**: 操作失败时的友好提示
5. **国际化**: 使用 $t() 函数处理多语言文本

## 使用建议

1. **选择合适的组件库**:
   - 前端用户界面优先使用 Naive UI
   - 管理后台使用 Element UI
   - 特殊需求时自定义实现

2. **保持一致性**:
   - 同一功能模块内使用相同的弹窗风格
   - 遵循项目的设计规范

3. **性能优化**:
   - 大型弹窗考虑懒加载
   - 避免在弹窗中进行复杂的计算

4. **用户体验**:
   - 提供明确的关闭方式
   - 重要操作需要二次确认
   - 保持弹窗内容简洁明了 
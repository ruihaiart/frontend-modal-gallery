# Genspark 弹窗样式库使用文档

本文档提供了Genspark项目中所有弹窗组件的使用指南、样式参数说明和最佳实践建议。

## 目录

1. [弹窗组件概览](#弹窗组件概览)
2. [基础弹窗组件](#基础弹窗组件)
   - [Modal 模态框](#modal-模态框)
   - [Drawer 抽屉](#drawer-抽屉)
   - [GlobalDialog 全局对话框](#globaldialog-全局对话框)
   - [ConfirmModal 确认框](#confirmmodal-确认框)
3. [第三方UI库弹窗](#第三方ui库弹窗)
   - [Element UI Dialog](#element-ui-dialog)
4. [特定功能弹窗](#特定功能弹窗)
   - [分享结果模态框](#分享结果模态框)
5. [弹窗使用最佳实践](#弹窗使用最佳实践)
6. [样式规范统一建议](#样式规范统一建议)

## 弹窗组件概览

Genspark项目中的弹窗组件可以分为以下几类：

- **基础弹窗组件**：通用的、可复用的弹窗基础组件
- **第三方UI库弹窗**：来自Element UI、Ant Design等第三方库的弹窗组件
- **特定功能弹窗**：为特定业务场景定制的弹窗组件

## 基础弹窗组件

### Modal 模态框

**文件路径**：`frontend-nuxt/ppt/components/Modal.vue`

**组件说明**：
通用模态框组件，使用Vue 3的Teleport特性将内容渲染到body，支持自定义宽度、动画效果和键盘Esc关闭等功能。

**参数说明**：

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| visible | Boolean | false | 控制模态框显示/隐藏 |
| width | Number | 480 | 模态框宽度 |
| closeButton | Boolean | false | 是否显示关闭按钮 |
| closeOnClickMask | Boolean | true | 点击遮罩层是否关闭 |
| closeOnEsc | Boolean | true | 按Esc键是否关闭 |
| contentStyle | Object | {} | 模态框内容的自定义样式 |

**事件**：

| 事件名 | 说明 |
|--------|------|
| update:visible | 更新visible的值 |
| closed | 模态框关闭后触发 |

**基本用法**：

```vue
<template>
  <button @click="showModal = true">打开模态框</button>
  
  <Modal v-model:visible="showModal" :width="500" closeButton>
    <div class="modal-example">
      <h2>模态框标题</h2>
      <p>这是一个居中显示的模态框示例</p>
      <div class="actions">
        <button @click="showModal = false">关闭</button>
      </div>
    </div>
  </Modal>
</template>

<script setup>
import { ref } from 'vue'
import Modal from '/ppt/components/Modal.vue'

const showModal = ref(false)
</script>
```

### Drawer 抽屉

**文件路径**：`frontend-nuxt/ppt/components/Drawer.vue`

**组件说明**：
侧边抽屉组件，支持从左侧或右侧弹出，适用于侧边菜单、表单和详情展示等场景。

**参数说明**：

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| visible | Boolean | false | 控制抽屉显示/隐藏 |
| width | Number | 320 | 抽屉宽度 |
| placement | String | 'right' | 抽屉位置，可选值：'left'或'right' |
| contentStyle | Object | {} | 抽屉内容的自定义样式 |

**事件**：

| 事件名 | 说明 |
|--------|------|
| update:visible | 更新visible的值 |

**基本用法**：

```vue
<template>
  <button @click="showDrawer = true">打开抽屉</button>
  
  <Drawer v-model:visible="showDrawer" :width="320" placement="right">
    <template #title>
      <span>抽屉标题</span>
    </template>
    <div class="drawer-content">
      <p>这是右侧抽屉内容</p>
      <button @click="showDrawer = false">关闭抽屉</button>
    </div>
  </Drawer>
</template>

<script setup>
import { ref } from 'vue'
import Drawer from '/ppt/components/Drawer.vue'

const showDrawer = ref(false)
</script>
```

### GlobalDialog 全局对话框

**文件路径**：`frontend-nuxt/components/GlobalDialog.vue`

**组件说明**：
全局对话框组件，支持确认模式和输入模式，适用于需要用户确认或输入内容的场景。

**参数说明**：

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| modelValue | Boolean | false | 控制对话框显示/隐藏 |
| mode | String | 'confirm' | 对话框模式，可选值：'confirm'或'input' |
| title | String | - | 对话框标题 |
| content | String | '' | 对话框内容（仅在confirm模式下有效） |
| warningContent | String | - | 警告内容（红色文字显示） |
| cancelButtonText | String | '取消' | 取消按钮文本 |
| confirmButtonText | String | '确认' | 确认按钮文本 |
| isDangerous | Boolean | false | 是否是危险操作（红色确认按钮） |
| initialValue | String | '' | 输入框初始值（仅在input模式下有效） |
| placeholder | String | - | 输入框占位符（仅在input模式下有效） |
| maxLength | Number | 100 | 输入框最大长度（仅在input模式下有效） |
| selectBeforeExtension | Boolean | false | 是否在选择文本时排除文件扩展名 |
| allowEmptyValue | Boolean | false | 是否允许输入框为空时确认 |
| confirmLoading | Boolean/null | null | 控制确认按钮的加载状态 |

**事件**：

| 事件名 | 说明 |
|--------|------|
| update:modelValue | 更新modelValue的值 |
| confirm | 点击确认按钮触发 |
| cancel | 点击取消按钮触发 |
| input-confirm | 输入确认时触发，参数为输入内容 |

**基本用法 - 确认模式**：

```vue
<template>
  <button @click="showDialog = true">打开确认对话框</button>
  
  <GlobalDialog
    v-model="showDialog"
    mode="confirm"
    title="确认操作"
    content="确定要执行此操作吗？"
    confirmButtonText="确定"
    cancelButtonText="取消"
    @confirm="handleConfirm"
    @cancel="handleCancel"
  />
</template>

<script setup>
import { ref } from 'vue'
import GlobalDialog from '/components/GlobalDialog.vue'

const showDialog = ref(false)

const handleConfirm = () => {
  console.log('用户点击确认')
}

const handleCancel = () => {
  console.log('用户点击取消')
}
</script>
```

**基本用法 - 输入模式**：

```vue
<template>
  <button @click="showInputDialog = true">打开输入对话框</button>
  
  <GlobalDialog
    v-model="showInputDialog"
    mode="input"
    title="重命名"
    initialValue="file.txt"
    placeholder="请输入新名称"
    confirmButtonText="保存"
    cancelButtonText="取消"
    @input-confirm="handleInputConfirm"
    @cancel="handleInputCancel"
  />
</template>

<script setup>
import { ref } from 'vue'
import GlobalDialog from '/components/GlobalDialog.vue'

const showInputDialog = ref(false)

const handleInputConfirm = (value) => {
  console.log('新名称:', value)
}

const handleInputCancel = () => {
  console.log('取消重命名')
}
</script>
```

### ConfirmModal 确认框

**文件路径**：`admin-nuxt/components/fashion_cms/ConfirmModal.vue`

**组件说明**：
简单的确认对话框，适用于需要用户确认的操作，如删除、提交等。

**参数说明**：

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| show | Boolean | false | 控制对话框显示/隐藏 |
| title | String | 'Confirm' | 对话框标题 |
| message | String | - | 对话框消息内容（必填） |
| confirmText | String | 'OK' | 确认按钮文本 |
| cancelText | String | 'Cancel' | 取消按钮文本 |

**事件**：

| 事件名 | 说明 |
|--------|------|
| confirm | 点击确认按钮触发 |
| cancel | 点击取消按钮触发 |

**基本用法**：

```vue
<template>
  <button @click="showConfirm = true">删除项目</button>
  
  <ConfirmModal
    :show="showConfirm"
    title="删除确认"
    message="确定要删除这个项目吗？此操作不可撤销。"
    confirmText="删除"
    cancelText="取消"
    @confirm="handleConfirm"
    @cancel="showConfirm = false"
  />
</template>

<script setup>
import { ref } from 'vue'
import ConfirmModal from '/components/fashion_cms/ConfirmModal.vue'

const showConfirm = ref(false)

const handleConfirm = () => {
  console.log('用户确认删除')
  showConfirm.value = false
}
</script>
```

## 第三方UI库弹窗

### Element UI Dialog

**使用说明**：
在项目中使用了Element UI的Dialog组件，用于展示标准的模态对话框。

**基本用法**：

```vue
<template>
  <el-button @click="dialogVisible = true">打开对话框</el-button>
  
  <el-dialog
    v-model="dialogVisible"
    title="对话框标题"
    width="50%"
  >
    <span>对话框内容</span>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="dialogVisible = false">
          确定
        </el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script setup>
import { ref } from 'vue'

const dialogVisible = ref(false)
</script>
```

**样式定制**：
在项目中，对Element UI的Dialog组件样式进行了一些定制：

```css
:deep(.el-dialog) {
  border-radius: 8px;
  overflow: hidden;
}

:deep(.el-dialog__header) {
  padding: 15px 20px;
  border-bottom: 1px solid #eaeaea;
}

:deep(.el-dialog__body) {
  padding: 20px;
}
```

## 特定功能弹窗

### 分享结果模态框

**文件路径**：`frontend-nuxt/components/deep_dive_search_component/search_result_share_modal.vue`

**组件说明**：
用于展示和分享搜索结果的全屏模态框，支持Markdown内容和思维导图的预览、复制和下载。

**参数说明**：

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| title | String | - | 分享内容标题 |
| shareUrl | String | - | 分享链接 |
| markdownContent | String | - | Markdown格式的内容 |
| mindMapContent | String | - | 思维导图内容 |

**事件**：

| 事件名 | 说明 |
|--------|------|
| close | 关闭模态框时触发 |

**基本用法**：

```vue
<template>
  <button @click="showShareModal = true">分享结果</button>
  
  <search_result_share_modal
    v-if="showShareModal"
    :title="'搜索结果标题'"
    :markdown-content="markdownContent"
    :mind-map-content="mindMapData"
    @close="showShareModal = false"
  />
</template>

<script setup>
import { ref } from 'vue'
import search_result_share_modal from '/components/deep_dive_search_component/search_result_share_modal.vue'

const showShareModal = ref(false)
const markdownContent = ref('# 搜索结果\n这是示例Markdown内容')
const mindMapData = ref(null)
</script>
```

## 弹窗使用最佳实践

1. **选择合适的弹窗类型**
   - 简单确认操作使用 `ConfirmModal` 或 `GlobalDialog`（confirm模式）
   - 需要用户输入内容使用 `GlobalDialog`（input模式）
   - 侧边栏内容使用 `Drawer` 组件
   - 复杂内容展示使用 `Modal` 组件

2. **弹窗开关状态管理**
   - 优先使用 `v-model` 或 `v-model:visible` 绑定弹窗的开关状态
   - 确保在组件卸载时关闭所有打开的弹窗

3. **避免嵌套弹窗**
   - 尽量避免在一个弹窗内打开另一个弹窗
   - 如必须嵌套，确保正确管理z-index层级

4. **合理处理弹窗关闭逻辑**
   - 提供明确的关闭按钮
   - 对于非关键操作，支持点击遮罩层和ESC键关闭
   - 对于重要操作，考虑禁用点击遮罩层关闭功能

5. **性能优化**
   - 对于复杂内容的弹窗，考虑使用懒加载或动态导入
   - 弹窗内的表单提交等操作应防止重复提交

6. **移动端适配**
   - 确保弹窗在移动设备上有合适的尺寸和交互体验
   - 考虑使用全屏模式或底部弹出的弹窗样式

## 样式规范统一建议

经过对项目中各类弹窗的分析，建议统一以下样式规范：

1. **样式一致性**
   - 统一弹窗圆角：8px
   - 统一标题字体大小：18px
   - 统一内容区域内边距：20px
   - 统一遮罩层透明度：rgba(0, 0, 0, 0.5)
   - 统一关闭按钮位置：右上角

2. **动画效果**
   - 统一使用缩放渐入/渐出动画
   - 动画持续时间：0.25s
   - 使用cubic-bezier曲线获得更平滑的效果

3. **响应式设计**
   - 桌面端：弹窗宽度不超过屏幕的80%，最大宽度800px
   - 移动端：弹窗宽度为屏幕宽度的90%，小屏幕下考虑全屏弹窗

4. **按钮设计**
   - 主操作按钮（确认、提交）使用主题色
   - 次要操作按钮（取消）使用灰色背景
   - 危险操作按钮（删除）使用红色警示
   - 按钮大小和内边距保持一致

5. **组件复用**
   - 优先使用基础弹窗组件（Modal、Drawer、GlobalDialog）
   - 避免创建重复功能的新弹窗组件
   - 提取共用的样式到全局样式文件中

通过统一这些规范，可以提高用户体验的一致性，并简化开发和维护工作。 
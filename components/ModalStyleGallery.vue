<template>
  <div class="modal-gallery">
    <div class="gallery-header">
      <h1>Genspark 弹窗样式集合</h1>
      <div class="filter-tabs">
        <div class="filter-group">
          <div class="filter-label">按功能分类:</div>
          <div class="filter-options">
            <button
              v-for="type in functionTypes"
              :key="type.value"
              :class="{ active: activeFunction === type.value }"
              @click="activeFunction = type.value"
            >
              {{ type.label }}
            </button>
            <button
              :class="{ active: activeFunction === 'all' }"
              @click="activeFunction = 'all'"
            >
              全部
            </button>
          </div>
        </div>
        <div class="filter-group">
          <div class="filter-label">按技术实现:</div>
          <div class="filter-options">
            <button
              v-for="type in techTypes"
              :key="type.value"
              :class="{ active: activeTech === type.value }"
              @click="activeTech = type.value"
            >
              {{ type.label }}
            </button>
            <button
              :class="{ active: activeTech === 'all' }"
              @click="activeTech = 'all'"
            >
              全部
            </button>
          </div>
        </div>
        <div class="filter-group">
          <div class="filter-label">按样式特点:</div>
          <div class="filter-options">
            <button
              v-for="type in styleTypes"
              :key="type.value"
              :class="{ active: activeStyle === type.value }"
              @click="activeStyle = type.value"
            >
              {{ type.label }}
            </button>
            <button
              :class="{ active: activeStyle === 'all' }"
              @click="activeStyle = 'all'"
            >
              全部
            </button>
          </div>
        </div>
      </div>
      <div class="search-bar">
        <input
          type="text"
          v-model="searchQuery"
          placeholder="搜索弹窗组件..."
          @input="handleSearch"
        />
      </div>
    </div>

    <div class="gallery-grid">
      <div class="style-card" v-for="modal in filteredModals" :key="modal.id">
        <div class="preview-area">
          <div class="preview-heading">
            <h3>{{ modal.name }}</h3>
            <button class="preview-btn" @click="showPreview(modal)">
              预览
            </button>
          </div>
          <div class="preview-image">
            <img
              v-if="modal.previewImage"
              :src="modal.previewImage"
              alt="预览图"
            />
            <div v-else class="placeholder-preview">
              <span>{{ modal.previewPlaceholder || '点击上方按钮预览' }}</span>
            </div>
          </div>
        </div>
        <div class="info-area">
          <div class="tags">
            <span class="tag function-tag">{{
              getFunctionLabel(modal.functionType)
            }}</span>
            <span class="tag tech-tag">{{ getTechLabel(modal.techType) }}</span>
            <span class="tag style-tag">{{
              getStyleLabel(modal.styleType)
            }}</span>
          </div>
          <div class="code-preview">
            <div class="code-header">
              <span>组件路径: {{ modal.filePath }}</span>
              <button class="copy-btn" @click="copyCode(modal.code)">
                复制代码
              </button>
            </div>
            <pre><code>{{ modal.codePreview }}</code></pre>
          </div>
          <div class="usage-info">
            <h4>使用说明</h4>
            <p>{{ modal.usage }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- 预览弹窗 -->
    <div v-if="previewModal" class="preview-modal-container">
      <div class="preview-modal-backdrop" @click="closePreview"></div>
      <div class="preview-modal">
        <div class="preview-modal-header">
          <h3>{{ activePreviewModal.name }} 预览</h3>
          <button class="close-preview-btn" @click="closePreview">×</button>
        </div>
        <div class="preview-modal-content">
          <component
            :is="activePreviewModal.component"
            v-if="activePreviewModal.component"
            v-bind="activePreviewModal.props || {}"
          />
          <div v-else class="preview-placeholder">
            <div
              class="placeholder-modal"
              :class="activePreviewModal.styleType"
            >
              <div class="placeholder-header">
                <h4>{{ activePreviewModal.name }}</h4>
                <span class="placeholder-close">×</span>
              </div>
              <div class="placeholder-body">
                <p>示例内容区域</p>
              </div>
              <div class="placeholder-footer">
                <button class="placeholder-btn cancel">取消</button>
                <button class="placeholder-btn confirm">确定</button>
              </div>
            </div>
          </div>
        </div>
        <div class="preview-modal-footer">
          <button @click="closePreview">关闭预览</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref, computed, onMounted } from 'vue'

  // 分类数据
  const functionTypes = [
    { value: 'confirm', label: '确认类弹窗' },
    { value: 'form', label: '表单类弹窗' },
    { value: 'display', label: '展示类弹窗' },
    { value: 'selection', label: '选择类弹窗' },
    { value: 'custom', label: '自定义功能弹窗' },
  ]

  const techTypes = [
    { value: 'ui-library', label: '第三方UI库' },
    { value: 'custom', label: '自定义组件' },
    { value: 'native', label: '原生HTML弹窗' },
  ]

  const styleTypes = [
    { value: 'center', label: '居中弹窗' },
    { value: 'drawer', label: '抽屉式弹窗' },
    { value: 'fullscreen', label: '全屏弹窗' },
    { value: 'bottom', label: '底部弹出' },
    { value: 'tooltip', label: '气泡提示' },
  ]

  // 状态变量
  const activeFunction = ref('all')
  const activeTech = ref('all')
  const activeStyle = ref('all')
  const searchQuery = ref('')
  const previewModal = ref(false)
  const activePreviewModal = ref(null)

  // 弹窗数据
  const modalList = ref([
    {
      id: 1,
      name: 'Modal 模态框',
      functionType: 'custom',
      techType: 'custom',
      styleType: 'center',
      filePath: 'frontend-nuxt/ppt/components/Modal.vue',
      codePreview: `<template>
  <Modal v-model:visible="showModal" :width="500" closeButton>
    <div class="modal-example">
      <h2>模态框标题</h2>
      <p>这是一个居中显示的模态框示例</p>
      <div class="actions">
        <button @click="showModal = false">关闭</button>
      </div>
    </div>
  </Modal>
</template>`,
      code:
        `<template>
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

<scr` +
        `ipt setup>
import { ref } from 'vue'
import Modal from '/ppt/components/Modal.vue'

const showModal = ref(false)
</scr` +
        `ipt>`,
      usage:
        '通用模态框组件，使用Teleport实现，支持自定义宽度、动画效果和键盘esc关闭等功能。',
    },
    {
      id: 2,
      name: 'Drawer 抽屉',
      functionType: 'custom',
      techType: 'custom',
      styleType: 'drawer',
      filePath: 'frontend-nuxt/ppt/components/Drawer.vue',
      codePreview: `<template>
  <Drawer v-model:visible="showDrawer" :width="320" placement="right">
    <template #title>
      <span>抽屉标题</span>
    </template>
    <div class="drawer-content">
      <p>这是右侧抽屉内容</p>
    </div>
  </Drawer>
</template>`,
      code:
        `<template>
  <Drawer v-model:visible="showDrawer" :width="320" placement="right">
    <template #title>
      <span>抽屉标题</span>
    </template>
    <div class="drawer-content">
      <p>这是右侧抽屉内容</p>
    </div>
  </Drawer>
</template>

<scr` +
        `ipt setup>
import { ref } from 'vue'
import Drawer from '/ppt/components/Drawer.vue'

const showDrawer = ref(false)
</scr` +
        `ipt>`,
      usage:
        '侧边抽屉组件，支持左右方向，可自定义宽度，适用于侧边菜单、表单和详情展示等场景。',
    },
    {
      id: 3,
      name: 'GlobalDialog 全局对话框',
      functionType: 'confirm',
      techType: 'custom',
      styleType: 'center',
      filePath: 'frontend-nuxt/components/GlobalDialog.vue',
      codePreview: `<template>
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
</template>`,
      code:
        `<template>
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

<scr` +
        `ipt setup>
import { ref } from 'vue'
import GlobalDialog from '/components/GlobalDialog.vue'

const showDialog = ref(false)

const handleConfirm = () => {
  console.log('用户点击确认')
}

const handleCancel = () => {
  console.log('用户点击取消')
}
</scr` +
        `ipt>`,
      usage:
        '全局对话框组件，支持确认模式和输入模式，可自定义标题、内容、按钮文本等。',
    },
    {
      id: 4,
      name: 'ConfirmModal 确认框',
      functionType: 'confirm',
      techType: 'custom',
      styleType: 'center',
      filePath: 'admin-nuxt/components/fashion_cms/ConfirmModal.vue',
      codePreview: `<template>
  <ConfirmModal
    :show="showConfirm"
    title="删除确认"
    message="确定要删除这个项目吗？此操作不可撤销。"
    confirmText="删除"
    cancelText="取消"
    @confirm="handleConfirm"
    @cancel="showConfirm = false"
  />
</template>`,
      code:
        `<template>
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

<scr` +
        `ipt setup>
import { ref } from 'vue'
import ConfirmModal from '/components/fashion_cms/ConfirmModal.vue'

const showConfirm = ref(false)

const handleConfirm = () => {
  console.log('用户确认删除')
  showConfirm.value = false
}
</scr` +
        `ipt>`,
      usage: '简单的确认对话框，适用于需要用户确认的操作，如删除、提交等。',
    },
    {
      id: 5,
      name: '分享结果模态框',
      functionType: 'display',
      techType: 'custom',
      styleType: 'fullscreen',
      filePath:
        'frontend-nuxt/components/deep_dive_search_component/search_result_share_modal.vue',
      codePreview: `<template>
  <search_result_share_modal
    :title="'搜索结果标题'"
    :markdown-content="markdownContent"
    :mind-map-content="mindMapData"
    @close="closeShareModal"
  />
</template>`,
      code:
        `<template>
  <search_result_share_modal
    :title="'搜索结果标题'"
    :markdown-content="markdownContent"
    :mind-map-content="mindMapData"
    @close="closeShareModal"
  />
</template>

<scr` +
        `ipt setup>
import { ref } from 'vue'
import search_result_share_modal from '/components/deep_dive_search_component/search_result_share_modal.vue'

const markdownContent = ref('# 搜索结果\\n这是示例Markdown内容')
const mindMapData = ref(null)

const closeShareModal = () => {
  console.log('关闭分享模态框')
}
</scr` +
        `ipt>`,
      usage:
        '用于展示和分享搜索结果的全屏模态框，支持Markdown内容和思维导图的预览、复制和下载。',
    },
    {
      id: 6,
      name: 'Element UI Dialog',
      functionType: 'display',
      techType: 'ui-library',
      styleType: 'center',
      filePath: 'admin-nuxt/components/icon-manager/views/Home.vue',
      codePreview: `<template>
  <el-dialog
    v-model="dialogVisible"
    title="图标详情"
    width="50%"
    class="icon-detail-dialog"
  >
    <div class="dialog-content">
      <!-- 对话框内容区域 -->
    </div>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="confirmDialog">
          确定
        </el-button>
      </span>
    </template>
  </el-dialog>
</template>`,
      code:
        `<template>
  <el-dialog
    v-model="dialogVisible"
    title="图标详情"
    width="50%"
    class="icon-detail-dialog"
  >
    <div class="dialog-content">
      <!-- 对话框内容区域 -->
    </div>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="confirmDialog">
          确定
        </el-button>
      </span>
    </template>
  </el-dialog>
</template>

<scr` +
        `ipt setup>
import { ref } from 'vue'

const dialogVisible = ref(false)

const confirmDialog = () => {
  console.log('用户确认对话框')
  dialogVisible.value = false
}
</scr` +
        `ipt>`,
      usage:
        'Element UI的对话框组件，提供标准的居中显示弹窗，支持自定义标题、内容和底部按钮区域。',
    },
  ])

  // 过滤处理
  const filteredModals = computed(() => {
    return modalList.value.filter(modal => {
      const functionMatch =
        activeFunction.value === 'all' ||
        modal.functionType === activeFunction.value
      const techMatch =
        activeTech.value === 'all' || modal.techType === activeTech.value
      const styleMatch =
        activeStyle.value === 'all' || modal.styleType === activeStyle.value
      const searchMatch =
        !searchQuery.value ||
        modal.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        modal.filePath.toLowerCase().includes(searchQuery.value.toLowerCase())

      return functionMatch && techMatch && styleMatch && searchMatch
    })
  })

  // 获取标签文本
  const getFunctionLabel = value => {
    const type = functionTypes.find(t => t.value === value)
    return type ? type.label : value
  }

  const getTechLabel = value => {
    const type = techTypes.find(t => t.value === value)
    return type ? type.label : value
  }

  const getStyleLabel = value => {
    const type = styleTypes.find(t => t.value === value)
    return type ? type.label : value
  }

  // 处理搜索
  const handleSearch = () => {
    // 实时搜索，不需要额外处理，依赖computed实现
  }

  // 展示预览
  const showPreview = modal => {
    activePreviewModal.value = modal
    previewModal.value = true
  }

  // 关闭预览
  const closePreview = () => {
    previewModal.value = false
    activePreviewModal.value = null
  }

  // 复制代码
  const copyCode = async code => {
    try {
      await navigator.clipboard.writeText(code)
      alert('代码已复制到剪贴板')
    } catch (err) {
      console.error('复制失败:', err)
    }
  }
</script>

<style scoped>
  .modal-gallery {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial,
      sans-serif;
  }

  .gallery-header {
    margin-bottom: 30px;
  }

  .gallery-header h1 {
    font-size: 24px;
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 1px solid #eaeaea;
  }

  .filter-tabs {
    margin-bottom: 20px;
  }

  .filter-group {
    margin-bottom: 15px;
  }

  .filter-label {
    font-weight: 600;
    margin-bottom: 8px;
  }

  .filter-options {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .filter-options button {
    padding: 6px 12px;
    border: 1px solid #ddd;
    border-radius: 4px;
    background: #f5f5f5;
    cursor: pointer;
    font-size: 14px;
    transition: all 0.2s;
  }

  .filter-options button:hover {
    background: #eaeaea;
  }

  .filter-options button.active {
    background: #2196f3;
    color: white;
    border-color: #2196f3;
  }

  .search-bar {
    margin: 20px 0;
  }

  .search-bar input {
    width: 100%;
    padding: 10px 15px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 16px;
  }

  .gallery-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(500px, 1fr));
    gap: 20px;
  }

  .style-card {
    border: 1px solid #eaeaea;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
    background: white;
  }

  .preview-area {
    padding: 15px;
    border-bottom: 1px solid #eaeaea;
  }

  .preview-heading {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }

  .preview-heading h3 {
    margin: 0;
    font-size: 18px;
  }

  .preview-btn {
    padding: 6px 12px;
    background: #4caf50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
  }

  .preview-image {
    height: 150px;
    background: #f5f5f7;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 4px;
  }

  .preview-image img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }

  .placeholder-preview {
    color: #888;
    text-align: center;
  }

  .info-area {
    padding: 15px;
  }

  .tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 10px;
  }

  .tag {
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 12px;
    font-weight: 600;
  }

  .function-tag {
    background: #e3f2fd;
    color: #1976d2;
  }

  .tech-tag {
    background: #e8f5e9;
    color: #2e7d32;
  }

  .style-tag {
    background: #fff3e0;
    color: #e65100;
  }

  .code-preview {
    background: #f5f5f7;
    border-radius: 4px;
    margin: 15px 0;
  }

  .code-header {
    display: flex;
    justify-content: space-between;
    padding: 8px 12px;
    background: #eaeaea;
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
    font-size: 14px;
    color: #333;
  }

  .copy-btn {
    background: transparent;
    border: none;
    color: #2196f3;
    cursor: pointer;
    font-size: 14px;
  }

  .code-preview pre {
    margin: 0;
    padding: 12px;
    overflow-x: auto;
    font-family: 'Fira Code', monospace;
    font-size: 14px;
    line-height: 1.5;
    color: #333;
  }

  .usage-info h4 {
    margin-top: 0;
    margin-bottom: 8px;
    font-size: 16px;
  }

  .usage-info p {
    margin: 0;
    color: #555;
    line-height: 1.5;
  }

  /* 预览弹窗样式 */
  .preview-modal-container {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 9999;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .preview-modal-backdrop {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
  }

  .preview-modal {
    position: relative;
    background: white;
    width: 80%;
    max-width: 800px;
    max-height: 80vh;
    border-radius: 8px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .preview-modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 20px;
    border-bottom: 1px solid #eaeaea;
  }

  .preview-modal-header h3 {
    margin: 0;
    font-size: 18px;
  }

  .close-preview-btn {
    background: none;
    border: none;
    font-size: 24px;
    cursor: pointer;
    color: #888;
  }

  .preview-modal-content {
    flex: 1;
    overflow: auto;
    padding: 20px;
  }

  .preview-placeholder {
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .placeholder-modal {
    width: 400px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
    overflow: hidden;
  }

  .placeholder-modal.drawer {
    width: 300px;
    height: 100%;
    position: absolute;
    top: 0;
    right: 0;
    border-radius: 0;
  }

  .placeholder-modal.fullscreen {
    width: 100%;
    height: 100%;
    border-radius: 0;
  }

  .placeholder-modal.bottom {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    border-radius: 8px 8px 0 0;
  }

  .placeholder-header {
    display: flex;
    justify-content: space-between;
    padding: 12px 15px;
    border-bottom: 1px solid #eaeaea;
  }

  .placeholder-header h4 {
    margin: 0;
    font-size: 16px;
  }

  .placeholder-close {
    font-size: 18px;
    cursor: pointer;
    color: #888;
  }

  .placeholder-body {
    padding: 15px;
    min-height: 100px;
  }

  .placeholder-footer {
    display: flex;
    justify-content: flex-end;
    padding: 12px 15px;
    border-top: 1px solid #eaeaea;
    gap: 10px;
  }

  .placeholder-btn {
    padding: 6px 12px;
    border-radius: 4px;
    font-size: 14px;
    cursor: pointer;
    border: none;
  }

  .placeholder-btn.cancel {
    background: #f5f5f5;
    color: #333;
  }

  .placeholder-btn.confirm {
    background: #2196f3;
    color: white;
  }

  .preview-modal-footer {
    padding: 15px 20px;
    border-top: 1px solid #eaeaea;
    display: flex;
    justify-content: flex-end;
  }

  .preview-modal-footer button {
    padding: 8px 16px;
    background: #f5f5f5;
    border: 1px solid #ddd;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
  }
</style>

# GenSpark UI Design System - Complete Rules

## 概述
此文档定义了 GenSpark 项目的完整 UI 设计系统规范，包括按钮组件和弹窗组件的设计标准。

## 颜色系统

### 主色调
```css
--color-primary: #232425;           /* 主按钮背景色 */
--color-primary-hover: #393A3B;     /* 主按钮悬停态 */
```

### 引导色
```css
--color-guide: #0F7FFF;             /* 强引导按钮背景色 */
--color-guide-hover: #0E72E5;       /* 强引导按钮悬停态 */
```

### 次要色
```css
--color-secondary: #F5F5F5;         /* 弱按钮背景色 */
--color-secondary-hover: #E9E9E9;   /* 弱按钮悬停态 */
```

### 边框色
```css
--color-border: #E2E2E2;            /* 线型按钮边框色 */
--color-border-light: #F0F0F0;      /* 弱按钮边框色 */
```

### 功能色
```css
--color-danger: #EF4444;            /* 危险操作按钮 */
--color-warning: #F59E0B;           /* 警告色 */
--color-success: #10B981;           /* 成功色 */
--color-warning-bg: #FFFBEE;        /* 警告背景色 */
```

## 按钮设计系统

### 按钮类型规范

#### 1. 主按钮（大圆角）
**使用场景**: 引导点击、常规入口、自然轻松的操作
**特征**: 30px 圆角，自然亲和的视觉效果

```css
.btn-primary-large {
  background: var(--color-primary);
  color: white;
  border: none;
  border-radius: 30px;
  transition: all 0.25s ease;
}

.btn-primary-large:hover {
  background: var(--color-primary-hover);
  box-shadow: 0 2px 8px rgba(35, 36, 37, 0.15);
}
```

#### 2. 主按钮（小圆角）
**使用场景**: 功能操作、弹窗确认、强操作类、严肃谨慎的场景
**特征**: 8px 圆角，功能性和严肃感

```css
.btn-primary-small {
  background: var(--color-primary);
  color: white;
  border: none;
  border-radius: 8px;
  transition: all 0.25s ease;
}
```

#### 3. 强引导按钮
**使用场景**: 重要功能引导、转化关键节点
**特征**: 蓝色背景，30px 圆角

```css
.btn-guide {
  background: var(--color-guide);
  color: white;
  border: none;
  border-radius: 30px;
  transition: all 0.25s ease;
}
```

#### 4. 线型按钮
**使用场景**: 次要操作、取消操作、边界明确的功能
**特征**: 透明背景，边框样式

```css
.btn-outline {
  background: transparent;
  color: var(--color-primary);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  transition: all 0.25s ease;
}
```

#### 5. 弱按钮
**使用场景**: 辅助功能、设置选项、状态切换
**特征**: 浅灰背景，12px 圆角

```css
.btn-secondary {
  background: var(--color-secondary);
  color: var(--color-primary);
  border: 1px solid var(--color-border-light);
  border-radius: 12px;
  transition: all 0.25s ease;
}
```

#### 6. 危险按钮
**使用场景**: 删除、重置等破坏性操作
**特征**: 红色背景，明确的警示性

```css
.btn-danger {
  background: var(--color-danger);
  color: white;
  border: none;
  border-radius: 8px;
  transition: all 0.25s ease;
}
```

### 按钮尺寸规范

#### 大按钮
```css
.btn-large {
  width: 208px;
  height: 40px;
  font-size: 16px;
  padding: 0 20px;
}
```

#### 中按钮
```css
.btn-medium {
  width: 144px;
  height: 36px;
  font-size: 16px;
  padding: 0 16px;
}
```

#### 小按钮
```css
.btn-small {
  width: 96px;
  height: 28px;
  font-size: 16px;
  padding: 0 12px;
}
```

## 弹窗设计系统

### 弹窗类型规范

#### 1. 确认弹窗 (Confirmation Modal)
**使用场景**: 删除确认、重要决策确认
**尺寸**: 小型 (300-400px)
**按钮组合**: 线型按钮（取消）+ 主按钮小圆角（确认）

```html
<div class="modal-overlay">
  <div class="modal-dialog" style="width: 400px;">
    <div class="modal-header">
      <h2>确认删除</h2>
      <button class="close-btn">×</button>
    </div>
    <div class="modal-body">
      <div class="warning-icon">⚠️</div>
      <p>此操作不可撤销，确定要删除吗？</p>
    </div>
    <div class="modal-footer">
      <button class="btn-base btn-outline btn-medium">取消</button>
      <button class="btn-base btn-primary-small btn-medium">确认删除</button>
    </div>
  </div>
</div>
```

#### 2. 表单弹窗 (Form Modal)
**使用场景**: 数据录入、设置配置、个人化设置
**尺寸**: 中型 (450-600px)
**按钮组合**: 线型按钮（取消）+ 主按钮大圆角（提交）

```html
<div class="modal-overlay">
  <div class="modal-dialog" style="width: 500px;">
    <div class="modal-header">
      <h2>编辑个人资料</h2>
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

#### 3. 通知弹窗 (Notification Modal)
**使用场景**: 系统通知、功能更新、促销信息
**尺寸**: 小-中型 (350-500px)
**按钮组合**: 主按钮大圆角（主要操作）或弱按钮（关闭）

```html
<div class="modal-overlay">
  <div class="modal-dialog" style="width: 450px;">
    <div class="modal-header">
      <h2>🎉 新功能发布</h2>
      <button class="close-btn">×</button>
    </div>
    <div class="modal-body">
      <p>我们为您带来了全新的功能体验！</p>
    </div>
    <div class="modal-footer">
      <button class="btn-base btn-secondary btn-medium">稍后查看</button>
      <button class="btn-base btn-guide btn-medium">立即体验</button>
    </div>
  </div>
</div>
```

#### 4. 预览弹窗 (Preview Modal)
**使用场景**: 图片预览、内容预览、详细信息查看
**尺寸**: 大型 (600-800px)
**按钮组合**: 弱按钮（关闭）+ 可选的主要操作按钮

```html
<div class="modal-overlay">
  <div class="modal-dialog" style="width: 600px;">
    <div class="modal-header">
      <h2>图片预览</h2>
      <button class="close-btn">×</button>
    </div>
    <div class="modal-body">
      <img src="preview.jpg" style="width: 100%;" />
    </div>
    <div class="modal-footer">
      <button class="btn-base btn-secondary btn-medium">关闭</button>
      <button class="btn-base btn-primary-large btn-medium">下载</button>
    </div>
  </div>
</div>
```

#### 5. 设置弹窗 (Settings Modal)
**使用场景**: 系统配置、偏好设置、复杂表单
**尺寸**: 中-大型 (500-700px)
**按钮组合**: 线型按钮（取消）+ 主按钮小圆角（保存）

### 弹窗尺寸规范

```css
/* 小型弹窗 */
.modal-small {
  width: 300px;
  max-width: 400px;
  max-height: 400px;
}

/* 中型弹窗 */
.modal-medium {
  width: 500px;
  max-width: 600px;
  max-height: 600px;
}

/* 大型弹窗 */
.modal-large {
  width: 700px;
  max-width: 800px;
  max-height: 90vh;
}
```

### 弹窗基础结构

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
}

.modal-dialog {
  background: white;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  padding: 24px;
  transform: scale(0.9) translateY(20px);
  transition: all 0.3s ease;
  max-width: 90vw;
  max-height: 90vh;
  overflow-y: auto;
}

.modal-overlay.active {
  opacity: 1;
  visibility: visible;
}

.modal-overlay.active .modal-dialog {
  transform: scale(1) translateY(0);
}
```

## 设计规范

### 圆角规范

- **大圆角 (30px)**: 自然、轻松、亲和 - 用于主按钮（大圆角）、强引导按钮
- **中圆角 (16px)**: 标准、平衡 - 用于弹窗、卡片
- **小圆角 (12px)**: 功能性、平衡 - 用于线型按钮、弱按钮
- **紧凑圆角 (8px)**: 严肃、紧凑 - 用于主按钮（小圆角）、危险按钮

### 间距规范

- **弹窗内部间距**: 24px
- **区块间距**: 16px
- **按钮间距**: 12px
- **表单元素间距**: 8px

### 弹窗按钮圆角一致性规则

**重要**: 当弹窗包含两个按钮时，两个按钮必须使用相同的圆角半径以保持视觉一致性：

- **确认弹窗**: 两个按钮都使用 8px 圆角（严肃/紧凑感）
- **表单弹窗**: 两个按钮都使用 12px 圆角（功能一致性）
- **通知弹窗**: 两个按钮都使用 12px 圆角（平衡外观）
- **预览弹窗**: 两个按钮都使用 12px 圆角（功能一致性）
- **设置弹窗**: 两个按钮都使用 12px 圆角（功能一致性）

### 阴影规范

```css
/* 按钮悬停阴影 */
box-shadow: 0 2px 8px rgba(35, 36, 37, 0.15);

/* 弹窗阴影 */
box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);

/* 卡片阴影 */
box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
```

## 组合使用规范

### 弹窗 + 按钮组合规则

1. **确认对话框**: 线型按钮-8px（取消）+ 主按钮-8px（确认）- 两个按钮都使用 8px 圆角
2. **表单提交**: 线型按钮-12px（取消）+ 主按钮-12px（提交）- 两个按钮都使用 12px 圆角  
3. **功能引导**: 线型按钮-12px（跳过）+ 强引导按钮-12px（继续）- 两个按钮都使用 12px 圆角
4. **设置/偏好**: 线型按钮-12px（取消）+ 主按钮-12px（保存）- 两个按钮都使用 12px 圆角
5. **危险操作**: 线型按钮-8px（取消）+ 危险按钮-8px（删除）- 两个按钮都使用 8px 圆角

**关键规则**: 弹窗中的两个按钮必须具有相同的圆角半径以保持视觉一致性。

### 层级规则

1. 每个弹窗只能有一个主按钮
2. 强引导按钮谨慎使用，用于关键转化点
3. 保持清晰的视觉层级
4. 一致的间距和对齐

## 无障碍要求

### 弹窗无障碍

1. 弹窗必须捕获焦点并在关闭时返回触发元素
2. ESC 键关闭弹窗
3. 点击外部区域关闭弹窗（除非是关键操作）
4. 正确的 ARIA 标签和角色
5. 支持屏幕阅读器

### 按钮无障碍

1. 最小触摸区域 44x44px
2. 颜色对比度至少 4.5:1
3. 支持键盘导航
4. 提供明确的 aria-label

## React/Vue 组件接口

### 弹窗组件接口

```typescript
interface ModalProps {
  type: 'confirmation' | 'form' | 'notification' | 'preview' | 'settings';
  size: 'small' | 'medium' | 'large';
  show: boolean;
  onClose: () => void;
  title: string;
  children: React.ReactNode;
  footer?: React.ReactNode;
  closeOnOutsideClick?: boolean;
  closeOnEsc?: boolean;
  danger?: boolean; // 用于确认危险操作
}
```

### 按钮组件接口

```typescript
interface ButtonProps {
  variant: 'primary-large' | 'primary-small' | 'guide' | 'outline' | 'secondary' | 'danger';
  size: 'large' | 'medium' | 'small';
  disabled?: boolean;
  loading?: boolean;
  icon?: React.ReactNode;
  children: React.ReactNode;
  onClick?: () => void;
  'aria-label'?: string;
}
```

## 实现示例

### React 弹窗组件

```tsx
const Modal: React.FC<ModalProps> = ({
  type,
  size,
  show,
  onClose,
  title,
  children,
  footer,
  closeOnOutsideClick = true,
  closeOnEsc = true,
  danger = false
}) => {
  const modalRef = useRef<HTMLDivElement>(null);
  
  useEffect(() => {
    if (show) {
      modalRef.current?.focus();
    }
  }, [show]);
  
  useEffect(() => {
    const handleEsc = (e: KeyboardEvent) => {
      if (closeOnEsc && e.key === 'Escape') {
        onClose();
      }
    };
    
    if (show) {
      document.addEventListener('keydown', handleEsc);
      document.body.style.overflow = 'hidden';
    }
    
    return () => {
      document.removeEventListener('keydown', handleEsc);
      document.body.style.overflow = 'auto';
    };
  }, [show, closeOnEsc, onClose]);
  
  if (!show) return null;
  
  return (
    <div 
      className={`modal-overlay ${show ? 'active' : ''}`}
      onClick={(e) => {
        if (closeOnOutsideClick && e.target === e.currentTarget) {
          onClose();
        }
      }}
    >
      <div 
        ref={modalRef}
        className={`modal-dialog modal-${size}`}
        role="dialog"
        aria-labelledby="modal-title"
        tabIndex={-1}
      >
        <div className="modal-header">
          <h2 id="modal-title" className="modal-title">
            {danger && <span className="danger-icon">⚠️</span>}
            {title}
          </h2>
          <button 
            className="close-btn" 
            onClick={onClose}
            aria-label="关闭弹窗"
          >
            ×
          </button>
        </div>
        <div className="modal-body">
          {children}
        </div>
        {footer && (
          <div className="modal-footer">
            {footer}
          </div>
        )}
      </div>
    </div>
  );
};
```

### Vue 弹窗组件

```vue
<template>
  <teleport to="body">
    <div 
      v-if="show"
      :class="['modal-overlay', { active: show }]"
      @click="handleOutsideClick"
    >
      <div 
        ref="modalRef"
        :class="['modal-dialog', `modal-${size}`]"
        role="dialog"
        :aria-labelledby="titleId"
        tabindex="-1"
      >
        <div class="modal-header">
          <h2 :id="titleId" class="modal-title">
            <span v-if="danger" class="danger-icon">⚠️</span>
            {{ title }}
          </h2>
          <button 
            class="close-btn" 
            @click="$emit('close')"
            aria-label="关闭弹窗"
          >
            ×
          </button>
        </div>
        <div class="modal-body">
          <slot></slot>
        </div>
        <div v-if="$slots.footer" class="modal-footer">
          <slot name="footer"></slot>
        </div>
      </div>
    </div>
  </teleport>
</template>

<script setup lang="ts">
interface Props {
  type: 'confirmation' | 'form' | 'notification' | 'preview' | 'settings';
  size: 'small' | 'medium' | 'large';
  show: boolean;
  title: string;
  closeOnOutsideClick?: boolean;
  closeOnEsc?: boolean;
  danger?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  closeOnOutsideClick: true,
  closeOnEsc: true,
  danger: false
});

const emit = defineEmits<{
  close: [];
}>();
</script>
```

## 质量检查清单

### 弹窗组件检查

- [ ] 使用了正确的弹窗类型和尺寸
- [ ] 实现了正确的按钮组合
- [ ] 包含了完整的无障碍支持
- [ ] 支持键盘导航和焦点管理
- [ ] 实现了正确的动画效果
- [ ] 遵循了设计系统的视觉规范

### 按钮组件检查

- [ ] 使用了正确的按钮类型
- [ ] 应用了合适的尺寸和圆角规范
- [ ] 实现了完整的状态（normal, hover, disabled, loading）
- [ ] 符合颜色系统要求
- [ ] 满足无障碍要求

---

**注意**: 此设计系统基于 GenSpark 项目的实际需求制定，弹窗和按钮组件应协调工作，确保整体的用户体验一致性。 
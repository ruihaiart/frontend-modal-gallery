# GenSpark Button Design System - User Rules

## 概述
此文档定义了 GenSpark 项目的按钮设计系统规范，用于指导所有按钮组件的开发和实现。

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
--color-warning-bg: #FFFBEE;        /* 警告背景色 */
```

## 按钮类型规范

### 1. 主按钮（大圆角）
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

.btn-primary-large:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}
```

### 2. 主按钮（小圆角）
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

### 3. 强引导按钮（引导功能类）
**使用场景**: 重要功能引导、转化关键节点
**特征**: 蓝色背景，30px 圆角

```css
.btn-guide-primary {
  background: var(--color-guide);
  color: white;
  border: none;
  border-radius: 30px;
  transition: all 0.25s ease;
}

.btn-guide-primary:hover {
  background: var(--color-guide-hover);
  box-shadow: 0 2px 8px rgba(15, 127, 255, 0.15);
}
```

### 4. 强引导按钮（小圆角）
**使用场景**: 表单提交、重要确认操作
**特征**: 蓝色背景，8px 圆角

```css
.btn-guide-small {
  background: var(--color-guide);
  color: white;
  border: none;
  border-radius: 8px;
  transition: all 0.25s ease;
}
```

### 5. 线型按钮
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

.btn-outline:hover {
  background: var(--color-primary);
  color: white;
  border-color: var(--color-primary);
}
```

### 6. 弱按钮
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

.btn-secondary:hover {
  background: var(--color-secondary-hover);
  border-color: var(--color-border);
}
```

## 尺寸规范

### 大按钮
```css
.btn-large {
  width: 208px;
  height: 40px;
  font-size: 16px;
  padding: 0 20px;
}
```
**使用场景**: 主要操作、重要功能入口

### 中按钮
```css
.btn-medium {
  width: 144px;
  height: 36px;
  font-size: 16px;
  padding: 0 16px;
}
```
**使用场景**: 常规操作、对话框按钮

### 小按钮
```css
.btn-small {
  width: 96px;
  height: 28px;
  font-size: 16px;
  padding: 0 12px;
}
```
**使用场景**: 紧凑布局、表格操作

### 图标按钮
```css
.btn-icon {
  height: 40px;
  padding: 0 16px;
  width: auto;
  min-width: fit-content;
}
```
**使用场景**: 带图标的操作按钮

## 圆角规范

### 大圆角 (30px)
**特点**: 自然、轻松、亲和
**适用**: 主按钮（大圆角）、强引导按钮（引导功能类）

### 中圆角 (12px)
**特点**: 功能性、平衡
**适用**: 线型按钮、弱按钮

### 小圆角 (8px)
**特点**: 严肃、谨慎、功能导向
**适用**: 主按钮（小圆角）、强引导按钮（小圆角）

## 状态规范

### Normal 状态
按钮的默认外观状态

### Hover 状态
```css
.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}
```

### Disabled 状态
```css
.btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
  pointer-events: none;
}
```

### Loading 状态
```css
.btn-loading {
  position: relative;
  color: transparent !important;
}

.btn-loading::after {
  content: '';
  position: absolute;
  width: 16px;
  height: 16px;
  border: 2px solid #ffffff;
  border-radius: 50%;
  border-top-color: transparent;
  animation: spin 1s ease-in-out infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

## 基础样式模板

```css
.btn-base {
  border: none;
  cursor: pointer;
  font-family: inherit;
  font-weight: 500;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  transition: all 0.25s ease;
  white-space: nowrap;
  text-decoration: none;
  outline: none;
  box-sizing: border-box;
}
```

## 使用指南

### 按钮选择决策树

1. **主要操作** → 主按钮（大圆角）
2. **重要功能引导** → 强引导按钮（引导功能类）
3. **表单提交/确认** → 主按钮（小圆角）或强引导按钮（小圆角）
4. **次要操作** → 线型按钮
5. **辅助功能** → 弱按钮

### 组合使用原则

1. 同一界面中主按钮不超过 1 个
2. 强引导按钮谨慎使用，避免过多
3. 按钮组合时保持视觉层次清晰
4. 相同操作级别使用相同样式

### 无障碍要求

1. 按钮文本对比度至少 4.5:1
2. 按钮最小点击区域 44x44px
3. 支持键盘导航
4. 提供明确的 aria-label

## 代码实现要求

### HTML 结构
```html
<!-- 主按钮 -->
<button class="btn-base btn-primary-large btn-large">
  确认提交
</button>

<!-- 带图标按钮 -->
<button class="btn-base btn-primary-large btn-icon">
  <span class="icon">+</span>
  添加任务
</button>
```

### React 组件示例
```tsx
interface ButtonProps {
  variant: 'primary-large' | 'primary-small' | 'guide-primary' | 'guide-small' | 'outline' | 'secondary';
  size: 'large' | 'medium' | 'small' | 'icon';
  disabled?: boolean;
  loading?: boolean;
  icon?: React.ReactNode;
  children: React.ReactNode;
  onClick?: () => void;
}

const Button: React.FC<ButtonProps> = ({
  variant,
  size,
  disabled,
  loading,
  icon,
  children,
  onClick
}) => {
  const className = `btn-base btn-${variant} btn-${size} ${loading ? 'btn-loading' : ''}`;
  
  return (
    <button
      className={className}
      disabled={disabled || loading}
      onClick={onClick}
    >
      {icon && <span className="icon">{icon}</span>}
      {children}
    </button>
  );
};
```

### Vue 组件示例
```vue
<template>
  <button
    :class="buttonClass"
    :disabled="disabled || loading"
    @click="handleClick"
  >
    <span v-if="icon" class="icon">
      <slot name="icon">{{ icon }}</slot>
    </span>
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    variant: {
      type: String,
      required: true,
      validator: (value) => [
        'primary-large', 'primary-small', 'guide-primary', 
        'guide-small', 'outline', 'secondary'
      ].includes(value)
    },
    size: {
      type: String,
      required: true,
      validator: (value) => ['large', 'medium', 'small', 'icon'].includes(value)
    },
    disabled: Boolean,
    loading: Boolean,
    icon: String
  },
  computed: {
    buttonClass() {
      return [
        'btn-base',
        `btn-${this.variant}`,
        `btn-${this.size}`,
        { 'btn-loading': this.loading }
      ];
    }
  },
  methods: {
    handleClick() {
      if (!this.disabled && !this.loading) {
        this.$emit('click');
      }
    }
  }
};
</script>
```

## 质量检查清单

- [ ] 使用了正确的按钮类型
- [ ] 应用了合适的尺寸规范
- [ ] 实现了完整的状态（normal, hover, disabled, loading）
- [ ] 遵循了圆角规范
- [ ] 符合颜色系统要求
- [ ] 满足无障碍要求
- [ ] 代码结构清晰，可维护性好

---

**注意**: 此设计系统基于 GenSpark 项目的实际需求制定，请严格遵循以确保界面一致性和用户体验。 
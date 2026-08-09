# Toast

> 全局浮窗消息提示 — **4 个 Status** × Imperative API。零配置、自动 mount Portal。

## 1. 总览

- **组件名**: `Toast` (imperative object, 非 React 组件)
- **用途**: 轻量级操作反馈, 不打断用户主流程
- **导入**:
  ```ts
  import { Toast } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Toast`
- **Figma**:
  - [Toast ComponentSet (1256:37)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1256-37) — 4 variants
  - [Display (1257:25)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1257-25)
- **Code Connect**: ✅ (`Toast.figma.tsx`)

**依据来源**:
- Tier 1: System Test ComponentSet `Toast` (1256:37)
- Tier 2: 旧规范 28:43168 — Toast (消息提醒) 精确视觉 + 行为
- 旧库 4131:1063 — 4 status 视觉参考

---

## 2. 4 个 Status (核心要先记住)

| Status | 颜色 | Icon | 业务示例 |
|---|---|---|---|
| `success` | 绿 `#30B566` | success-s | Operation saved · Order placed · Email sent |
| `error`   | 红 `#FF4742` | error-s | Save failed · Network error · Invalid input |
| `info`    | 蓝 `#2673DD` | information-s | Sync started · New version available |
| `warning` | 黄 `#EDA500` | notice-triangle-s | Approaching limit · Action required soon |

---

## 3. 决策树 (AI 必读)

```
需要反馈用户?
├─ 操作结果通知 (成功 / 失败 / 状态更新)?
│    └─ 用 Toast (轻量, 自动消失)
├─ 需要用户主动确认 / 必须看到?
│    └─ 用 Modal (打断, 需点击确认)
├─ 阻塞错误需要详细解释?
│    └─ 用 Modal 或 Alert (内联)
└─ 表单字段验证错误?
     └─ 用 Form 字段 inline error, 不用 Toast

Toast 选哪个 status?
├─ 成功? → success (绿)
├─ 失败 / 错误? → error (红)
├─ 中性消息 / 普通通知? → info (蓝)
└─ 需要用户注意但不阻断? → warning (黄)
```

---

## 4. API 完整签名

### `Toast.success(message, options?)` (& error/info/warning)

| 参数 | 类型 | 说明 |
|---|---|---|
| `message` | `ReactNode` | 提示文本/节点 |
| `options.duration` | `number?` | 消失时长 (ms), 默认 `3000`, 传 `0` = 不自动消失 |

**返回**: `string` — toast id, 可用于 `Toast.dismiss(id)` 手动关闭

### `Toast.show({ status, message, duration? })`
完整 props 形式, 用于动态 status。

### `Toast.dismiss(id)`
关闭单条。

### `Toast.clear()`
清空所有 toast。

---

## 5. 场景示例

### 5.1 基础调用 (最常用)
```tsx
import { Toast } from '@shopee/design-system';

// 保存成功
await api.save();
Toast.success('Saved successfully');

// 操作失败
try {
  await api.delete();
} catch (e) {
  Toast.error('Delete failed: ' + e.message);
}
```

### 5.2 自定义 duration
```tsx
Toast.success('Done', { duration: 1500 });        // 1.5s 消失
Toast.error('Critical', { duration: 0 });         // 不自动消失
```

### 5.3 手动关闭
```tsx
const id = Toast.info('Uploading...', { duration: 0 });
// 上传完成后
api.upload().finally(() => Toast.dismiss(id));
```

### 5.4 动态 status
```tsx
function notify(result: { ok: boolean; msg: string }) {
  Toast.show({
    status: result.ok ? 'success' : 'error',
    message: result.msg,
  });
}
```

### 5.5 多条排队
```tsx
// 旧规范: 最多 2 条同屏, 多余排队
Toast.info('Step 1');
Toast.info('Step 2');
Toast.info('Step 3'); // 等前面消失再出
Toast.info('Step 4'); // 排队中
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| 背景 | `#FFFFFF` | `--Toast-colorBg` |
| 文字色 | `#333333` | `--Toast-colorText` |
| 字号/字重 | 14px Roboto Regular | `--Toast-fontSize` |
| 行高 | 22px (允许 2 行) | `--Toast-lineHeight` |
| Padding | 12px 16px | `--Toast-paddingBlock/Inline` |
| Border-radius | 4px | `--Toast-borderRadius` |
| Icon size | 16px | `--Toast-iconSize` |
| Icon→text gap | 8px | `--Toast-iconGap` |
| Min/Max width | 160 / 600 px | `--Toast-minWidth/maxWidth` |
| Shadow | 2 层 (10% + 6%) | `--Toast-shadow` |
| 距顶 | 24px | `--Toast-topOffset` |
| 同屏上限 | 2 条 | `--Toast-maxVisible` |
| 默认 duration | 3000ms | `--Toast-duration` |

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| `<Toast status="success" message="..." />` | `Toast.success('...')` | Toast 是 imperative API, 不是 React 组件 |
| 用 Toast 显示 form 字段错误 | 用 inline 字段 error | Form 错误必须留在字段旁, Toast 会被忽略 |
| 用 Toast 显示需要用户确认的内容 | 用 `<Modal />` | Toast 自动消失, 用户可能错过关键信息 |
| 同时触发 5+ Toast | 控制频率, 合并消息 | 多条 toast 体验差; 同屏上限 2 是硬约束 |
| Toast 内放复杂 JSX (按钮/表单) | 简单文本 / 链接 | Toast 设计为单行/双行简短消息 |
| `Toast.error(longErrorObj)` 超长 stack | 提取人类可读的关键信息 | maxWidth 600, 超长会换行/截断 |
| 业务必须看到的提示用 Toast | 用 Modal / Alert | Toast 可能被错过 (3s 自动消失) |
| 手动放 `<ToastContainer />` | 不用手动放 (auto-mount) | 已通过 createRoot 自动 mount, 重复放会出双重 toast |

---

## 8. Accessibility

- **error / warning** → `role="alert"`, `aria-live="assertive"` (屏读器立即播报)
- **success / info** → `role="status"`, `aria-live="polite"` (屏读器在空闲时播报)
- 不用 `<button>` 包裹 Toast, 也不接 click 关闭 (避免误触)
- duration 0 (persistent) 时, 屏读器仍正常播报

---

## 9. 历史变更

- **2026-06-05 v1** — Phase 5 首版
  - 4 status (success/error/info/warning)
  - Imperative API + auto-mount Portal
  - 队列 + slide-in 动画 + 同屏上限 2
  - 复用 Icon 库 status icons

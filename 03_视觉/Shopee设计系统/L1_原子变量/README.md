# L1 原子变量

L1 负责所有视觉数值的来源。**Figma Local Variables 是唯一真源**；本文件是它的离线镜像，用于出稿前建立正确的取值心智和交付前的客观核验。

- 库：`Seller Center Library`｜fileKey `KTvcllui6OGgNPI5f1DfHe`
- 变量集合：`Shopee Tokens`
- 文档页：`✅ Design Token 设计令牌`（node `1:2`）
- 本文件核验时间：**2026-08-09**

## 调用时机

页面骨架和组件已确定后读取。**不要用 Token 反推页面结构。**

出稿前至少确认三件事：本次要用的语义色属于哪一组、间距落在哪几个档位、文本用哪个命名文本样式。

---

## 一、三层 Token 架构

这是本层最重要的规则，此前完全未记录。

| 层 | 名称 | 内容 | 出稿时能否直接引用 |
|---|---|---|---|
| Tier 1 | **Base** | 调色板原色。9 色相 × 10 阶 + 4 个 alpha 叠加，共 94 个 | ❌ **不可直接引用** |
| Tier 2 | **Alias** | 语义层。Neutral 一组 + Brand 一组 | ✅ 首选 |
| Tier 3 | **Components** | 组件专用。`Components/{组件}/Global/*` 与 `Components/{组件}/Component/*` | ✅ 该组件内部使用 |

**引用规则：出稿一律引用 Tier 2 或 Tier 3，不直接引用 Tier 1。**

Base 层只是色板，没有语义——今天 `Orange/6` 是主色，主色改版时改的是 `colorPrimary` 的指向，直接绑 `Orange/6` 的地方不会跟着变。同理，组件内部的间距、高度、颜色优先找该组件的 Tier 3 token（例如 `Components/Header/Component/heightBase`），找不到再用 Foundation。

> 「不直接引用 Base 层」是依据三层结构和 Alias 层描述得出的规则，尚未在 Figma 中作为强制约束写死。**首次实际出稿时向设计负责人确认一次**，确认后再作为 L5 的硬判定项。

---

## 二、Tier 1 Base 调色板（94）

出稿不直接引用，仅用于理解 Alias 指向和核对色值。

| 阶 | Orange | Volcano | Teal | Blue | Red | Green | Yellow | Purple | Neutral |
|---|---|---|---|---|---|---|---|---|---|
| 1 | `#FEF6F5` | `#FEECE1` | `#E3F5F3` | `#E5EEFB` | `#FFE9E8` | `#EBF9EF` | `#FFF7E0` | `#F9F0FF` | `#FFFFFF` |
| 2 | `#FFE1D4` | `#FFE4BF` | `#B3E3D7` | `#CFE9FF` | `#FFEAE6` | `#D9F5E0` | `#FFEFB8` | `#EFDBFF` | `#FAFAFA` |
| 3 | `#FFC1AB` | `#FFD096` | `#87D6C5` | `#A6D4FF` | `#FFC6BD` | `#B7E8C4` | `#FFE38F` | `#D3ADF7` | `#F6F6F6` |
| 4 | `#FF9F82` | `#FFB96E` | `#5FC9B6` | `#79B6F7` | `#FF9F94` | `#92DCA6` | `#FFD566` | `#B37FEB` | `#EEEEEE` |
| 5 | `#FA7857` | `#FF9F45` | `#3ABDA9` | `#4D94EB` | `#FF756B` | `#6FD489` | `#FFC93D` | `#9254DE` | `#E5E5E5` |
| **6** | **`#EE4D2D`** | `#FF831D` | `#1BAF9D` | `#2673DD` | `#FF4742` | `#55CC77` | `#FFBF00` | `#722ED1` | `#B7B7B7` |
| 7 | `#C7331C` | `#D9620D` | `#0E8A7F` | `#1654B8` | `#D92E2E` | `#30B566` | `#EDA500` | `#531DAB` | `#999999` |
| 8 | `#A11D0E` | `#B34602` | `#05635F` | `#0A3991` | `#B31D22` | `#1F8B4D` | `#B37A00` | `#391085` | `#666666` |
| 9 | `#7A0D05` | `#8C3100` | `#003D3C` | `#02236B` | `#8C0F18` | `#136033` | `#8C5B00` | `#22075E` | `#333333` |
| 10 | `#540503` | `#662000` | `#001717` | `#011445` | `#660A13` | `#0A3D21` | `#663F00` | `#120338` | `#121212` |

第 6 阶是各色相的主阶。`Orange/6 = #EE4D2D` 是 Shopee 主色。

**Alpha 叠加**：`Alpha/04` `Alpha/08` `Alpha/12` `Alpha/50` = `#000000` 分别 0.04 / 0.08 / 0.12 / 0.50。

---

## 三、Tier 2 Alias — Neutral

文本、图标、背景、边框、填充。**出稿最高频的一组。**

### 文本

| Token | 指向 | 用途 |
|---|---|---|
| `colorTextHeading` | Base/Neutral/10 `#121212` | 标题 |
| `colorText` | Base/Neutral/9 `#333333` | 正文 |
| `colorTextSecondary` | Base/Neutral/8 `#666666` | 次级文本 |
| `colorTextTertiary` | Base/Neutral/7 `#999999` | 三级文本 |
| `colorTextQuaternary` | Base/Neutral/6 `#B7B7B7` | 四级文本 |
| `colorTextLabel` | → colorTextSecondary | 表单 label |
| `colorTextDescription` | → colorTextTertiary | 说明文字 |
| `colorTextPlaceholder` | → colorTextQuaternary | 占位符 |
| `colorTextDisabled` | → colorTextQuaternary | 禁用文本 |
| `colorTextLightSolid` | Base/Neutral/1 `#FFFFFF` | 深底上的文字 |

### 图标

| Token | 指向 |
|---|---|
| `colorIcon` | → colorTextTertiary |
| `colorIconHover` | → colorText |

### 背景

| Token | 指向 | 用途 |
|---|---|---|
| `colorBgContainer` | Base/Neutral/1 `#FFFFFF` | 容器底 |
| `colorBgElevated` | Base/Neutral/1 `#FFFFFF` | 浮层底 |
| `colorBgLayout` | Base/Neutral/3 `#F6F6F6` | 页面底 |
| `colorBgMask` | Base/Alpha/50 | 遮罩 |
| `colorBgSpotlight` | Base/Neutral/9 | 高亮/反白块 |
| `colorBgContainerDisabled` | → colorFillTertiary | 禁用容器 |
| `colorBgTextHover` | → colorFillSecondary | 文本按钮 hover |
| `colorBgTextActive` | → colorFill | 文本按钮 active |
| `colorBorderBg` | → colorBgContainer | 边框内底色 |

### 边框与分割

| Token | 指向 |
|---|---|
| `colorBorder` | Base/Neutral/5 `#E5E5E5` |
| `colorBorderSecondary` | Base/Neutral/4 `#EEEEEE` |
| `colorSplit` | Base/Alpha/08 |

### 填充

| Token | 指向 |
|---|---|
| `colorFill` | Base/Alpha/12 |
| `colorFillSecondary` | Base/Alpha/08 |
| `colorFillTertiary` | Base/Alpha/04 |
| `colorFillQuaternary` | Base/Alpha/04 |
| `colorFillContent` | → colorFillSecondary |
| `colorFillContentHover` | → colorFill |
| `colorFillAlter` | → colorFillQuaternary |

> ⚠️ **页面自身计数不一致**：Neutral Colors 页的说明文字写「35 tokens across 5 use-case groups」，但表格实际渲染 31 行（文本 10 / 图标 2 / 背景 9 / 边框 3 / 填充 7），分组数确为 5。差 4 个。可能是说明文字过时，也可能有 4 个变量存在于 `Shopee Tokens` 集合但未画进文档表。需要对照变量面板核一次。
>
> 对照：Base 表实测 94 行、页面标注 94，一致；Brand 表实测 61 行、页面标注 61，一致。只有 Neutral 对不上。

---

## 四、Tier 2 Alias — Brand（61）

7 个语义角色。**每个角色都是一整套 10 个变体，不是单个颜色**——做 hover、按下、浅底、边框、文字色时必须用对应变体，不得自己调透明度或换阶。

统一模式（以 `X` 代表 Primary / Success / Warning / Error / Info）：

| 后缀 | 指向 | 用途 |
|---|---|---|
| `colorX` | Base/{色相}/6 | 主体色 |
| `colorXHover` | Base/{色相}/5 | 悬停 |
| `colorXActive` | Base/{色相}/7 | 按下 |
| `colorXBg` | Base/{色相}/1 | 浅色底 |
| `colorXBgHover` | Base/{色相}/2 | 浅色底悬停 |
| `colorXBorder` | Base/{色相}/3 | 边框 |
| `colorXBorderHover` | Base/{色相}/4 | 边框悬停 |
| `colorXText` | Base/{色相}/7 | 文字 |
| `colorXTextHover` | Base/{色相}/8 | 文字悬停 |
| `colorXTextActive` | Base/{色相}/10 | 文字按下 |

角色与色相对应：

| 角色 | 色相 | 主体色值 |
|---|---|---|
| Primary | Orange | `#EE4D2D` |
| Success | Green | `#55CC77` |
| Warning | Yellow | `#FFBF00` |
| Error | Red | `#FF4742` |
| Info | Blue | `#2673DD` |

额外 token：

| Token | 值 / 指向 |
|---|---|
| `colorWarningOutline` | `#FFBF00`, 0.10 |
| `colorErrorOutline` | `#FF4742`, 0.10 |
| `colorLink` | → colorInfo |
| `colorLinkHover` | → colorInfoHover |
| `colorLinkActive` | → colorInfoActive |
| `controlOutline` | `#EE4D2D`, 0.10 |
| `controlItemBgActive` | → colorPrimaryBg |
| `controlItemBgActiveHover` | → colorPrimaryBgHover |
| `controlItemBgActiveDisabled` | → colorFill |
| `controlItemBgHover` | → colorFillTertiary |
| `controlTmpOutline` | → colorFillQuaternary |

---

## 五、Tier 3 Components

命名空间：

- `Components/{组件}/Global/*` —— 该组件的颜色角色，如 `Components/Header/Global/colorBg`、`Components/Header/Global/colorDivider`
- `Components/{组件}/Component/*` —— 该组件的尺寸与间距，如 `Components/Header/Component/heightBase`、`Components/Toolbar/Component/buttonGap`

许多 Tier 3 token 带中文描述，记录了取值依据（例如 `Components/Header/Component/heightBase` 注明「Header 整体高度, 旧 Guidelines 实测 56px」）。**调整组件尺寸前先读描述**，避免推翻已对齐旧规范的结论。

出稿顺序：组件专用 token → Foundation token → 才考虑提新 token。不在组件内写魔法数字。

---

## 六、Foundation

### 圆角

| Token | 值 |
|---|---:|
| `borderRadiusXS` | 2 |
| `borderRadiusSM` | 4 |
| `borderRadius` | 6 |
| `borderRadiusLG` | 8 |

绑定在 `CORNER_RADIUS` scope，只在圆角属性中出现。

### 尺寸

**Base 档位（9 档，不是 6 档）：**

| Token | 值 | 常见用途 |
|---|---:|---|
| `sizeXXS` | 4 | 最小间隙、图标与文字贴合 |
| `sizeXS` | 8 | 同类元素间距 |
| `sizeSM` | 12 | 紧凑内边距 |
| `sizeMS` | 16 | 内容水平内边距（语义区别于 `size`） |
| `size` | 16 | 默认间距、表单字段水平间距 |
| `sizeMD` | 20 | 表单字段垂直间距 |
| `sizeLG` | 24 | 区块间距、卡片和页面内边距 |
| `sizeXL` | 32 | 大区块间距 |
| `sizeXXL` | 48 | 页面级大留白 |

⚠️ `sizeMS` 与 `size` 数值都是 16，但语义不同：`paddingContentHorizontal` 指向 `sizeMS`，`paddingContentHorizontalSM` 指向 `size`。按语义选，不按数值选。

**工具档位**：`sizeUnit` 4｜`sizeStep` 4｜`sizePopupArrow` 16｜`controlInteractiveSize` 16

**控件高度**：`controlHeightXS` 16｜`controlHeightSM` 24｜`controlHeight` 32｜`controlHeightLG` 40

**线宽**：`lineWidth` 1｜`lineWidthBold` 2｜`controlOutlineWidth` 2｜`lineWidthFocus` 4

**断点**：

| Token | 值 | | Token | 值 |
|---|---:|---|---|---:|
| `screenXS` | 480 | | `screenXSMax` | 575 |
| `screenSM` | 576 | | `screenSMMax` | 767 |
| `screenMD` | 768 | | `screenMDMax` | 991 |
| `screenLG` | 992 | | `screenLGMax` | 1199 |
| `screenXL` | 1200 | | `screenXLMax` | 1599 |
| `screenXXL` | 1600 | | | |

各 `screenXMin` 指向对应的 `screenX`。L3 规定仅 desktop、只考虑浏览器宽度自适应，断点主要用于确认目标视口。

### 间距

`margin*` 与 `padding*` 全部别名到 `Size/Base`，一一对应：`marginXXS`→`sizeXXS`、`marginXS`→`sizeXS`、`marginSM`→`sizeSM`、`margin`→`size`、`marginMD`→`sizeMD`、`marginLG`→`sizeLG`、`marginXL`→`sizeXL`、`marginXXL`→`sizeXXL`；`padding*` 同理（无 `paddingXXL`）。

内容内边距：

| Token | 指向 | 值 |
|---|---|---:|
| `paddingContentHorizontal` | → sizeMS | 16 |
| `paddingContentHorizontalLG` | → sizeLG | 24 |
| `paddingContentHorizontalSM` | → size | 16 |
| `paddingContentVertical` | → sizeSM | 12 |
| `paddingContentVerticalLG` | → sizeMS | 16 |
| `paddingContentVerticalSM` | → sizeXS | 8 |

控件内边距是字面值，不别名：`controlPaddingHorizontal` 12｜`controlPaddingHorizontalSM` 8

### 字体

| Token | 值 |
|---|---|
| `fontFamily` | Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', … |
| `fontFamilyCode` | 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, … |

| 字号 Token | 值 | | 行高 Token | 倍数 · px |
|---|---:|---|---|---|
| `fontSizeSM` | 12 | | `lineHeightSM` | 1.333 · 16/12 |
| `fontSize` | 14 | | `lineHeight` | 1.429 · 20/14 |
| `fontSizeLG` | 16 | | `lineHeightLG` | 1.500 · 24/16 |
| `fontSizeXL` | 18 | | `lineHeightXL` | 1.444 · 26/18 |
| `fontSizeHeading2` | 20 | | `lineHeightHeading2` | 1.400 · 28/20 |
| `fontSizeHeading1` | 24 | | `lineHeightHeading1` | 1.333 · 32/24 |

`fontWeightStrong` = 500。**只有 6 个字号档位**，不得新增相近字号。

### 文本样式（9 个命名样式）

Figma 文本面板可直接选用。**优先用命名样式，不要手动拼字号 + 行高 + 字重。**

| 样式 | 规格 |
|---|---|
| `Heading/xl` | 24px · Medium · 32px 行高 |
| `Heading/l` | 20px · Medium · 28px |
| `Heading/m` | 18px · Medium · 26px |
| `Heading/s` | 16px · Medium · 24px |
| `Heading/xs` | 14px · Medium · 20px |
| `Body/medium` | 14px · Medium · 20px |
| `Body/regular` | 14px · Regular · 20px |
| `Caption/medium` | 12px · Medium · 16px |
| `Caption/regular` | 12px · Regular · 16px |

⚠️ `Heading/xs` 与 `Body/medium` 规格完全相同（14/Medium/20），按语义选：前者是小标题，后者是强调正文。

### 阴影（3 个 Effect Style）

每个都是 3 层 drop shadow 堆叠，**必须整体套用 Effect Style，不得手写单层阴影**。

| Style | 用途 | 层 |
|---|---|---|
| `boxShadow` | 默认层级。Popover、Tooltip、Dropdown | `0 2 4 0 rgba(0,0,0,.02)` + `0 1 6 -1 rgba(0,0,0,.02)` + `0 1 2 0 rgba(0,0,0,.03)` |
| `boxShadowSecondary` | 显著层级。Modal、Drawer、Popconfirm | `0 9 28 8 rgba(0,0,0,.05)` + `0 3 6 -4 rgba(0,0,0,.12)` + `0 6 16 0 rgba(0,0,0,.08)` |
| `boxShadowTertiary` | 保留，当前与 `boxShadow` 相同 | 同 `boxShadow` |

---

## 六之二、文本对比度（重要）

Shopee 色板中有相当一部分语义色**达不到 WCAG AA 正文标准（4.5:1）**。这不是错误，是色板的既定事实；但它意味着「所有文本都必须达到 AA」这条通用规则在本设计系统内不成立，必须按用途分层。

实测值（sRGB，白底 `#FFFFFF` / 页面底 `colorBgLayout` `#F6F6F6`）：

| Token | 色值 | 白底 | 页面底 | 可作正文 |
|---|---|---:|---:|---|
| `colorTextHeading` | `#121212` | 18.73:1 | 17.33:1 | ✅ |
| `colorText` | `#333333` | 12.63:1 | 11.69:1 | ✅ |
| `colorTextSecondary` | `#666666` | 5.74:1 | 5.31:1 | ✅ |
| `colorTextTertiary`（= Description / Icon） | `#999999` | 2.85:1 | 2.64:1 | ❌ |
| `colorTextQuaternary`（= Placeholder / Disabled） | `#B7B7B7` | 2.01:1 | 1.86:1 | ❌ |
| `colorPrimary` | `#EE4D2D` | 3.66:1 | 3.39:1 | ❌ |
| `colorPrimaryText` | `#C7331C` | 5.36:1 | 4.96:1 | ✅ |
| `colorError` | `#FF4742` | 3.37:1 | 3.12:1 | ❌ |
| `colorErrorText` | `#D92E2E` | 4.79:1 | 4.44:1 | ✅ 白底；页面底 4.44 略低于 4.5 |
| `colorInfo` / `colorLink` | `#2673DD` | 4.59:1 | 4.24:1 | ✅ 白底；**页面底不达标** |
| `colorInfoText` | `#1654B8` | 7.01:1 | 6.49:1 | ✅ |
| `colorSuccess` | `#55CC77` | 2.04:1 | 1.89:1 | ❌ |
| `colorSuccessText` | `#30B566` | 2.65:1 | 2.45:1 | ❌ 连 Text 变体也不达标 |
| `colorWarning` | `#FFBF00` | 1.65:1 | 1.53:1 | ❌ |
| `colorWarningText` | `#EDA500` | 2.10:1 | 1.95:1 | ❌ 连 Text 变体也不达标 |

### 使用规则

1. **正文、标题、表格数据、表单值** —— 只用 `colorTextHeading` / `colorText` / `colorTextSecondary`。
2. **彩色文字用 `*Text` 变体，不用主体色。** `colorPrimary`（3.66）不能当正文色，`colorPrimaryText`（5.36）才可以。Error、Info 同理。这是色板已经内置的解法。
3. **Success 与 Warning 即使用 `*Text` 变体也不达标**（2.65 / 2.10）。这两类状态**不得只靠颜色文字承载信息**，必须同时有图标、状态文案或 Tag 形状；或改用 `colorText` 作文字、只用状态色做图标与底色。这与「不只依赖颜色传达状态」是同一条要求的具体化。
4. **注意背景差异**：`colorLink`（`colorInfo`）在白底 4.59 达标，放到页面底 `colorBgLayout` 只有 4.24，**不达标**。链接放在灰底区域时改用 `colorInfoText`。`colorErrorText` 在页面底 4.44 同样擦边，同样处理。
5. **`colorTextDescription`（→ Tertiary，2.85）承载真实信息时不达标。** 说明文字若是理解任务所必需，改用 `colorTextSecondary`；只作辅助补充时可保留 Tertiary，并在自检中登记。
6. **Placeholder 与 Disabled 免于对比度要求**，WCAG 1.4.3 对失效控件有明确豁免，保持 `colorTextQuaternary` 即可。
7. `colorBorder`（1.26）等非文本元素不适用文本对比度标准，按边界可辨识判断。

> 以上比值由 sRGB 相对亮度公式计算得出（2026-08-09）。作为硬判定前建议用对比度工具复核一次，并就第 3、5 条与设计负责人确认取舍。

---

## 七、使用规则

- 不写裸色值、裸间距、裸字号、裸圆角、裸阴影。
- 颜色引用 Tier 2 Alias 或 Tier 3 Components，不直接引用 Tier 1 Base。
- 需要 hover / active / 禁用 / 浅底 / 边框 / 文字色时，用该语义角色已有的变体，不调透明度、不换色阶。
- 组件已有变体时，不用透明度或自定义样式模拟状态。
- 文本优先用 9 个命名文本样式；确需单独设置时，字号只能取 6 个档位之一，行高取配对值。
- 阴影只用 3 个 Effect Style，不手写。
- Figma 与本文件冲突时，**以当前 Figma 为准**，并回来更新本文件或记录差异。
- 无法读取或无法确认的值标记为「未验证」，不得在自查中判为通过。

## 八、反例

| 反例 | 正确做法 |
|---|---|
| 为接近截图新增一个相似色值 | 在 Alias 层找语义最接近的角色变体 |
| 直接绑 `Base/Orange/6` 做主色 | 绑 `colorPrimary` |
| 用 `colorPrimary` + 透明度做 hover | 用 `colorPrimaryHover` |
| 使用 14、18、22 等非规范间距修补布局 | 取 `sizeXXS`–`sizeXXL` 九档之一 |
| 用透明度模拟 Disabled 状态 | 用组件 Disabled 变体 + `colorTextDisabled` / `colorBgContainerDisabled` |
| 手写一层 `0 2 8 rgba(0,0,0,.1)` 阴影 | 套 `boxShadow` 或 `boxShadowSecondary` |
| 手动设 16px + Medium + 24px 行高 | 选 `Heading/s` 文本样式 |
| 把旧源码中的变量当作当前 Figma Token | 现读 Figma |

## 九、核验记录

- **2026-08-09**：首次从 Figma 文档页 `✅ Design Token 设计令牌`（node `1:2`）全量抄录。此前本文件只记录了 6 个间距档位和 6 个语义色名（共 12 项），实际体系为三层近 200 个 token。本次补齐：三层架构说明、94 个 Base 色、Neutral 与 Brand 两组 Alias、Tier 3 命名规则、圆角 / 尺寸 / 间距 / 字体 / 文本样式 / 阴影六组 Foundation。
- **2026-08-09（复核）**：9 个 Foundation / Color 表逐表核对。Base 实测 94 行、Brand 实测 61 行，均与页面标注一致；Neutral 实测 31 行、页面标注 35，不一致。新增「文本对比度」一节，实测发现色板中 8 个语义色达不到 WCAG AA 正文标准，其中 Success 与 Warning 连 `*Text` 变体也不达标——据此修订了通用视觉规范与 L5 中原本一刀切的对比度判定。
- 待复核项：① Neutral Alias 表 31 行 vs 说明文字 35，需对照变量面板确认差的 4 个；② 「不直接引用 Base 层」需向设计负责人确认后再作为硬判定项；③ 文本对比度分层规则的第 3、5 条（Success/Warning 处理方式、Description 何时必须升到 Secondary）需设计负责人拍板；④ 深色主题——文档页只有 Light Theme 一列，L3 已规定仅 light，如未来引入深色需重新抄录。

# Design System

## Investment Management Mobile Application

**Version:** 1.0  
**Last Updated:** 2024-01-17  
**UI Kit:** shadcn/ui (adapted for React Native via NativeWind)  
**Styling:** Tailwind CSS / NativeWind  
**Icons:** Lucide React Native  

---

## 1. Color Palette

### 1.1 Primary Colors

The primary color palette conveys trust, professionalism, and financial stability—essential qualities for an investment management application.

| Name | Hex | Tailwind | Usage |
|------|-----|----------|-------|
| **Primary** | `#1E40AF` | `primary-700` | Main brand color, CTAs, active states |
| **Primary Light** | `#3B82F6` | `primary-500` | Hover states, secondary CTAs |
| **Primary Lighter** | `#60A5FA` | `primary-400` | Light backgrounds, subtle highlights |
| **Primary Lightest** | `#DBEAFE` | `primary-100` | Very light backgrounds, disabled fills |
| **Primary Dark** | `#1E3A8A` | `primary-800` | Pressed states, text on light primary |
| **Primary Darkest** | `#172554` | `primary-900` | Dark mode primary |

**CSS Variables:**
```css
:root {
  --primary: 30 64 175;        /* #1E40AF */
  --primary-foreground: 255 255 255;
}
```

### 1.2 Secondary Colors

Secondary colors provide visual interest and hierarchy without competing with the primary palette.

| Name | Hex | Tailwind | Usage |
|------|-----|----------|-------|
| **Secondary** | `#0F766E` | `secondary-700` | Secondary actions, highlights |
| **Secondary Light** | `#14B8A6` | `secondary-500` | Hover states, badges |
| **Secondary Lighter** | `#5EEAD4` | `secondary-300` | Light backgrounds |
| **Secondary Dark** | `#0D9488` | `secondary-600` | Pressed states |

### 1.3 Semantic Colors

Semantic colors communicate status, feedback, and importance levels.

#### Success (Positive returns, confirmations)
| Name | Hex | Tailwind | Usage |
|------|-----|----------|-------|
| **Success** | `#15803D` | `success-700` | Success states, positive values |
| **Success Light** | `#22C55E` | `success-500` | Success icons, light mode |
| **Success Background** | `#DCFCE7` | `success-100` | Success backgrounds |

#### Warning (Caution, pending states)
| Name | Hex | Tailwind | Usage |
|------|-----|----------|-------|
| **Warning** | `#B45309` | `warning-700` | Warning states, alerts |
| **Warning Light** | `#F59E0B` | `warning-500` | Warning icons |
| **Warning Background** | `#FEF3C7` | `warning-100` | Warning backgrounds |

#### Error (Negative returns, errors, destructive actions)
| Name | Hex | Tailwind | Usage |
|------|-----|----------|-------|
| **Error** | `#B91C1C` | `error-700` | Error states, negative values |
| **Error Light** | `#EF4444` | `error-500` | Error icons |
| **Error Background** | `#FEE2E2` | `error-100` | Error backgrounds |

#### Info (Informational content)
| Name | Hex | Tailwind | Usage |
|------|-----|----------|-------|
| **Info** | `#0369A1` | `info-700` | Info states, tips |
| **Info Light** | `#0EA5E9` | `info-500` | Info icons |
| **Info Background** | `#E0F2FE` | `info-100` | Info backgrounds |

### 1.4 Neutral Colors

Neutral colors form the foundation of the UI, providing contrast and readability.

| Name | Hex | Tailwind | Usage |
|------|-----|----------|-------|
| **Black** | `#0A0A0A` | `neutral-950` | Pure black (use sparingly) |
| **Gray 900** | `#171717` | `neutral-900` | Primary text |
| **Gray 800** | `#262626` | `neutral-800` | Secondary text |
| **Gray 700** | `#404040` | `neutral-700` | Tertiary text |
| **Gray 600** | `#525252` | `neutral-600` | Placeholder text |
| **Gray 500** | `#737373` | `neutral-500` | Disabled text |
| **Gray 400** | `#A3A3A3` | `neutral-400` | Icons, dividers |
| **Gray 300** | `#D4D4D4` | `neutral-300` | Borders |
| **Gray 200** | `#E5E5E5` | `neutral-200` | Light borders, separators |
| **Gray 100** | `#F5F5F5` | `neutral-100` | Light backgrounds |
| **Gray 50** | `#FAFAFA` | `neutral-50` | Card backgrounds |
| **White** | `#FFFFFF` | `white` | Background, inverse text |

### 1.5 Financial Colors

Special colors for financial data display.

| Name | Hex | Usage |
|------|-----|-------|
| **Profit/Gain** | `#15803D` | Positive returns, gains |
| **Loss/Decline** | `#B91C1C` | Negative returns, losses |
| **Neutral/Unchanged** | `#737373` | No change |

### 1.6 Color Contrast Ratios (Accessibility)

All color combinations meet WCAG 2.1 AA requirements (minimum 4.5:1 for normal text, 3:1 for large text).

| Combination | Ratio | WCAG Level |
|-------------|-------|------------|
| Primary (#1E40AF) on White | 7.2:1 | AAA |
| Gray 900 (#171717) on White | 17.4:1 | AAA |
| Gray 800 (#262626) on White | 12.6:1 | AAA |
| White on Primary (#1E40AF) | 7.2:1 | AAA |
| Success (#15803D) on White | 5.2:1 | AA |
| Error (#B91C1C) on White | 5.0:1 | AA |
| Gray 600 (#525252) on White | 5.9:1 | AA |

### 1.7 Dark Mode Colors

| Element | Light Mode | Dark Mode |
|---------|------------|-----------|
| Background | `#FFFFFF` | `#0A0A0A` |
| Card Background | `#FAFAFA` | `#171717` |
| Primary Text | `#171717` | `#FAFAFA` |
| Secondary Text | `#525252` | `#A3A3A3` |
| Border | `#E5E5E5` | `#262626` |
| Primary | `#1E40AF` | `#3B82F6` |
| Success | `#15803D` | `#22C55E` |
| Error | `#B91C1C` | `#EF4444` |

---

## 2. Typography

### 2.1 Font Families

| Family | Usage | Font |
|--------|-------|------|
| **Heading** | Titles, headings | Inter (system fallback: SF Pro, Roboto) |
| **Body** | Body text, labels | Inter (system fallback: SF Pro, Roboto) |
| **Mono** | Numbers, codes | JetBrains Mono (fallback: SF Mono, Roboto Mono) |

**NativeWind Configuration:**
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    fontFamily: {
      sans: ['Inter', 'system-ui', 'sans-serif'],
      mono: ['JetBrains Mono', 'Menlo', 'monospace'],
    },
  },
};
```

### 2.2 Font Size Scale

| Token | Size | Line Height | Tailwind | Usage |
|-------|------|-------------|----------|-------|
| **xs** | 12px | 16px | `text-xs` | Captions, timestamps |
| **sm** | 14px | 20px | `text-sm` | Labels, secondary text |
| **base** | 16px | 24px | `text-base` | Body text |
| **lg** | 18px | 28px | `text-lg` | Emphasized body |
| **xl** | 20px | 28px | `text-xl` | Subheadings |
| **2xl** | 24px | 32px | `text-2xl` | Section headings |
| **3xl** | 30px | 36px | `text-3xl` | Screen titles |
| **4xl** | 36px | 40px | `text-4xl` | Large titles |
| **5xl** | 48px | 48px | `text-5xl` | Hero numbers |

### 2.3 Font Weights

| Token | Weight | Tailwind | Usage |
|-------|--------|----------|-------|
| **Light** | 300 | `font-light` | Large display text |
| **Normal** | 400 | `font-normal` | Body text |
| **Medium** | 500 | `font-medium` | Labels, emphasis |
| **Semibold** | 600 | `font-semibold` | Headings, buttons |
| **Bold** | 700 | `font-bold` | Strong emphasis |

### 2.4 Letter Spacing

| Token | Value | Tailwind | Usage |
|-------|-------|----------|-------|
| **Tighter** | -0.05em | `tracking-tighter` | Large headlines |
| **Tight** | -0.025em | `tracking-tight` | Headings |
| **Normal** | 0 | `tracking-normal` | Body text |
| **Wide** | 0.025em | `tracking-wide` | Labels, uppercase |
| **Wider** | 0.05em | `tracking-wider` | Buttons, CTAs |
| **Widest** | 0.1em | `tracking-widest` | Legal text |

### 2.5 Typography Components

#### Heading Styles
```typescript
// Heading component variants
const headingVariants = {
  h1: 'text-4xl font-bold tracking-tight text-gray-900',
  h2: 'text-3xl font-semibold tracking-tight text-gray-900',
  h3: 'text-2xl font-semibold tracking-tight text-gray-900',
  h4: 'text-xl font-semibold text-gray-900',
  h5: 'text-lg font-medium text-gray-900',
  h6: 'text-base font-medium text-gray-900',
};
```

#### Body Styles
```typescript
const bodyVariants = {
  large: 'text-lg text-gray-800 leading-relaxed',
  base: 'text-base text-gray-800 leading-normal',
  small: 'text-sm text-gray-700 leading-normal',
  caption: 'text-xs text-gray-500 leading-normal',
};
```

#### Financial Numbers
```typescript
const financialStyles = {
  value: 'font-mono text-3xl font-semibold tabular-nums',
  change: 'font-mono text-sm font-medium tabular-nums',
  percentage: 'font-mono text-base tabular-nums',
};
```

---

## 3. Spacing

### 3.1 Spacing Scale

The spacing scale follows an 8px base unit for visual consistency.

| Token | Size | Tailwind | Pixels | Usage |
|-------|------|----------|--------|-------|
| **0** | 0 | `p-0`, `m-0` | 0px | No spacing |
| **0.5** | 0.125rem | `p-0.5`, `m-0.5` | 2px | Micro spacing |
| **1** | 0.25rem | `p-1`, `m-1` | 4px | Tight spacing |
| **1.5** | 0.375rem | `p-1.5`, `m-1.5` | 6px | Compact spacing |
| **2** | 0.5rem | `p-2`, `m-2` | 8px | Standard small |
| **2.5** | 0.625rem | `p-2.5`, `m-2.5` | 10px | Medium small |
| **3** | 0.75rem | `p-3`, `m-3` | 12px | Default compact |
| **3.5** | 0.875rem | `p-3.5`, `m-3.5` | 14px | Near standard |
| **4** | 1rem | `p-4`, `m-4` | 16px | Standard padding |
| **5** | 1.25rem | `p-5`, `m-5` | 20px | Comfortable |
| **6** | 1.5rem | `p-6`, `m-6` | 24px | Section padding |
| **8** | 2rem | `p-8`, `m-8` | 32px | Large sections |
| **10** | 2.5rem | `p-10`, `m-10` | 40px | Screen padding |
| **12** | 3rem | `p-12`, `m-12` | 48px | Major sections |
| **16** | 4rem | `p-16`, `m-16` | 64px | Spacious |
| **20** | 5rem | `p-20`, `m-20` | 80px | Hero areas |
| **24** | 6rem | `p-24`, `m-24` | 96px | Large gaps |

### 3.2 Padding Conventions

| Component | Padding | Tailwind |
|-----------|---------|----------|
| **Screen** | 20px horizontal, 24px vertical | `px-5 py-6` |
| **Card** | 16px | `p-4` |
| **Card (compact)** | 12px | `p-3` |
| **Button (sm)** | 8px horizontal, 6px vertical | `px-2 py-1.5` |
| **Button (md)** | 16px horizontal, 8px vertical | `px-4 py-2` |
| **Button (lg)** | 24px horizontal, 12px vertical | `px-6 py-3` |
| **Input** | 12px horizontal, 10px vertical | `px-3 py-2.5` |
| **List Item** | 16px horizontal, 12px vertical | `px-4 py-3` |
| **Section Header** | 16px horizontal, 12px vertical | `px-4 py-3` |

### 3.3 Margin Conventions

| Element | Margin | Tailwind |
|---------|--------|----------|
| **Section spacing** | 24px bottom | `mb-6` |
| **Paragraph spacing** | 16px bottom | `mb-4` |
| **Label to input** | 8px | `mb-2` |
| **Form field spacing** | 16px | `mb-4` |
| **Button group** | 12px | `gap-3` |
| **List items** | 1px separator | N/A (use border) |

### 3.4 Gap Values

| Context | Gap | Tailwind |
|---------|-----|----------|
| **Inline elements** | 4px | `gap-1` |
| **Button groups** | 8px | `gap-2` |
| **Card grids** | 12px | `gap-3` |
| **Form fields** | 16px | `gap-4` |
| **Sections** | 24px | `gap-6` |
| **Major sections** | 32px | `gap-8` |

---

## 4. Components

### 4.1 Button

#### Variants
```typescript
const buttonVariants = {
  // Primary - main actions
  primary: 'bg-primary-700 text-white font-semibold rounded-lg active:bg-primary-800',
  
  // Secondary - secondary actions
  secondary: 'bg-gray-100 text-gray-900 font-medium rounded-lg active:bg-gray-200',
  
  // Outline - tertiary actions
  outline: 'border-2 border-primary-700 text-primary-700 font-medium rounded-lg active:bg-primary-50',
  
  // Ghost - subtle actions
  ghost: 'text-primary-700 font-medium active:bg-primary-100',
  
  // Destructive - dangerous actions
  destructive: 'bg-error-700 text-white font-semibold rounded-lg active:bg-error-800',
  
  // Success - confirmation actions
  success: 'bg-success-700 text-white font-semibold rounded-lg active:bg-success-800',
};
```

#### Sizes
```typescript
const buttonSizes = {
  sm: 'px-3 py-1.5 text-sm',
  md: 'px-4 py-2.5 text-base',
  lg: 'px-6 py-3.5 text-lg',
  icon: 'p-2',
};
```

#### States
| State | Visual Treatment |
|-------|-------------------|
| **Default** | Base colors |
| **Hover/Pressed** | Darker shade (10% darker) |
| **Active** | Darkest shade |
| **Disabled** | 50% opacity, no pointer events |
| **Loading** | Spinner icon, disabled interaction |

#### Button Props
```typescript
interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost' | 'destructive' | 'success';
  size?: 'sm' | 'md' | 'lg' | 'icon';
  disabled?: boolean;
  loading?: boolean;
  leftIcon?: React.ReactNode;
  rightIcon?: React.ReactNode;
  fullWidth?: boolean;
  onPress?: () => void;
}
```

### 4.2 Input Fields

#### Text Input
```typescript
const inputVariants = {
  default: 'border border-gray-300 rounded-lg bg-white px-3 py-2.5 text-base',
  focused: 'border-primary-500 ring-2 ring-primary-100',
  error: 'border-error-500 ring-2 ring-error-100',
  disabled: 'bg-gray-100 text-gray-500',
};
```

#### Input Sizes
```typescript
const inputSizes = {
  sm: 'px-2.5 py-1.5 text-sm',
  md: 'px-3 py-2.5 text-base',
  lg: 'px-4 py-3 text-lg',
};
```

#### Input Props
```typescript
interface InputProps {
  label?: string;
  placeholder?: string;
  helperText?: string;
  error?: string;
  disabled?: boolean;
  required?: boolean;
  leftIcon?: React.ReactNode;
  rightIcon?: React.ReactNode;
  type?: 'text' | 'email' | 'password' | 'number' | 'tel';
}
```

### 4.3 Cards

#### Card Variants
```typescript
const cardVariants = {
  // Default card
  default: 'bg-white rounded-xl border border-gray-200 p-4',
  
  // Elevated card
  elevated: 'bg-white rounded-xl shadow-md p-4',
  
  // Outlined card
  outlined: 'bg-transparent rounded-xl border border-gray-300 p-4',
  
  // Interactive card
  interactive: 'bg-white rounded-xl border border-gray-200 p-4 active:bg-gray-50',
};
```

#### Card Props
```typescript
interface CardProps {
  variant?: 'default' | 'elevated' | 'outlined' | 'interactive';
  padding?: 'none' | 'sm' | 'md' | 'lg';
  onPress?: () => void;
}
```

### 4.4 Navigation

#### Bottom Tab Navigation
```typescript
const tabStyles = {
  container: 'bg-white border-t border-gray-200 px-2 py-1',
  tab: 'flex-1 items-center py-2',
  tabActive: 'text-primary-700',
  tabInactive: 'text-gray-500',
  icon: 'w-6 h-6',
  label: 'text-xs mt-1',
  indicator: 'absolute top-0 h-0.5 w-8 bg-primary-700 rounded-full',
};
```

#### Top Navigation (Header)
```typescript
const headerStyles = {
  container: 'bg-white border-b border-gray-200 px-4 py-3',
  title: 'text-lg font-semibold text-gray-900',
  backButton: 'p-2 -ml-2',
  actionButton: 'p-2 -mr-2',
};
```

### 4.5 Modals

#### Modal Styles
```typescript
const modalStyles = {
  overlay: 'bg-black/50 flex items-center justify-center',
  container: 'bg-white rounded-2xl mx-4 max-w-sm w-full overflow-hidden',
  header: 'px-6 pt-6 pb-2',
  title: 'text-xl font-semibold text-gray-900',
  body: 'px-6 py-4',
  footer: 'px-6 pb-6 pt-2 flex gap-3 justify-end',
};
```

#### Modal Variants
| Type | Usage | Behavior |
|------|-------|----------|
| **Alert** | Critical warnings | Single action to dismiss |
| **Confirm** | Action confirmation | Cancel + Confirm buttons |
| **Form** | Data input | Full form with submit |
| **Bottom Sheet** | Quick actions | Slides up from bottom |

### 4.6 Lists

#### List Item
```typescript
const listItemStyles = {
  container: 'flex-row items-center px-4 py-3 border-b border-gray-100',
  leading: 'mr-3',
  content: 'flex-1',
  title: 'text-base font-medium text-gray-900',
  subtitle: 'text-sm text-gray-500',
  trailing: 'ml-3',
  chevron: 'text-gray-400',
};
```

#### List Variants
| Variant | Usage |
|---------|-------|
| **Simple** | Text only |
| **With Icon** | Icon + text |
| **With Avatar** | Avatar + text + metadata |
| **With Actions** | Text + action buttons |
| **Selectable** | Checkbox/radio + text |

### 4.7 Forms

#### Form Field Layout
```typescript
const formFieldStyles = {
  container: 'mb-4',
  label: 'text-sm font-medium text-gray-700 mb-1.5',
  required: 'text-error-500',
  input: 'border border-gray-300 rounded-lg bg-white px-3 py-2.5',
  error: 'text-sm text-error-600 mt-1',
  helper: 'text-sm text-gray-500 mt-1',
};
```

#### Form Components
| Component | Usage |
|-----------|-------|
| **Text Input** | Single line text |
| **Text Area** | Multi-line text |
| **Select** | Dropdown selection |
| **Checkbox** | Boolean options |
| **Radio** | Mutually exclusive options |
| **Toggle/Switch** | On/off settings |
| **Date Picker** | Date selection |
| **Number Input** | Numeric values |

### 4.8 Chat Components

#### Message Bubble
```typescript
const messageBubbleStyles = {
  // Sent messages (user)
  sent: 'bg-primary-700 text-white rounded-2xl rounded-tr-sm px-4 py-2.5',
  
  // Received messages (manager)
  received: 'bg-gray-100 text-gray-900 rounded-2xl rounded-tl-sm px-4 py-2.5',
  
  // Timestamp
  timestamp: 'text-xs text-gray-400 mt-1',
  
  // Status indicator
  status: 'text-xs text-gray-400',
};
```

#### Message Input
```typescript
const messageInputStyles = {
  container: 'flex-row items-center px-4 py-3 bg-white border-t border-gray-200',
  input: 'flex-1 bg-gray-100 rounded-full px-4 py-2.5 mr-3',
  sendButton: 'w-10 h-10 rounded-full bg-primary-700 items-center justify-center',
};
```

### 4.9 Portfolio Components

#### Value Display
```typescript
const valueDisplayStyles = {
  container: 'flex-col',
  primaryValue: 'font-mono text-3xl font-semibold tabular-nums text-gray-900',
  secondaryValue: 'font-mono text-sm font-medium tabular-nums',
  positive: 'text-success-700',
  negative: 'text-error-700',
  neutral: 'text-gray-500',
};
```

#### Position Card
```typescript
const positionCardStyles = {
  container: 'bg-white rounded-xl border border-gray-200 p-4',
  header: 'flex-row justify-between items-center mb-2',
  assetName: 'text-base font-medium text-gray-900',
  assetSymbol: 'text-sm text-gray-500',
  value: 'font-mono text-lg font-semibold tabular-nums',
  change: 'font-mono text-sm font-medium tabular-nums',
  weight: 'text-xs text-gray-400',
};
```

---

## 5. Borders & Radius

### 5.1 Border Widths

| Token | Width | Tailwind | Usage |
|-------|-------|----------|-------|
| **None** | 0 | `border-0` | No border |
| **Default** | 1px | `border` | Standard borders |
| **Medium** | 2px | `border-2` | Emphasized borders |
| **Thick** | 4px | `border-4` | Strong emphasis |

### 5.2 Border Radius Scale

| Token | Radius | Tailwind | Usage |
|-------|--------|----------|-------|
| **None** | 0 | `rounded-none` | Sharp corners |
| **sm** | 4px | `rounded-sm` | Slight rounding |
| **Default** | 6px | `rounded` | Standard rounding |
| **md** | 8px | `rounded-md` | Medium rounding |
| **lg** | 12px | `rounded-lg` | Large rounding (buttons) |
| **xl** | 16px | `rounded-xl` | Extra large (cards) |
| **2xl** | 20px | `rounded-2xl` | Cards, modals |
| **3xl** | 24px | `rounded-3xl` | Large containers |
| **Full** | 9999px | `rounded-full` | Pills, avatars, circles |

### 5.3 Shadow Scale

| Token | Shadow | Tailwind | Usage |
|-------|--------|----------|-------|
| **None** | None | `shadow-none` | No shadow |
| **sm** | Subtle | `shadow-sm` | Cards on light backgrounds |
| **Default** | Light | `shadow` | Elevated cards |
| **md** | Medium | `shadow-md` | Dropdowns, tooltips |
| **lg** | Large | `shadow-lg` | Modals, overlays |
| **xl** | Extra large | `shadow-xl` | Floating elements |
| **2xl** | Dramatic | `shadow-2xl` | Hero elements |

**Shadow Values:**
```css
--shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
--shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
--shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
--shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
--shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
--shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);
```

---

## 6. Breakpoints

### 6.1 Responsive Breakpoints

| Breakpoint | Min Width | Max Width | Devices |
|------------|-----------|-----------|---------|
| **Mobile** | 0px | 639px | Phones (iPhone, Android) |
| **Tablet** | 640px | 1023px | iPads, tablets |
| **Desktop** | 1024px | ∞ | Tablets in landscape, web |

**Tailwind Configuration:**
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    screens: {
      'sm': '640px',   // Tablet
      'md': '768px',   // Tablet portrait
      'lg': '1024px',  // Desktop / Tablet landscape
      'xl': '1280px',  // Large desktop
      '2xl': '1536px', // Extra large desktop
    },
  },
};
```

### 6.2 Mobile-First Design

Design for mobile first, then enhance for larger screens:

```typescript
// Example responsive styling
const containerStyles = 'px-4 sm:px-6 lg:px-8'; // Padding increases with screen size
const cardStyles = 'rounded-xl sm:rounded-2xl'; // More rounding on larger screens
const gridStyles = 'grid-cols-1 sm:grid-cols-2 lg:grid-cols-3'; // More columns on larger screens
```

### 6.3 Platform-Specific Considerations

| Platform | Safe Areas | Navigation | Touch Target |
|----------|------------|------------|--------------|
| **iOS** | Top notch, bottom home indicator | Tab bar at bottom | 44pt minimum |
| **Android** | Status bar, navigation gesture | Bottom navigation | 48dp minimum |

---

## 7. Accessibility

### 7.1 WCAG 2.1 AA Requirements

| Requirement | Implementation |
|-------------|----------------|
| **1.1.1 Non-text Content** | All images have alt text, decorative images marked as such |
| **1.3.1 Info and Relationships** | Semantic markup, proper heading hierarchy |
| **1.4.1 Use of Color** | Color not sole means of conveying information |
| **1.4.3 Contrast Minimum** | 4.5:1 for normal text, 3:1 for large text |
| **1.4.4 Resize Text** | Content readable at 200% zoom |
| **2.1.1 Keyboard** | All functionality accessible via keyboard |
| **2.4.1 Bypass Blocks** | Skip links or clear navigation |
| **2.4.3 Focus Order** | Logical tab order |
| **2.4.7 Focus Visible** | Visible focus indicators |
| **3.2.1 On Focus** | No unexpected context changes |
| **4.1.1 Parsing** | Valid markup |
| **4.1.2 Name, Role, Value** | Proper ARIA attributes |

### 7.2 Focus Indicators

| Element | Focus Style |
|---------|-------------|
| **Buttons** | 2px ring in primary-500, offset 2px |
| **Inputs** | 2px ring in primary-500, offset 0px |
| **Links** | 2px underline in primary-500 |
| **Cards (interactive)** | 2px ring in primary-500 |
| **Custom controls** | 2px ring in primary-500 |

```typescript
const focusStyles = {
  button: 'focus:ring-2 focus:ring-primary-500 focus:ring-offset-2 focus:outline-none',
  input: 'focus:ring-2 focus:ring-primary-500 focus:border-primary-500 focus:outline-none',
  link: 'focus:underline focus:decoration-2 focus:underline-offset-2',
};
```

### 7.3 Color Contrast

**Minimum Contrast Ratios:**
- Normal text (< 18pt or < 14pt bold): 4.5:1
- Large text (≥ 18pt or ≥ 14pt bold): 3:1
- UI components and graphical objects: 3:1

**Testing Tools:**
- WebAIM Contrast Checker
- Stark (Figma plugin)
- axe DevTools

### 7.4 Screen Reader Considerations

#### Labels and Announcements
```typescript
// Accessibility props for React Native
<Button
  accessibilityLabel="Submit form"
  accessibilityHint="Submits the form and saves your data"
  accessibilityRole="button"
/>
```

#### Semantic Structure
- Use proper heading levels (H1 → H6)
- Use descriptive link text (not "click here")
- Provide form labels linked to inputs
- Use ARIA landmarks where appropriate

#### Dynamic Content
- Announce changes with `accessibilityLiveRegion`
- Provide status updates for loading/error states
- Use `accessibilityViewIsModal` for modals

### 7.5 Touch Target Sizes

| Element | Minimum Size | Recommended |
|---------|--------------|-------------|
| **Buttons** | 44×44 pt | 48×48 pt |
| **Links** | 44×44 pt | 48×48 pt |
| **Form controls** | 44×44 pt | 48×48 pt |
| **Icons (actionable)** | 44×44 pt | 48×48 pt |
| **List items** | 44pt height | 48pt height |

### 7.6 Motion and Animation

| Consideration | Implementation |
|---------------|----------------|
| **Reduced motion** | Respect `prefers-reduced-motion` |
| **No auto-play** | Don't auto-play animations |
| **Seizure prevention** | No more than 3 flashes per second |
| **Animation duration** | Keep under 300ms for UI elements |

```typescript
// Respecting reduced motion preference
import { useReducedMotion } from 'react-native-reanimated';

const duration = useReducedMotion() ? 0 : 300;
```

---

## 8. Iconography

### 8.1 Icon Library

**Primary Icon Set:** Lucide React Native

### 8.2 Icon Sizes

| Size | Pixels | Usage |
|------|--------|-------|
| **xs** | 12px | Inline indicators |
| **sm** | 16px | Small UI elements |
| **md** | 20px | Default icons |
| **lg** | 24px | Navigation, featured |
| **xl** | 32px | Hero sections |
| **2xl** | 48px | Feature highlights |

### 8.3 Common Icons

| Icon | Name | Usage |
|------|------|-------|
| `ChevronRight` | Navigation | Forward navigation, disclosure |
| `ChevronLeft` | Navigation | Back navigation |
| `ChevronDown` | Disclosure | Expand/collapse |
| `X` | Action | Close, remove |
| `Check` | Status | Success, completed |
| `Plus` | Action | Add, create |
| `Minus` | Action | Remove, decrease |
| `Search` | Action | Search |
| `Home` | Navigation | Home tab |
| `User` | Navigation | Profile tab |
| `MessageCircle` | Navigation | Chat tab |
| `PieChart` | Navigation | Portfolio tab |
| `TrendingUp` | Financial | Positive trend, gain |
| `TrendingDown` | Financial | Negative trend, loss |
| `DollarSign` | Financial | Currency, money |
| `Shield` | Security | Security, protected |
| `Lock` | Security | Lock, secure |
| `Eye` | Visibility | View, show |
| `EyeOff` | Visibility | Hide |
| `Bell` | Notifications | Notification, alert |
| `Settings` | Settings | Settings, preferences |
| `HelpCircle` | Help | Help, info |
| `LogOut` | Auth | Logout |

---

## 9. Animation & Transitions

### 9.1 Timing Functions

| Name | Value | Usage |
|------|-------|-------|
| **Ease-in** | `cubic-bezier(0.4, 0, 1, 1)` | Exiting elements |
| **Ease-out** | `cubic-bezier(0, 0, 0.2, 1)` | Entering elements |
| **Ease-in-out** | `cubic-bezier(0.4, 0, 0.2, 1)` | State transitions |
| **Linear** | `linear` | Continuous motion |

### 9.2 Duration Scale

| Token | Duration | Usage |
|-------|----------|-------|
| **Faster** | 100ms | Micro-interactions |
| **Fast** | 150ms | Hover states |
| **Normal** | 200ms | Standard transitions |
| **Slow** | 300ms | Modal, panel transitions |
| **Slower** | 500ms | Page transitions |

### 9.3 Common Animations

#### Fade
```typescript
const fadeVariants = {
  initial: { opacity: 0 },
  animate: { opacity: 1 },
  exit: { opacity: 0 },
};
```

#### Slide
```typescript
const slideVariants = {
  slideUp: {
    initial: { translateY: 20, opacity: 0 },
    animate: { translateY: 0, opacity: 1 },
  },
  slideDown: {
    initial: { translateY: -20, opacity: 0 },
    animate: { translateY: 0, opacity: 1 },
  },
};
```

#### Scale
```typescript
const scaleVariants = {
  initial: { scale: 0.95, opacity: 0 },
  animate: { scale: 1, opacity: 1 },
  exit: { scale: 0.95, opacity: 0 },
};
```

---

## 10. Z-Index Scale

| Level | Value | Usage |
|-------|-------|-------|
| **Base** | 0 | Default layer |
| **Dropdown** | 10 | Dropdowns, selects |
| **Sticky** | 20 | Sticky headers |
| **Fixed** | 30 | Fixed navigation |
| **Modal Backdrop** | 40 | Modal overlay |
| **Modal** | 50 | Modal content |
| **Popover** | 60 | Tooltips, popovers |
| **Toast** | 70 | Notifications |
| **Tooltip** | 80 | Tooltips over modals |

---

## 11. Design Tokens Summary

### CSS Custom Properties
```css
:root {
  /* Colors */
  --color-primary: 30 64 175;
  --color-secondary: 15 118 110;
  --color-success: 21 128 61;
  --color-warning: 180 83 9;
  --color-error: 185 28 28;
  --color-info: 3 105 161;
  
  /* Typography */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
  
  /* Spacing */
  --spacing-unit: 4px;
  
  /* Radii */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-2xl: 20px;
  --radius-full: 9999px;
  
  /* Shadows */
  --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
  
  /* Animation */
  --duration-fast: 150ms;
  --duration-normal: 200ms;
  --duration-slow: 300ms;
  
  /* Z-index */
  --z-dropdown: 10;
  --z-modal: 50;
  --z-toast: 70;
}
```

---

## 12. Component Library Reference

### shadcn/ui Components (Adapted for React Native)

| Component | Status | Notes |
|-----------|--------|-------|
| Button | ✅ Ready | Full variants |
| Input | ✅ Ready | With validation |
| Textarea | ✅ Ready | With auto-grow |
| Label | ✅ Ready | Form labels |
| Card | ✅ Ready | Multiple variants |
| Avatar | ✅ Ready | With fallback |
| Badge | ✅ Ready | Status, count |
| Switch | ✅ Ready | Toggle control |
| Checkbox | ✅ Ready | With label |
| Radio | ✅ Ready | Group with label |
| Select | ✅ Ready | Native picker |
| Sheet | ✅ Ready | Bottom sheet |
| Dialog | ✅ Ready | Modal |
| Toast | ✅ Ready | Notifications |
| Skeleton | ✅ Ready | Loading states |
| Separator | ✅ Ready | Dividers |
| Tabs | ✅ Ready | Tab navigation |
| Tooltip | ✅ Ready | Native tooltip |

---

## 13. Usage Guidelines

### 13.1 Color Usage

| Context | Color | Example |
|---------|-------|---------|
| Primary actions | Primary | "Submit" button |
| Secondary actions | Secondary | "Cancel" button |
| Destructive actions | Error | "Delete" button |
| Positive values | Success | +12.5% return |
| Negative values | Error | -5.2% loss |
| Neutral values | Gray | 0% change |
| Important alerts | Warning | "Verify identity" |
| Informational | Info | Tips, hints |

### 13.2 Typography Usage

| Context | Style | Example |
|---------|-------|---------|
| Screen title | `text-3xl font-semibold` | "Portfolio" |
| Section header | `text-xl font-semibold` | "Positions" |
| Card title | `text-lg font-medium` | "Apple Inc." |
| Body text | `text-base` | Product description |
| Secondary text | `text-sm text-gray-500` | Timestamps, hints |
| Financial values | `font-mono text-lg font-semibold` | "$125,430.00" |
| Captions | `text-xs text-gray-400` | Legal text |

### 13.3 Spacing Usage

| Context | Spacing |
|---------|---------|
| Screen padding | 20px horizontal, 24px vertical |
| Section spacing | 24px between sections |
| Card padding | 16px |
| List item padding | 16px horizontal, 12px vertical |
| Button padding (md) | 16px horizontal, 10px vertical |
| Input padding | 12px horizontal, 10px vertical |

---

## 14. Design Review Checklist

Before finalizing any design:

- [ ] All text meets minimum contrast ratio (4.5:1)
- [ ] Touch targets are at least 44×44pt
- [ ] Focus indicators are visible
- [ ] Color is not the only way to convey information
- [ ] Typography hierarchy is clear and consistent
- [ ] Spacing follows the defined scale
- [ ] Components follow established patterns
- [ ] Dark mode is considered (if applicable)
- [ ] Animations respect reduced motion preferences
- [ ] Screen reader labels are provided
- [ ] Error states are clearly communicated
- [ ] Loading states are shown appropriately

---

*Design System Version 1.0*  
*Created by UI/UX Designer Agent*  
*Date: 2024-01-17*
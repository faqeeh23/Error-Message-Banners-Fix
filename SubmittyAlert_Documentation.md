---
layout: default
title: System Alert Banners (Vue Component)
category: Developer
subcategory: User Interface
---

# System Alert Banners (Vue)

Submitty relies on alert banners to relay critical information to users. To ensure a standardized, accessible, and highly maintainable User Interface, these messages are implemented using the global `SubmittyAlert.vue` component.

## 🚀 Overview

The `SubmittyAlert.vue` component completely decouples alert business logic from raw HTML structures. It dynamically adjusts borders, semantic icons, and accessibility tags based on a single `type` property.

All underlying aesthetic values—including Okabe-Ito colorblind-safe palettes and glassmorphism properties—are maintained directly within the component's scoped styles.

## 📦 How to Use

Whenever you need to render a warning, success, error, or informational message inside a `.twig` or Vue template, wrap your content in the `<SubmittyAlert>` component.

### Basic Implementation

```html
<template>
  <SubmittyAlert type="warning">
    <strong>Warning:</strong> TA Beta Testing starts after submission open date. 
    TAs will not be able to test the assignment before it is released to students.
  </SubmittyAlert>
</template>

<script setup>
import SubmittyAlert from '@/components/SubmittyAlert.vue';
</script>
```

### Supported Alert Types (`type` Prop)

The component accepts a `type` string prop. If omitted, it gracefully defaults to `info`.

1. **`error`** (Deep Red): Used for highly critical warnings, late submission penalties, or system failures.
2. **`warning`** (Golden Orange): Used to warn the user of potential issues or restricted actions.
3. **`success`** (Bluish Green): Used to confirm successful submissions or saved settings.
4. **`info`** (Classic Blue): Used for neutral announcements (e.g., Office Hours queues).

*Note: The actual hex codes mapped to these types are strictly derived from the WCAG AA Colorblind-safe palette defined in the component's scoped styles.*

## 💎 Advanced Features

### 1. Fully Content-Agnostic `<slot>`
You are not restricted to plain text. The inner `<slot>` wrapper allows you to inject links, buttons, or complex HTML structures inside the banner:

```html
<SubmittyAlert type="error">
  <p>Your grade for this assignment will be recorded as a zero.</p>
  <a href="/extensions" class="btn">Request a Deadline Extension</a>
</SubmittyAlert>
```

## 👁️‍🗨️ Accessibility (a11y) Standards
This component implements strict VPAT/WCAG AA principles by default:
- **No Pure-Color Reliance**: It forcefully renders contextual Lucide icons (`CheckCircle`, `AlertTriangle`, etc.) ensuring colorblind users can immediately identify the severity.
- **Screen Reader Only Tags**: Wraps the visual icon with hidden `<span class="sr-only">` textual identifiers announcing the specific alert type to assistive technologies.
- **Aria Live**: Inherits `aria-live="polite"` so screen readers appropriately queue the notification without interrupting critical workflows.

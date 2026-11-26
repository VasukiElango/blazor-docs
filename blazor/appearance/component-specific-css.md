---
layout: post
title: Component-Specific CSS in Blazor Themes | Syncfusion®
description: Learn how to load only the styles required for the components used in your Blazor application using component-specific CSS packages.
platform: Blazor
component: Appearance
documentation: ug
---

# Component-Specific CSS in Blazor Themes

The Syncfusion&reg; Blazor Themes support **component-specific CSS references**. Every supported theme is split into a shared **Base** package and a set of individual **component** packages, so applications can load only the styles required by the components they use.

Instead of referencing a single, all-in-one theme stylesheet, you reference the **Base** stylesheet followed by one stylesheet per component that is rendered in the application. The Base stylesheet must always be loaded first because it provides the common styles, variables, typography, animations, utility classes, and shared component dependencies that every Syncfusion&reg; Blazor component relies on.

## Overview

Each theme is distributed as a set of stylesheets organized into three logical groups:

* **Base package** – A mandatory `base.min.css` stylesheet that contains the shared styles, design tokens (CSS custom properties), typography, animations, utility classes, and styles for components that other components depend on (for example, icons, popup container, ripple effect).
* **Component packages** – One `.min.css` file per Syncfusion&reg; Blazor component that contains the styles specific to that component. Applications reference only the component stylesheets that match the components they render.
* **Lite variants** – Optional optimized builds that use a `-lite` suffix in the stylesheet filename (for example, `base-lite.min.css` and `diagram-lite.min.css`) that omit the bigger size mode styles and provide a reduced CSS footprint while preserving visual consistency.

The standard reference for a single component looks like the following example for the [Blazor Diagram](https://www.syncfusion.com/blazor-components/blazor-diagram) component using the Fluent 2 theme:

```html
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/diagram/diagram.min.css" />
```

The **first** stylesheet (`base.min.css`) is required. The remaining stylesheets are added **only for the components that are actually used** in the application.

## Why use component-specific CSS

Referencing only the required component styles offers the following advantages:

* **Reduced CSS payload** – Avoid loading styles for components that are not used in the application.
* **Faster initial load** – Smaller CSS files mean less data to download, parse, and apply, which improves first-paint and time-to-interactive metrics.
* **Better production hygiene** – The styles referenced in the host page match exactly the components rendered by the application.
* **Predictable upgrades** – New components added to a theme package do not bloat the existing application bundle because each application explicitly references the styles it needs.

N> The component-specific CSS references can be used with all reference methods supported by Syncfusion&reg; Blazor: static web assets, the Syncfusion&reg; CDN, the [Custom Resource Generator (CRG)](https://blazor.syncfusion.com/documentation/common/custom-resource-generator), and [Theme Studio](https://blazor.syncfusion.com/documentation/appearance/theme-studio).

## Component-specific CSS references

Applications reference the **Base** stylesheet once and then add a `<link>` tag only for each component that is rendered. The following examples show the most common scenarios.

### Diagram component

For an application that renders only the [Blazor Diagram](https://www.syncfusion.com/blazor-components/blazor-diagram) component, reference the Base stylesheet and the Diagram component stylesheet:

```html
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/diagram/diagram.min.css" />
```

### Grid component

For an application that renders only the [Blazor DataGrid](https://www.syncfusion.com/blazor-components/blazor-datagrid) component, reference the Base stylesheet and the DataGrid component stylesheet:

```html
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/grid/grid.min.css" />
```

### Multiple components

For an application that uses the [Blazor Button](https://www.syncfusion.com/blazor-components/blazor-button), [Blazor DataGrid](https://www.syncfusion.com/blazor-components/blazor-datagrid), and [Blazor Diagram](https://www.syncfusion.com/blazor-components/blazor-diagram) components together, add a stylesheet for each component after the Base stylesheet:

```html
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/button/button.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/grid/grid.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/diagram/diagram.min.css" />
```

The order of the component stylesheets after `base.min.css` does not matter. The Base stylesheet must always appear first.

## Lite theme support

The component-specific CSS references are available for both **standard** and **lite** theme variants. In lite variants, append `-lite` to the filename (for example, `base-lite.min.css` and `<component>-lite.min.css`) under the theme folder.

### Standard theme example

```html
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/diagram/diagram.min.css" />
```

### Lite theme example

```html
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base-lite.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/diagram/diagram-lite.min.css" />
```

The lite theme variant provides a smaller CSS footprint because it excludes the bigger size mode styles. Use the lite variant when the application does not use the bigger size mode (the `.e-bigger` class). Refer to the [lite theme documentation](https://blazor.syncfusion.com/documentation/appearance/themes#lite-theme-files) for details on when to choose the lite variant.

N> Lite themes preserve the appearance and functionality of Syncfusion&reg; Blazor components while delivering a reduced CSS payload.

## Component-to-CSS reference

For each theme, the stylesheets are published as individual component folders under the theme name inside the `Syncfusion.Blazor.Themes` static web assets. Each component folder contains a `.min.css` stylesheet for the standard variant and a `-lite.min.css` stylesheet for the lite variant.

The following table lists the component-specific CSS packages and their paths. Replace `<THEME-NAME>` with the theme name you are using (for example, `fluent2`, `fluent2-dark`, `material3`, `bootstrap5.3`, `tailwind3`, or `highcontrast`). For lite variants, replace `.min.css` with `-lite.min.css` (for example, `base-lite.min.css` or `grid-lite.min.css`).

<table>
  <thead>
    <tr>
      <th style="width:30%">Component</th>
      <th style="width:35%">Standard stylesheet path</th>
      <th style="width:35%">Lite stylesheet path</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Base (mandatory)</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/base/base.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/base/base-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Accordion</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/accordion/accordion.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/accordion/accordion-lite.min.css</code></td>
    </tr>
    <tr>
      <td>AI AssistView</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/ai-assistview/ai-assistview.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/ai-assistview/ai-assistview-lite.min.css</code></td>
    </tr>
    <tr>
      <td>AppBar</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/appbar/appbar.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/appbar/appbar-lite.min.css</code></td>
    </tr>
    <tr>
      <td>AutoComplete</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/auto-complete/auto-complete.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/auto-complete/auto-complete-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Avatar</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/avatar/avatar.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/avatar/avatar-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Badge</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/badge/badge.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/badge/badge-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Barcode</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/barcode/barcode.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/barcode/barcode-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Block Editor</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/blockeditor/blockeditor.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/blockeditor/blockeditor-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Breadcrumb</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/breadcrumb/breadcrumb.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/breadcrumb/breadcrumb-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Button</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/button/button.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/button/button-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Button Group</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/button-group/button-group.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/button-group/button-group-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Calendar</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/calendar/calendar.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/calendar/calendar-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Card</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/card/card.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/card/card-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Carousel</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/carousel/carousel.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/carousel/carousel-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Chat UI</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/chat-ui/chat-ui.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/chat-ui/chat-ui-lite.min.css</code></td>
    </tr>
    <tr>
      <td>CheckBox</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/check-box/check-box.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/check-box/check-box-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Chips</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/chips/chips.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/chips/chips-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Color Picker</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/color-picker/color-picker.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/color-picker/color-picker-lite.min.css</code></td>
    </tr>
    <tr>
      <td>ComboBox</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/combo-box/combo-box.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/combo-box/combo-box-lite.min.css</code></td>
    </tr>
    <tr>
      <td>ContextMenu</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/context-menu/context-menu.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/context-menu/context-menu-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Dashboard Layout</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/dashboard-layout/dashboard-layout.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/dashboard-layout/dashboard-layout-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Data Form</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/data-form/data-form.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/data-form/data-form-lite.min.css</code></td>
    </tr>
    <tr>
      <td>DatePicker</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/datepicker/datepicker.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/datepicker/datepicker-lite.min.css</code></td>
    </tr>
    <tr>
      <td>DateRangePicker</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/daterangepicker/daterangepicker.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/daterangepicker/daterangepicker-lite.min.css</code></td>
    </tr>
    <tr>
      <td>DateTimePicker</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/datetimepicker/datetimepicker.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/datetimepicker/datetimepicker-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Diagram</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/diagram/diagram.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/diagram/diagram-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Dialog</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/dialog/dialog.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/dialog/dialog-lite.min.css</code></td>
    </tr>
    <tr>
      <td>DocumentEditor</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/document-editor/document-editor.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/document-editor/document-editor-lite.min.css</code></td>
    </tr>
    <tr>
      <td>DropDownButton</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/drop-down-button/drop-down-button.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/drop-down-button/drop-down-button-lite.min.css</code></td>
    </tr>
    <tr>
      <td>DropDownList</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/drop-down-list/drop-down-list.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/drop-down-list/drop-down-list-lite.min.css</code></td>
    </tr>
    <tr>
      <td>DropDownTree</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/drop-down-tree/drop-down-tree.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/drop-down-tree/drop-down-tree-lite.min.css</code></td>
    </tr>
    <tr>
      <td>FileManager</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/file-manager/file-manager.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/file-manager/file-manager-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Floating Action Button</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/floating-action-button/floating-action-button.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/floating-action-button/floating-action-button-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Form Renderer</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/form-renderer/form-renderer.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/form-renderer/form-renderer-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Gantt</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/gantt/gantt.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/gantt/gantt-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Grid</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/grid/grid.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/grid/grid-lite.min.css</code></td>
    </tr>
    <tr>
      <td>ImageEditor</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/image-editor/image-editor.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/image-editor/image-editor-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Inline AI Assist</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/inline-ai-assist/inline-ai-assist.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/inline-ai-assist/inline-ai-assist-lite.min.css</code></td>
    </tr>
    <tr>
      <td>In-place Editor</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/inplace-editor/inplace-editor.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/inplace-editor/inplace-editor-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Input</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/input/input.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/input/input-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Kanban</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/kanban/kanban.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/kanban/kanban-lite.min.css</code></td>
    </tr>
    <tr>
      <td>ListBox</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/list-box/list-box.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/list-box/list-box-lite.min.css</code></td>
    </tr>
    <tr>
      <td>ListView</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/list-view/list-view.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/list-view/list-view-lite.min.css</code></td>
    </tr>
    <tr>
      <td>MaskedTextBox</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/maskedtextbox/maskedtextbox.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/maskedtextbox/maskedtextbox-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Mention</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/mention/mention.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/mention/mention-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Menu</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/menu/menu.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/menu/menu-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Message</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/message/message.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/message/message-lite.min.css</code></td>
    </tr>
    <tr>
      <td>MultiColumn ComboBox</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/multicolumn-combobox/multicolumn-combobox.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/multicolumn-combobox/multicolumn-combobox-lite.min.css</code></td>
    </tr>
    <tr>
      <td>MultiSelect</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/multi-select/multi-select.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/multi-select/multi-select-lite.min.css</code></td>
    </tr>
    <tr>
      <td>NumericTextBox</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/numerictextbox/numerictextbox.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/numerictextbox/numerictextbox-lite.min.css</code></td>
    </tr>
    <tr>
      <td>OTP Input</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/otp-input/otp-input.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/otp-input/otp-input-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Pager</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/pager/pager.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/pager/pager-lite.min.css</code></td>
    </tr>
    <tr>
      <td>PDF Viewer</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/pdfviewer/pdfviewer.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/pdfviewer/pdfviewer-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Pivot Table</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/pivotview/pivotview.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/pivotview/pivotview-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Popup</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/popup/popup.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/popup/popup-lite.min.css</code></td>
    </tr>
    <tr>
      <td>ProgressButton</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/progress-button/progress-button.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/progress-button/progress-button-lite.min.css</code></td>
    </tr>
    <tr>
      <td>QueryBuilder</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/query-builder/query-builder.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/query-builder/query-builder-lite.min.css</code></td>
    </tr>
    <tr>
      <td>RadioButton</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/radio-button/radio-button.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/radio-button/radio-button-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Rating</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/rating/rating.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/rating/rating-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Ribbon</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/ribbon/ribbon.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/ribbon/ribbon-lite.min.css</code></td>
    </tr>
    <tr>
      <td>RichTextEditor</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/rich-text-editor/rich-text-editor.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/rich-text-editor/rich-text-editor-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Scheduler</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/schedule/schedule.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/schedule/schedule-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Sidebar</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/sidebar/sidebar.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/sidebar/sidebar-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Signature</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/signature/signature.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/signature/signature-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Skeleton</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/skeleton/skeleton.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/skeleton/skeleton-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Slider</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/slider/slider.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/slider/slider-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Smart TextArea</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/smart-textarea/smart-textarea.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/smart-textarea/smart-textarea-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Speech To Text</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/speech-to-text/speech-to-text.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/speech-to-text/speech-to-text-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Speed Dial</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/speed-dial/speed-dial.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/speed-dial/speed-dial-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Spinner</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/spinner/spinner.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/spinner/spinner-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Split Button</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/split-button/split-button.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/split-button/split-button-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Splitter</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/splitter/splitter.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/splitter/splitter-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Spreadsheet</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/spreadsheet/spreadsheet.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/spreadsheet/spreadsheet-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Stepper</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/stepper/stepper.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/stepper/stepper-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Switch</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/switch/switch.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/switch/switch-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Tab</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/tab/tab.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/tab/tab-lite.min.css</code></td>
    </tr>
    <tr>
      <td>TextArea</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/textarea/textarea.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/textarea/textarea-lite.min.css</code></td>
    </tr>
    <tr>
      <td>TextBox</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/textbox/textbox.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/textbox/textbox-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Timeline</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/timeline/timeline.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/timeline/timeline-lite.min.css</code></td>
    </tr>
    <tr>
      <td>TimePicker</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/timepicker/timepicker.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/timepicker/timepicker-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Toast</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/toast/toast.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/toast/toast-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Toolbar</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/toolbar/toolbar.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/toolbar/toolbar-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Tooltip</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/tooltip/tooltip.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/tooltip/tooltip-lite.min.css</code></td>
    </tr>
    <tr>
      <td>TreeGrid</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/treegrid/treegrid.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/treegrid/treegrid-lite.min.css</code></td>
    </tr>
    <tr>
      <td>TreeView</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/treeview/treeview.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/treeview/treeview-lite.min.css</code></td>
    </tr>
    <tr>
      <td>Uploader</td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/uploader/uploader.min.css</code></td>
      <td><code>_content/Syncfusion.Blazor.Themes/&lt;THEME-NAME&gt;/uploader/uploader-lite.min.css</code></td>
    </tr>
  </tbody>
</table>

## Where to reference the styles

Add the Base and component-specific `<link>` tags to the host page of your application. The exact file depends on the Blazor application model:

* For a **Blazor Web App** using **Server**, **WebAssembly**, or **Auto** interactive render modes, add the references in the `<head>` section of **`~/Components/App.razor`**.
* For a **Blazor WebAssembly standalone app**, add the references in the `<head>` section of **`~/wwwroot/index.html`**.

The following example shows a Blazor Web App that renders the [Blazor Diagram](https://www.syncfusion.com/blazor-components/blazor-diagram), [Blazor DataGrid](https://www.syncfusion.com/blazor-components/blazor-datagrid), and [Blazor Button](https://www.syncfusion.com/blazor-components/blazor-button) components using the Fluent 2 theme:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <base href="/" />

    <!-- Syncfusion Blazor Themes: Base (mandatory) + components used by this app -->
    <link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base.min.css" />
    <link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/button/button.min.css" />
    <link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/grid/grid.min.css" />
    <link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/diagram/diagram.min.css" />
</head>
<body>
    ...
</body>
</html>
```

To use the lite variants instead, reference the `-lite.min.css` files:

```html
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/base/base-lite.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/button/button-lite.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/grid/grid-lite.min.css" />
<link rel="stylesheet" href="_content/Syncfusion.Blazor.Themes/fluent2/diagram/diagram-lite.min.css" />
```

To ensure the host can serve the static web assets, verify that [UseStaticFiles](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles) is called in `~/Program.cs`. For a **Blazor Web App**, this is required in the server project. A standalone **Blazor WebAssembly** app does not require any server-side middleware configuration.

## CDN reference

The component-specific CSS packages are also available on the Syncfusion&reg; CDN under the theme folder. Replace the static web asset path with the CDN URL, keeping the same `base/<component>/<file>` layout:

```html
<link rel="stylesheet" href="https://cdn.syncfusion.com/blazor/{{ site.blazorversion }}/styles/fluent2/base/base.min.css" />
<link rel="stylesheet" href="https://cdn.syncfusion.com/blazor/{{ site.blazorversion }}/styles/fluent2/diagram/diagram.min.css" />
```

For lite variants, reference the `-lite.min.css` files under the theme folder:

```html
<link rel="stylesheet" href="https://cdn.syncfusion.com/blazor/{{ site.blazorversion }}/styles/fluent2/base/base-lite.min.css" />
<link rel="stylesheet" href="https://cdn.syncfusion.com/blazor/{{ site.blazorversion }}/styles/fluent2/diagram/diagram-lite.min.css" />
```

N> Ensure that the version in the CDN URL matches the version of the [Syncfusion.Blazor.Themes](https://www.nuget.org/packages/Syncfusion.Blazor.Themes/) NuGet package referenced by your application.

## See also

* [Apply and Customize Blazor Themes](https://blazor.syncfusion.com/documentation/appearance/themes)
* [Change Theme Dynamically in Blazor Applications](https://blazor.syncfusion.com/documentation/appearance/dynamic-theme-switching)
* [Enable Touch Friendly Size Modes in Blazor](https://blazor.syncfusion.com/documentation/appearance/size-modes)
* [Custom Resource Generator (CRG)](https://blazor.syncfusion.com/documentation/common/custom-resource-generator)
* [Theme Studio](https://blazor.syncfusion.com/documentation/appearance/theme-studio)

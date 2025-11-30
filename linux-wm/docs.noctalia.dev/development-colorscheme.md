---
url: https://docs.noctalia.dev/development/colorscheme/
title: Create a Predefined Color Scheme | Noctalia Docs
source_domain: docs.noctalia.dev
---

# Create a Predefined Color Scheme | Noctalia Docs

# Create a Predefined Color Scheme

This guide walks you through adding a new **predefined color scheme** to **Noctalia**.

---

## Overview

[Section titled “Overview”](https://docs.noctalia.dev/development/colorscheme/#overview)

Adding a new predefined color scheme involves five steps:

1. [Create the scheme directory](https://docs.noctalia.dev/development/colorscheme/#step-1-create-the-scheme-directory)
2. [Create the main scheme file](https://docs.noctalia.dev/development/colorscheme/#step-2-create-the-main-scheme-file)
3. [Create terminal themes](https://docs.noctalia.dev/development/colorscheme/#step-3-create-terminal-themes)
4. [Test your scheme](https://docs.noctalia.dev/development/colorscheme/#step-4-test-your-scheme)

---

Important: Repository for PRs

Pull requests for new color schemes should be submitted to the [noctalia-colorschemes](https://github.com/noctalia-dev/noctalia-colorschemes) repository, not the main noctalia-shell repository.

---

## Step 1: Create the Scheme Directory

[Section titled “Step 1: Create the Scheme Directory”](https://docs.noctalia.dev/development/colorscheme/#step-1-create-the-scheme-directory)

Create a new directory in the ColorScheme assets folder:

**`Assets/ColorScheme/YourSchemeName/`**

For example, if you’re creating a “Monokai” scheme:

**`Assets/ColorScheme/Monokai/`**

---

## Step 2: Create the Main Scheme File

[Section titled “Step 2: Create the Main Scheme File”](https://docs.noctalia.dev/development/colorscheme/#step-2-create-the-main-scheme-file)

Create the main scheme file named after your scheme:

**`Assets/ColorScheme/Monokai/Monokai.json`**

```
{

"dark": {

"mPrimary": "#a6e22e",

"mOnPrimary": "#272822",

"mSecondary": "#66d9ef",

"mOnSecondary": "#272822",

"mTertiary": "#f92672",

"mOnTertiary": "#272822",

"mError": "#f92672",

"mOnError": "#272822",

"mSurface": "#272822",

"mOnSurface": "#f8f8f2",

"mHover": "#3a3a32",

"mOnHover": "#f8f8f2",

"mSurfaceVariant": "#3e3d32",

"mOnSurfaceVariant": "#a6e22e",

"mOutline": "#75715e",

"mShadow": "#272822"

},

"light": {

"mPrimary": "#a6e22e",

"mOnPrimary": "#f8f8f2",

"mSecondary": "#66d9ef",

"mOnSecondary": "#f8f8f2",

"mTertiary": "#f92672",

"mOnTertiary": "#f8f8f2",

"mError": "#f92672",

"mOnError": "#f8f8f2",

"mSurface": "#f8f8f2",

"mOnSurface": "#272822",

"mHover": "#e6e1dc",

"mOnHover": "#272822",

"mSurfaceVariant": "#e6e1dc",

"mOnSurfaceVariant": "#272822",

"mOutline": "#a6e22e",

"mShadow": "#d8d8d8"

}

}
```

### Color Properties Explained

[Section titled “Color Properties Explained”](https://docs.noctalia.dev/development/colorscheme/#color-properties-explained)

Each color scheme must define both `dark` and `light` variants with these Material Design 3 properties:

* **`mPrimary`** - Primary color (buttons, links, highlights)
* **`mOnPrimary`** - Text/icon color on primary surfaces
* **`mSecondary`** - Secondary accent color
* **`mOnSecondary`** - Text/icon color on secondary surfaces
* **`mTertiary`** - Tertiary accent color
* **`mOnTertiary`** - Text/icon color on tertiary surfaces
* **`mError`** - Error/warning color
* **`mOnError`** - Text/icon color on error surfaces
* **`mSurface`** - Main background color
* **`mOnSurface`** - Primary text color
* **`mHover`** - Hover-state surface color for interactive elements
* **`mOnHover`** - Text/icon color on hover surfaces
* **`mSurfaceVariant`** - Secondary background color (cards, panels)
* **`mOnSurfaceVariant`** - Text color on surface variants
* **`mOutline`** - Border/divider color
* **`mShadow`** - Shadow color

### Color Selection Guidelines

[Section titled “Color Selection Guidelines”](https://docs.noctalia.dev/development/colorscheme/#color-selection-guidelines)

1. **Primary Color**: Choose a distinctive color that represents your scheme’s character
2. **Secondary/Tertiary**: Use complementary colors that work well with the primary
3. **Surface Colors**: Ensure good contrast for readability
4. **Error Color**: Typically red-based for universal recognition
5. **Outline Colors**: Should provide subtle separation without being distracting

---

## Step 3: Create Terminal Themes

[Section titled “Step 3: Create Terminal Themes”](https://docs.noctalia.dev/development/colorscheme/#step-3-create-terminal-themes)

Create terminal-specific themes for better contrast and readability. Terminal themes bypass the Material Design 3 generation and use your scheme’s colors directly.

### Directory Structure

[Section titled “Directory Structure”](https://docs.noctalia.dev/development/colorscheme/#directory-structure)

Create terminal theme directories:

```
Assets/ColorScheme/Monokai/

├── Monokai.json

└── terminal/

├── foot/

│   ├── Monokai-dark

│   └── Monokai-light

├── ghostty/

│   ├── Monokai-dark

│   └── Monokai-light

└── kitty/

├── Monokai-dark.conf

└── Monokai-light.conf
```

### Foot Terminal Theme

[Section titled “Foot Terminal Theme”](https://docs.noctalia.dev/development/colorscheme/#foot-terminal-theme)

**`Assets/ColorScheme/Monokai/terminal/foot/Monokai-dark`**

```
[colors]

background=272822

foreground=f8f8f2

# Normal colors

regular0=272822

regular1=f92672

regular2=a6e22e

regular3=f4bf75

regular4=66d9ef

regular5=ae81ff

regular6=a1efe4

regular7=f8f8f2

# Bright colors

bright0=75715e

bright1=f92672

bright2=a6e22e

bright3=f4bf75

bright4=66d9ef

bright5=ae81ff

bright6=a1efe4

bright7=f9f8f5

[cursor]

color=f8f8f2 272822
```

### Ghostty Terminal Theme

[Section titled “Ghostty Terminal Theme”](https://docs.noctalia.dev/development/colorscheme/#ghostty-terminal-theme)

**`Assets/ColorScheme/Monokai/terminal/ghostty/Monokai-dark`**

```
[colors]

background=272822

foreground=f8f8f2

# Normal colors

regular0=272822

regular1=f92672

regular2=a6e22e

regular3=f4bf75

regular4=66d9ef

regular5=ae81ff

regular6=a1efe4

regular7=f8f8f2

# Bright colors

bright0=75715e

bright1=f92672

bright2=a6e22e

bright3=f4bf75

bright4=66d9ef

bright5=ae81ff

bright6=a1efe4

bright7=f9f8f5

[cursor]

color=f8f8f2 272822
```

### Kitty Terminal Theme

[Section titled “Kitty Terminal Theme”](https://docs.noctalia.dev/development/colorscheme/#kitty-terminal-theme)

**`Assets/ColorScheme/Monokai/terminal/kitty/Monokai-dark.conf`**

```
color0 #272822

color1 #f92672

color2 #a6e22e

color3 #f4bf75

color4 #66d9ef

color5 #ae81ff

color6 #a1efe4

color7 #f8f8f2

color8 #75715e

color9 #f92672

color10 #a6e22e

color11 #f4bf75

color12 #66d9ef

color13 #ae81ff

color14 #a1efe4

color15 #f9f8f5

background #272822

selection_foreground #272822

cursor #f8f8f2

cursor_text_color #272822

foreground #f8f8f2

selection_background #f8f8f2
```

### Terminal Color Mapping

[Section titled “Terminal Color Mapping”](https://docs.noctalia.dev/development/colorscheme/#terminal-color-mapping)

Terminal themes use a standard 16-color palette:

* **colors 0-7**: Normal colors (dark background variants)
* **colors 8-15**: Bright colors (lighter variants)
* **background**: Terminal background
* **foreground**: Primary text color
* **cursor**: Cursor color and text color
* **selection\_foreground/background**: Text selection colors

---

## Step 4: Test Your Scheme

[Section titled “Step 4: Test Your Scheme”](https://docs.noctalia.dev/development/colorscheme/#step-4-test-your-scheme)

1. **Place your scheme files** in the correct directories
2. **Restart Noctalia** to load the new scheme
3. **Open settings** and navigate to Color Scheme
4. **Select your scheme** from the predefined schemes list
5. **Test both dark and light modes**
6. **Verify terminal themes** work correctly
7. **Check Material Design 3 generation** if you have templates enabled

### Testing Checklist

[Section titled “Testing Checklist”](https://docs.noctalia.dev/development/colorscheme/#testing-checklist)

* Scheme appears in the predefined schemes list
* Dark mode variant works correctly
* Light mode variant works correctly
* Terminal themes apply correctly
* Material Design 3 templates generate properly
* Colors have good contrast and readability
* Scheme name displays correctly

---

## Step 5: Add Translations

[Section titled “Step 5: Add Translations”](https://docs.noctalia.dev/development/colorscheme/#step-5-add-translations)

Add translations for your scheme name in the translation files:

**`Assets/Translations/en.json`**

```
{

"color-scheme": {

"predefined": {

"schemes": {

"Monokai": "Monokai"

}

}

}

}
```

**`Assets/Translations/fr.json`**

```
{

"color-scheme": {

"predefined": {

"schemes": {

"Monokai": "Monokai"

}

}

}

}
```

Add translations for all supported languages:

* `en.json` (English)
* `fr.json` (French)
* `de.json` (German)
* `es.json` (Spanish)
* `pt.json` (Portuguese)
* `zh-CN.json` (Chinese Simplified)

---

## How Predefined Schemes Work

[Section titled “How Predefined Schemes Work”](https://docs.noctalia.dev/development/colorscheme/#how-predefined-schemes-work)

### Color Generation Process

[Section titled “Color Generation Process”](https://docs.noctalia.dev/development/colorscheme/#color-generation-process)

When a predefined scheme is selected:

1. **Scheme Loading**: The system loads your `SchemeName.json` file
2. **Variant Selection**: Chooses `dark` or `light` variant based on current mode
3. **Material Design 3 Generation**: Uses `ColorsConvert.js` to generate a complete Material Design 3 palette
4. **Template Processing**: Applies colors to enabled Matugen templates
5. **Terminal Theme Application**: Uses terminal-specific themes for better contrast

### Material Design 3 Palette Generation

[Section titled “Material Design 3 Palette Generation”](https://docs.noctalia.dev/development/colorscheme/#material-design-3-palette-generation)

The system automatically generates complementary colors:

* **Container Colors**: Lighter/darker variants of primary colors
* **“On” Colors**: High-contrast text colors for each surface
* **Surface Variants**: Progressive elevation levels
* **Outline Colors**: Border and divider colors
* **Shadow Colors**: Drop shadow colors

### Terminal Theme Special Handling

[Section titled “Terminal Theme Special Handling”](https://docs.noctalia.dev/development/colorscheme/#terminal-theme-special-handling)

Terminal themes bypass Material Design 3 generation and use your scheme’s colors directly for optimal readability and contrast.

---

## Color Scheme Design Tips

[Section titled “Color Scheme Design Tips”](https://docs.noctalia.dev/development/colorscheme/#color-scheme-design-tips)

### Choosing Colors

[Section titled “Choosing Colors”](https://docs.noctalia.dev/development/colorscheme/#choosing-colors)

1. **Start with a Base**: Choose 2-3 core colors that define your scheme’s character
2. **Consider Accessibility**: Ensure sufficient contrast ratios (WCAG AA minimum)
3. **Test Both Modes**: Dark and light variants should both be usable
4. **Think About Usage**: Consider how colors will look in different contexts

### Popular Color Scheme Sources

[Section titled “Popular Color Scheme Sources”](https://docs.noctalia.dev/development/colorscheme/#popular-color-scheme-sources)

* **Existing Themes**: Adapt popular themes (Dracula, Nord, Catppuccin)
* **Design Systems**: Use established design system color palettes
* **Nature Inspiration**: Draw colors from natural environments

### Tools for Color Selection

[Section titled “Tools for Color Selection”](https://docs.noctalia.dev/development/colorscheme/#tools-for-color-selection)

* **Color Pickers**: Use tools like Coolors.co or Adobe Color
* **Contrast Checkers**: Verify accessibility with WebAIM contrast checker
* **Preview Tools**: Test colors in actual applications
* **Terminal Testing**: Verify terminal themes work well for coding

---

## Troubleshooting

[Section titled “Troubleshooting”](https://docs.noctalia.dev/development/colorscheme/#troubleshooting)

### Common Issues

[Section titled “Common Issues”](https://docs.noctalia.dev/development/colorscheme/#common-issues)

1. **Scheme Not Appearing**: Check file naming and directory structure
2. **Colors Not Applying**: Verify JSON syntax and color format
3. **Poor Contrast**: Use contrast checking tools to verify readability
4. **Terminal Themes Broken**: Check terminal-specific file formats
5. **Translation Missing**: Ensure scheme name is in all translation files

### Debug Tips

[Section titled “Debug Tips”](https://docs.noctalia.dev/development/colorscheme/#debug-tips)

1. **Check Logs**: Look for color scheme loading errors in Noctalia logs
2. **Validate JSON**: Use JSON validators to check syntax
3. **Test Incrementally**: Add one component at a time
4. **Compare Working Schemes**: Use existing schemes as references

---

Terminal Themes

Terminal themes are crucial for developer workflows. Ensure your terminal colors provide excellent readability and syntax highlighting support.

Accessibility

Always verify that your color scheme meets accessibility guidelines, especially for users with visual impairments.
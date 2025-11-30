---
url: https://docs.noctalia.dev/configuration/advanced-app-theming/
title: Advanced App Theming | Noctalia Docs
source_domain: docs.noctalia.dev
---

# Advanced App Theming | Noctalia Docs

# Advanced App Theming

Noctalia includes powerful theming capabilities that can automatically apply your chosen color scheme to various applications. Whether you’re using colors from your wallpaper or a predefined scheme, Noctalia can keep your entire desktop consistent.It also includes some advanced features for you to use.

## Advanced: Custom Templates

[Section titled “Advanced: Custom Templates”](https://docs.noctalia.dev/configuration/advanced-app-theming/#advanced-custom-templates)

For advanced users who want to theme additional applications, Noctalia supports custom Matugen templates.

### Enabling Custom Templates

[Section titled “Enabling Custom Templates”](https://docs.noctalia.dev/configuration/advanced-app-theming/#enabling-custom-templates)

1. Go to **Settings → Color Scheme → Templates**
2. Scroll to **Misc** section
3. Enable **User templates**
4. A template file will be created at `~/.config/noctalia/user-templates.toml`

### Creating Your Own Templates

[Section titled “Creating Your Own Templates”](https://docs.noctalia.dev/configuration/advanced-app-theming/#creating-your-own-templates)

Edit `~/.config/noctalia/user-templates.toml` to add your custom templates:

```
[config]

# Example: Theme Alacritty terminal

[templates.alacritty]

input_path = "~/.config/noctalia/templates/alacritty.toml"

output_path = "~/.config/alacritty/colors.toml"

post_hook = "echo 'Alacritty theme updated'"
```

### Template File Format

[Section titled “Template File Format”](https://docs.noctalia.dev/configuration/advanced-app-theming/#template-file-format)

Your template files use Matugen’s template syntax with color placeholders:

```
/* Example CSS template */

.my-app {

background: {{colors.surface.default.hex}};

color: {{colors.on_surface.default.hex}};

accent: {{colors.primary.default.hex}};

}
```

### Available Color Variables

[Section titled “Available Color Variables”](https://docs.noctalia.dev/configuration/advanced-app-theming/#available-color-variables)

Matugen generates a full Material Design 3 color palette with many color roles like `primary`, `secondary`, `tertiary`, `surface`, `error`, and more.

For a complete list of all available colors and formats, see the [Matugen Configuration Documentation](https://github.com/InioX/matugen/wiki/Configuration#colors).

You can also look at Noctalia’s built-in templates in `Assets/MatugenTemplates/` for practical examples.

### Template Workflow

[Section titled “Template Workflow”](https://docs.noctalia.dev/configuration/advanced-app-theming/#template-workflow)

1. **Create template file** anywhere you like (e.g., `~/.config/matugen/templates/myapp.css` or `~/myapp-template.css`)
2. **Add color placeholders** using the syntax above
3. **Configure in user-templates.toml** with input/output paths
4. **Optional: Add post\_hook** to reload the app after theming
5. **Change your color scheme** and the template will be processed automatically

### Post Hooks

[Section titled “Post Hooks”](https://docs.noctalia.dev/configuration/advanced-app-theming/#post-hooks)

Post hooks run commands after generating a theme, useful for reloading applications:

```
[templates.neovim]

input_path = "~/.config/matugen/templates/neovim-colors.lua"

output_path = "~/.config/nvim/colors/noctalia.lua"

post_hook = "echo 'Neovim theme updated - restart Neovim to apply'"
```

## Troubleshooting

[Section titled “Troubleshooting”](https://docs.noctalia.dev/configuration/advanced-app-theming/#troubleshooting)

### Theme Not Applying

[Section titled “Theme Not Applying”](https://docs.noctalia.dev/configuration/advanced-app-theming/#theme-not-applying)

* **Restart the application** - Some apps need a restart to load new themes
* **Verify template syntax** - Invalid syntax will prevent theme generation

### Colors Look Wrong

[Section titled “Colors Look Wrong”](https://docs.noctalia.dev/configuration/advanced-app-theming/#colors-look-wrong)

* **Light/Dark mode** - Check if your color scheme setting matches your preference
* **Matugen not installed** - Wallpaper colors require `matugen` package
* **Application limitations** - Some apps may not support all color properties

### Custom Templates Not Working

[Section titled “Custom Templates Not Working”](https://docs.noctalia.dev/configuration/advanced-app-theming/#custom-templates-not-working)

* **File paths** - Use absolute paths or `~` for home directory
* **TOML syntax** - Validate your `user-templates.toml` syntax
* **Check logs** - Run Noctalia from terminal to see error messages

## Manual Theme Application

[Section titled “Manual Theme Application”](https://docs.noctalia.dev/configuration/advanced-app-theming/#manual-theme-application)

If you need to manually trigger theme regeneration:

1. Change any color scheme setting in Noctalia
2. Toggle between wallpaper colors and predefined schemes
3. Switch dark/light mode

## Getting Help

[Section titled “Getting Help”](https://docs.noctalia.dev/configuration/advanced-app-theming/#getting-help)

For theming support:

* Check [Matugen documentation](https://github.com/InioX/matugen) for template syntax
* Visit our [GitHub Issues](https://github.com/noctalia-dev/noctalia-shell/issues)
* Join our [Discord](https://discord.noctalia.dev) community
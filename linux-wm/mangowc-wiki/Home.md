- [Config path](#config-path)
  - [using the default config path](#using-the-default-config-path)
  - [sub config](#sub-config)
  - [custom config path](#custom-config-path)
- [Window Effects Configuration](#window-effects-configuration)
- [Animation Configuration](#animation-configuration)
- [Scroller Layout Settings](#scroller-layout-settings)
- [Master-Stack Layout Settings](#master-stack-layout-settings)
- [Overview Settings](#overview-settings)
  - [A More Detailed Explanation](#a-more-detailed-explanation)
  - [Notice](#notice)
- [Miscellaneous Settings](#miscellaneous-settings)
- [Keyboard Settings](#keyboard-settings)
- [Trackpad Settings \& Mouse Settings](#trackpad-settings--mouse-settings)
- [Appearance Settings](#appearance-settings)
- [Tag Rules](#tag-rules)
  - [support layout\_name](#support-layout_name)
  - [example](#example)
- [Layer Rules](#layer-rules)
- [Window Rules](#window-rules)
- [Monitor Rules](#monitor-rules)
- [Env setting](#env-setting)
- [Exec setting](#exec-setting)
- [Key Bindings](#key-bindings)
  - [format](#format)
  - [bind flag](#bind-flag)
  - [Key mode](#key-mode)
  - [Available Commands](#available-commands)
- [Reload Config Bind](#reload-config-bind)
- [Mouse Bindings](#mouse-bindings)
- [Axis Bindings](#axis-bindings)
- [Switch Bindings](#switch-bindings)
- [Gesture Bindings](#gesture-bindings)
- [Keyboard layout and IME](#keyboard-layout-and-ime)
  - [ime env for fcitx5](#ime-env-for-fcitx5)
- [Waybar for mango](#waybar-for-mango)
  - [config](#config)
  - [style.css](#stylecss)
- [Custom animation](#custom-animation)
- [More Monitor Settings](#more-monitor-settings)
- [Tearing(Game mode)](#tearinggame-mode)
- [Screen Scale](#screen-scale)
  - [not use global scale(recommended)](#not-use-global-scalerecommended)
- [Scratchpad](#scratchpad)
  - [sway like scratchpad](#sway-like-scratchpad)
  - [Named Scratchpad](#named-scratchpad)
- [Ipc](#ipc)
- [Virtual Monitor](#virtual-monitor)
- [screen record or share(obs or wemeet)](#screen-record-or-shareobs-or-wemeet)
- [clipboard](#clipboard)
- [file picker(file selector)](#file-pickerfile-selector)
- [Keyring](#keyring)
- [some config I suggest.](#some-config-i-suggest)
- [Question and Answer(High-frequency)](#question-and-answerhigh-frequency)


## Config path

### using the default config path

- the default config path is `~/.config/mango/config.conf`

- the default autostart path is `~/.config/mango/autostart.sh`

- the fallback config path is in `/etc/mango/config.conf`, you can find the default config here

```sh
cp /etc/mango/config.conf ~/.config/mango/config.conf
touch ~/.config/mango/autostart.sh
chmod +x ~/.config/mango/autostart.sh
```

### sub config
you can use `source` keyword to include other config file.
```conf
# absolute path
source=~/.config/mango/bind.conf
# relative path
source=./bind.conf
```

### custom config path
you can use `MANGOCONFIG` env to set the config-folder-path and the autostart-folder-patch
for example, start mango with `MANGOCONFIG` env
```bash
# config path is /home/xxx/config.conf
# autostart path is /home/xxx/autostart.sh
MANGOCONFIG=/home/xxx/ mango
```

## Window Effects Configuration
- `blur` Has a relatively high impact on computer performance. If your computer's hardware is lacking, it is not recommended to enable it.
- `blur_optimized` Will cache wallpaper and blur backgroup, significantly reducing gpu usage. Disabling it will significantly increase gpu consumption and may cause rendering lag.

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `blur` | integer | 0 | Enable window blur (0-disable, 1-enable) |
| `blur_layer` | integer | 0 | Enable layer blur (0-disable, 1-enable) |
| `blur_optimized` | integer | 1 | Enable blur background cache (0-disable, 1-enable) |
| `blur_params_num_passes` | integer | 2 | Number of blur passes |
| `blur_params_radius` | integer | 5 | Blur radius |
| `blur_params_noise` | float | 0.02 | Blur noise level |
| `blur_params_brightness` | float | 0.9 | Blur brightness adjustment |
| `blur_params_contrast` | float | 0.9 | Blur contrast adjustment |
| `blur_params_saturation` | float | 1.2 | Blur saturation adjustment |
| `shadows` | integer | 0 | Enable window shadows (0-disable, 1-enable) |
| `shadow_only_floating` | integer | 1 | Only draw shadows for floating windows (0-disable, 1-enable) |
| `layer_shadows` | integer | 0 | Enable layer shadows (0-disable, 1-enable) |
| `shadows_size` | integer | 10 | Shadow size |
| `shadows_blur` | integer | 15 | Shadow blur amount |
| `shadows_position_x` | integer | 0 | Shadow X offset |
| `shadows_position_y` | integer | 0 | Shadow Y offset |
| `shadowscolor` | hex color | 0x000000ff | Shadow color (ARGB format) |
| `border_radius` | integer | 6 | Window border radius |
| `no_radius_when_single` | integer | 0 | Disable radius when single window (0-disable, 1-enable) |
| `focused_opacity` | float | 1.0 | Opacity of focused window (0.0-1.0) |
| `unfocused_opacity` | float | 1.0 | Opacity of unfocused window (0.0-1.0) |

## Animation Configuration

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `animations` | integer | 1 | Enable animations (0-disable, 1-enable) |
| `layer_animations` | integer | 0 | Enable layer animations (0-disable, 1-enable) |
| `animation_type_open` | string | slide | Open animation type (zoom, slide, fade, none) |
| `animation_type_close` | string | slide | Close animation type (zoom, slide, fade, none) |
| `layer_animation_type_open` | string | slide | Open layer animation type (slide,zoom, fade, none) |
| `layer_animation_type_close` | string | slide | Close layer animation type (slide, zoom, fade, none) |
| `animation_fade_in` | integer | 1 | Enable fade-in effect (0-disable, 1-enable) |
| `animation_fade_out` | integer | 1 | Enable fade-out effect (0-disable, 1-enable) |
| `tag_animation_direction` | integer | 1 | Tag animation direction (1-horizontal, 0-vertical) |
| `zoom_initial_ratio` | float | 0.3 | Initial zoom ratio |
| `zoom_end_ratio` | float | 0.8 | End zoom ratio |
| `fadein_begin_opacity` | float | 0.5 | Fade-in starting opacity |
| `fadeout_begin_opacity` | float | 0.8 | Fade-out starting opacity |
| `animation_duration_move` | integer | 500 | Move animation duration (ms) |
| `animation_duration_open` | integer | 400 | Open animation duration (ms) |
| `animation_duration_tag` | integer | 350 | Tag animation duration (ms) |
| `animation_duration_close` | integer | 800 | Close animation duration (ms) |
| `animation_duration_focus` | integer | 0 | Focus change(opacity transition) animation duration (ms) |
| `animation_curve_open` | string | 0.46,1.0,0.29,1 | Open animation bezier curve |
| `animation_curve_move` | string | 0.46,1.0,0.29,1 | Move animation bezier curve |
| `animation_curve_tag` | string | 0.46,1.0,0.29,1 | Tag animation bezier curve |
| `animation_curve_close` | string | 0.08,0.92,0,1 | Close animation bezier curve |
| `animation_curve_focus` | string | 0.46,1.0,0.29,1 | Focus change(opacity transition) animation bezier curve |

## Scroller Layout Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `scroller_structs` | integer | 20 |The width reserved on both sides of the screen when the window size ratio is 1 |
| `scroller_default_proportion` | float | 0.8 | Default scroller proportion for window width |
| `scroller_focus_center` | integer | 0 | Always make focus window center in screen (0-disable, 1-enable) |
| `scroller_prefer_center` | integer | 0 | If the last focused window is inside the monitor, don't make the focused window centered, if not , then make the focused window center (0-disable, 1-enable) |
| `edge_scroller_pointer_focus` | integer | 1 | if window not completely in the monitor,still focus it by pointer motion (0-disable, 1-enable) |
| `scroller_ignore_proportion_single` | integer | 0 | not auto adjust the window when there is single window in current tag (0-disable, 1-enable) |
| `scroller_default_proportion_single` | float | 1.0 | Default proportion of scroller window when there is single window in the current tag|
| `scroller_proportion_preset` | string | 0.5,0.8,1.0 | Preset proportion of scroller window values for switch|

## Master-Stack Layout Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `new_is_master` | integer | 1 | New window becomes master (0-disable, 1-enable) |
| `default_mfact` | float | 0.55 | Default master area factor |
| `default_nmaster` | integer | 1 | Default number of master windows |
| `smartgaps` | integer | 0 | Enable smart gaps (0-disable, 1-enable) |
| `center_master_overspread` | integer | 0 | Center master window overspread whole screen when there is no stack window,only works for center_tile layout |
| `center_when_single_stack` | integer | 1| Center master window when there is only one stack window,only works for center_tile layout |


## Overview Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `hotarea_size` | integer | 10 | Hot area size in pixels |
| `enable_hotarea` | integer | 1 | Enable hot areas (0-disable, 1-enable) |
| `ov_tab_mode` | integer | 0 | Overview tab mode (0-disable, 1-enable) |
| `overviewgappi` | integer | 5 | Inner gap in overview mode |
| `overviewgappo` | integer | 30 | Outer gap in overview mode |

### A More Detailed Explanation
``enable_hotarea``: when your cursor enters the bottom left corner of the monitor, it will toggle the overview mode.
``hotarea_size``: the size of hotarea, 10x10 default.
``ov_tab_mode``: the overview will circle switch focus when you toggle overview and will leave ov mode when you release your mod key.

### Notice

When you are in overview mode, you can use the right mouse button to close a window, and the left mouse button to jump to a window.


## Miscellaneous Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `xwayland_persistence` | integer | 1 | (0 or 1) Enable xwayland persistence (needs a relogin to take effect) |
| `syncobj_enable` | integer | 0 | (0 or 1) Enable drm_syncobj (needs a relogin to take effect) |
| `adaptive_sync` | integer | 0 | (0 or 1) Enable variable refresh rate(vrr) |
| `allow_shortcuts_inhibit` | 1 | (0 or 1) Allow shortcuts to be inhibited by clients |
| `allow_tearing` | 0 | (0 or 1 or 2) Allow tearing,refer to [tearing](#tearinggame-mode) |
| `allow_lock_transparent`| integer | 0 | (0 or 1) Enable transparent lock screen |
| `axis_bind_apply_timeout` | integer | 100 | Detect the intervals of consecutive scroll for axisbind |
| `focus_on_activate` | integer | 1 | (0 or 1) Focus window when window send activate event (0-disable, 1-enable) |
| `inhibit_regardless_of_visibility` | integer | 0 | (0 or 1) Invisible clients can also trigger idle inhibit |
| `sloppyfocus` | integer | 1 | (0 or 1) Focus follow mouse move |
| `warpcursor` | integer | 1 | (0 or 1) Cursor warping when focus change|
| `focus_cross_monitor` | integer | 0 | (0 or 1) Focus across monitors |
| `exchange_cross_monitor` | integer | 0 | (0 or 1) exchange two clients across monitors |
| `scratchpad_cross_monitor` | integer | 0 | (0 or 1) all monitors have the same scratchpad |
| `focus_cross_tag` | integer | 0 |(0 or 1)  Focus across tags |
| `view_current_to_back` | integer | 1 |(0 or 1)  View current tag will auto back to prev view tag |
| `enable_floating_snap` | integer | 0 |(0 or 1) Enable floating window snap |
| `snap_distance` | integer | 30 |(0 - 9999) The max distance to trigger  floating window snap |
| `cursor_size` | integer | 24 |(0 - 9999) Set cursor size |
| `cursor_theme` | string | - | Set cursor theme |
| `no_border_when_single` | interger | 0 | Don't render border when the window is alone in the tag |
| `cursor_hide_timeout` | interger(sec) | 0 | 0 -9999 (0 meas disable hide cursor)| Hide cursor when timeout|
| `drag_tile_to_tile` |  interger | 0 | (0 or 1) If the dragged window is a tiled window, it will retile when the drag ends|
| `single_scratchpad` | interger | 1 | only show one out of named scratchpads or the normal scratchpad |

## Keyboard Settings
| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `repeat_rate` | integer | 25 | Keyboard repeat rate |
| `repeat_delay` | integer | 600 | Keyboard repeat delay |
| `numlockon` | integer | 1 |(0 or 1) Numlock state on startup |


## Trackpad Settings & Mouse Settings
| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `disable_trackpad` | integer | 0 | (0 or 1) Disable trackpad |
| `tap_to_click` | integer | 1 | (0 or 1) Enable tap to click |
| `tap_and_drag` | integer | 1 | (0 or 1) Enable tap and drag |
| `drag_lock` | integer | 1 | (0 or 1) Enable drag lock |
| `trackpad_natural_scrolling` | integer | 0 | (0 or 1) Natural scrolling direction |
| `disable_while_typing` | integer | 1 |(0 or 1)  Disable trackpad while typing |
| `left_handed` | integer | 0 | (0 or 1) Left-handed mode |
| `middle_button_emulation` | integer | 0 |(0 or 1)  Middle mouse button emulation |
| `swipe_min_threshold` | integer | 20 | Minimum swipe threshold |
| `mouse_natural_scrolling` | integer | 0 |(0 or 1)  Natural scrolling for mouse |
| `accel_profile` | integer | 2 |(0 or 1 or 2)  accel mode |
| `accel_speed` | float | 0.0 |(-1 - 1)  accel speed |
| `scroll_method` | integer | 1 | (0: none, 1: two-finger, 2: edge, 4: button) Scrolling method for touchpads |
| `click_method` | integer | 1 | (0: none, 1: button areas, 2: clickfinger) Method for triggering button clicks on touchpads |
| `send_events_mode` | integer | 0 | (0: enabled, 1: disabled, 2: disabled on external mouse) Controls when events are sent from the device |
| `button_map` | integer | 0 | (0:left/right/middle, 1:left/middle/right) |

**Detailed Descriptions:**

1. **scroll_method**  
   Configures the scrolling technique for touchpads:  
   - `0`: Never send scroll events instead of pointer motion events.
   - `1`: Send scroll events when two fingers are logically down on the device.
   - `2`: Send scroll events when a finger moves along the bottom or right edge of a device.
   - `4`: Send scroll events when a button is down and the device moves along a scroll-capable axis.

2. **click_method**  
   Configures how touchpad clicks are registered:  
   - `0`: No software click emulation.
   - `1`: Use software-button areas to generate button events.
   - `2`: The number of fingers decides which button press to generate.

3. **send_events_mode**  
   Controls event delivery behavior:  
   - `0`: Send events from this device normally.
   - `1`: Do not send events through this device. 
   - `2`: If an external pointer device is plugged in, do not send events from this device.

4. **button_map**  
    The 1/2/3 finger tap maps to mouse buttons:  
    - `0`: left/right/middle  
    - `1`: left/middle/right

5. **accel_profile**
  - `0` : Don't use accel
  - `1` : No dynamic acceleration. Pointer speed = original input speed × (1 + accel_speed).
  - `2` : Slow movement leads to less acceleration, while fast movement leads to more acceleration.



## Appearance Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `gappih` | integer | 5 | Horizontal inner gap |
| `gappiv` | integer | 5 | Vertical inner gap |
| `gappoh` | integer | 10 | Horizontal outer gap |
| `gappov` | integer | 10 | Vertical outer gap |
| `scratchpad_width_ratio` | float | 0.8 | (0.1-1.0) scratchpad width ratio |
| `scratchpad_height_ratio` | float | 0.9 | (0.1-1.0) scratchpad height ratio |
| `borderpx` | integer | 4 | Border width |
| `rootcolor` | hex | 0x201b14ff | Root window color |
| `bordercolor` | hex | 0x444444ff | Border color |
| `focuscolor` | hex | 0xad741fff | Focused window border color |
| `maximizescreencolor` | hex | 0x89aa61ff | Maximized screen color |
| `urgentcolor` | hex | 0xad401fff | Urgent window color |
| `scratchpadcolor` | hex | 0x516c93ff | Scratchpad color |
| `globalcolor` | hex | 0xb153a7ff | Global window color |
| `overlaycolor` | hex | 0x14a57cff | Overlay window color |

## Tag Rules
- you can set all parameters in one line
- If only `id` is set, the rule is followed when the id matches.
- If both `id` and `monitor_name` are set, the rule is followed only if both `id` and `monitor_name` match.

Format:
```conf
tagrule=id:Values,Parameter:Values,Parameter:Values
tagrule=id:Values,monitor_name:eDP-1,Parameter:Values,Parameter:Values
```
### support layout_name
  - tile
  - scroller
  - monocle
  - grid
  - deck
  - center_tile
  - right_tile
  - vertical_tile
  - vertical_scroller
  - vertical_grid
  - vertical_spiral
  - vertical_deck

| Parameter | Type | Values | Description |
|-----------|------|--------|-------------|
| `id` | integer | 0-9 | Match by tags id,0 means ~0 tag |
| `monitor_name` | string | monitor name | Match by monitor name |
| `layout_name` | string | layout name | Layout name to set |
| `no_render_border` | integer | 0 or 1 | diable render border |
| `no_hide` | integer | 0,1 | not hide even if the tag is empty |


### example
- persistent tag(1-4)
maomao config:
```conf
tagrule=id:1,no_hide:1
tagrule=id:2,no_hide:1
tagrule=id:3,monitor_name:eDP-1,no_hide:1
tagrule=id:4,monitor_name:eDP-1,no_hide:1
```
waybar config:
```json
"ext/workspaces": {
  "format": "{icon}",
  "ignore-hidden": true,
  "on-click": "activate",
  "sort-by-id": true,
},
```

## Layer Rules
- you can set all parameters in one line

Format:
```conf 
layerrule=layer_name:Values,Parameter:Values,Parameter:Values
```

| Parameter | Type | Values | Description |
|-----------|------|--------|-------------|
| `layer_name` | string | layer_name | match name of layer, support regex |
| `animation_type_open` | string | slide, zoom, fade, none | Set open animation |
| `animation_type_close` | string | slide, zoom, fade, none | Set close animation |
| `noblur` | integer | 0 or 1 | Disable blur |
| `noanim` | integer | 0 or 1 | Disable layer animation |
| `noshadow` | integer | 0 or 1 | Disable layer shadow |

- you can use `mmsg -e` to get the last open layer name

```conf
# no blur slurp select layer
layerrule=noblur:1,layer_name:selection
```

## Window Rules

- you can set all parameters in one line
- if you both set appid and title, the window will only follow the rules when appid and title both match

Format:
```conf
windowrule=Parameter:Values,title:Values
windowrule=Parameter:Values,Parameter:Values,appid:Values,title:Values
```

| Parameter | Type | Values | Description |
|-----------|------|--------|-------------|
| `appid` | string | Any | Match by application ID, support regex |
| `title` | string | Any | Match by window title, support regex |
| `tags` | integer | 1-9 | Assign to specific tag |
| `isfloating` | integer | 0,1 | Force floating state |
| `isfullscreen` | integer | 0,1 | Force fullscreen state |
| `scroller_proportion` | float | 0.1-1.0 | Set scroller proportion |
| `scroller_proportion_single` | float | 0.1-1.0 | Set scroller auto adjust proportion when it is single window |
| `animation_type_open` | string | zoom,slide,fade,none | Set open animation |
| `animation_type_close` | string | zoom,slide,fade,none | Set close animation |
| `isnoborder` | integer | 0,1 | Remove window border |
| `isnoshadow` | integer | 0,1 | not apply shadow|
| `isnoanimation` | integer | 0,1 | not apply animation|
| `monitor` | string | Any | Assign to monitor by monitor name |
| `offsetx` | integer | -100-100 | X offset from center (%) |
| `offsety` | integer | -100-100 | Y offset from center (%) |
| `width` | integer | 0-9999 | Window width when it becomes a floating window |
| `height` | integer | 0-9999 | Window height when it becomes a floating window |
| `isterm` | integer | 0,1 | A new gui window will replace the isterm window when it is opened |
| `noswallow` | integer | 0,1 | The window will not replace the isterm window  |
| `globalkeybinding` | string | [mod scombination][-][key] | Global keybinding (only works for wayland apps) |
| `isopensilent` | integer | 0,1 | Open without focus |
| `istagsilent` | integer | 0,1 | Dont focus if client is not in current view tag |
| `isglobal` | integer | 0,1 | Open as global window|
| `isoverlay` | integer | 0,1 | Make it always in top layer|
| `ignore_maximize` | integer | 0,1 (default 1) | Don't handle maximize request from client |
| `ignore_minimize` | integer | 0,1  (default 1) | Don't handle minimize request from client |
| `force_maximize` | integer | 0,1  (default 1) | the state of client default to maximized |
| `isnosizehint` | integer | 0,1 | Don't use min size and max size for size hints|
| `isunglobal` | integer | 0,1 | Open as unmanaged global window (for desktop pets or camerawindows) |
| `isnamedscratchpad` | integer | 0,1 | 0: disable, 1: named scratchpad |
| `nofadein` | integer | 0,1 | Window ignores fadein animation |
| `no_force_center` | integer | 0,1 | Window does not force center |
| `noopenmaximized` | integer | 0,1 | Window does not open as maximized mode |
| `focused_opacity` | integer | 0,1 | Window focused opacity |
| `unfocused_opacity` | integer | 0,1 | Window unfocused opacity |
| `noblur` | integer | 0,1 | Window does not have blur effect |
| `allow_csd` | integer | 0,1 | Allow client side decoration |
| `force_tile_state` | integer | 0,1 | Force set window to tile state |
| `force_tearing` | integer | 0,1 | Set window to tearing state,refer to [tearing](#tearinggame-mode) |
| `allow_shortcuts_inhibit` | integer | 0,1 (default 1) | Allow shortcuts to be inhibited by clients |


```conf
windowrule=width:1000,height:900,appid:yesplaymusic,title:Demons
windowrule=globalkeybinding:ctrl+alt-o,appid:com.obsproject.Studio
windowrule=globalkeybinding:ctrl+alt-n,appid:com.obsproject.Studio
windowrule=isopensilent:1,appid:com.obsproject.Studio
```

## Monitor Rules
- notice

If you use xwayland, don't set any display to negative coordinates, as this will cause the click event to be abnormal, refer to this
[xwayland issue](https://gitlab.freedesktop.org/xorg/xserver/-/issues/899)
 

| Parameter | Format | Example | Description |
|-----------|--------|---------|-------------|
| `monitorrule` | name,mfact,nmaster,layout,transform,scale,x,y,width,height,refreshrate | eDP-1,0.55,1,tile,0,1,0,0,1920,1080,60 | Configure monitor properties |

Transform values:
- 0: No transform
- 1: 90° counter-clockwise
- 2: 180° counter-clockwise
- 3: 270° counter-clockwise
- 4: 180° vertical flip
- 5: Flip + 90° counter-clockwise
- 6: Flip + 180° counter-clockwise
- 7: Flip + 270° counter-clockwise

- example
```conf
monitorrule=eDP-1,0.55,1,tile,0,1,0,0,1920,1080,60
monitorrule=HDMI-A-1,0.55,1,tile,0,1,1925,0,2560,1440,144
```

## Env setting
- will reset every time after config reload
```conf
env=<ENV NAME>,<ENV VALUE>
```
for example:
```conf
env=HELLO,word
```

## Exec setting
``exec`` will run every time after a config reload
``exec-once`` will only exec once after mango startup

```conf
exec-once=<COMMAND>
exec=<COMMAND>
```
For example:
```conf
exec-once=waybar
exec=bash reloadsomething.sh
```
Here waybar will only run when mango is started for the first time, and reloadsomething.sh will run every time the config is hotloaded.

## Key Bindings

### format
The key binding format follows this pattern:
`bind` will auto convert keysym to keycode for compare.(This means it is compatible with all keyboard layouts, but the matching may not be precise enough.)

```conf
# compare keycode
bind=<MODIFIERS>,<KEY>,<COMMAND>,<PARAMETERS>
```
- `<MODIFIERS>`: Comma-separated modifier keys (SUPER,CTRL,ALT,SHIFT,NONE),You can combine the keys with `+`, like `SUPER+CTRL+ALT`

- `<KEY>`: The key to bind (keyname from `xev` output)
- `<COMMAND>`: The action to execute
- `<PARAMETERS>`: Optional parameters for the command

### bind flag
- `bind[flag]`,flag can be one of the following or their combination.
  - l : still apply bind when screen is locked
  - s : use keysym instead of keycode to bind
  - r : handle release event instead of press event

```conf
bindl=SUPER,l,quit
bindls=SUPER,s,quit
```

The modifier and key can use keycode to replace.

```conf
bind=ALT,q,killclient,
bind=ALT+ctrl,Q,killclient,
bind=ALT,code:24,killclient,
bind=code:64,code:24,killclient,
bind=code:64+code:133,code:24,killclient,
bind=Alt+code:133,code:24,killclient,
bind=NONE,XF86MonBrightnessUp,spawn,brightnessctl set +5%
```

### Key mode
Divide the keys into different modes.

- 1. set keymode before bind, then the bind will apply to the keymode
- 2. if no keymode set before bind, default keymode is `default`
- 3. `common` keymode will be apply to all binds

- example: bind to test mode.
```conf

keymode=common
bind=Super,r,reload_config

keymode=default
bind=alt,Return,spawn,st
bind=Super,f,setkeymode,test

keymode=test
bind=alt,Return,spawn,foot
bind=Super,f,setkeymode,default
```
you can use `setkeymode` to set keymode. and use `mmsg -b` to get the current keymode.

### Available Commands

| Command | Parameters | Description |
|---------|------------|-------------|
| reload_config | - | Reload configuration file |
| spawn | command | Execute command directly |
| spawn_shell | command | Execute command in shell|
| spawn_on_empty | command,tagnumber | Open command on empty tag,if not empty, focus it |
| quit | - | Quit window manager |
| killclient | - | Close focused window |
| focuslast | - | Focus last focused window |
| focusstack | next/prev | Focus next/prev window in stack |
| focusdir | left/right/up/down | Focus window in direction |
| exchange_client | left/right/up/down | Swap window position |
| exchange_stack_client | next/prev | Exchange window position in stack |
| toggleglobal | - | Toggle window global state |
| toggleoverview | - | Toggle overview mode |
| togglefloating | - | Toggle floating state |
| toggleoverlay | - | Toggle overlay state |
| togglemaximizescreen | - | Toggle maximize state |
| togglefullscreen | - | Toggle fullscreen state |
| togglefakefullscreen | - | Toggle fakefullscreen state |
| minimized | - | Minimize window |
| restore_minimized | - | Restore minimized window |
| toggle_render_border | - | Toggle whether to render border |
| toggle_scratchpad | - | Toggle scratchpad |
| toggle_name_scratchpad | (appid,title,width,height,cmd) (a,none,1,1,foot)/(none,b,1,1,foot) | Toggle scratchpad |
| set_proportion | float number (0.0-1.0) | Set scroller window proportion |
| switch_proportion_preset | - | Cycle proportion presets of scroller window |
| incnmaster | +1/-1 | Adjust master window count |
| setmfact | +/-value (+10)/(-10) | Adjust master area factor |
| zoom | - | exchange with master window |
| setlayout | layout_name (scroller) | Set specific layout |
| switch_layout | - | Cycle through layouts |
| view                     | tag_number: [-1,0,1-9] [, synctag(0,1)] | View specific tag (0=view all tags, -1=view previous tagset); synctag:tag action syncs to all monitors (0=no,1=yes) |
| viewtoleft               | [synctag(0,1)]                          | View tag to the left; synctag:tag action syncs to all monitors (0=no,1=yes)                                        |
| viewtoright              | [synctag(0,1)]                          | View tag to the right; synctag:tag action syncs to all monitors (0=no,1=yes)                                       |
| viewtoleft_have_client   | [synctag(0,1)]                          | View left tag and focus client if present; synctag:tag action syncs to all monitors (0=no,1=yes)                   |
| viewtoright_have_client  | [synctag(0,1)]                          | View right tag and focus client if present; synctag:tag action syncs to all monitors (0=no,1=yes)                  |
| viewcrossmon | tag_number,monitor_name  | view to specified tag of the specified monitor |
| tag                      | tag_number: [1-9] [, synctag(0,1)]      | Move window to specified tag; synctag:tag action syncs to all monitors (0=no,1=yes)                                |
| tagtoleft                | [synctag(0,1)]                          | Move window to left tag; synctag:tag action syncs to all monitors (0=no,1=yes)                                     |
| tagtoright               | [synctag(0,1)]                          | Move window to right tag; synctag:tag action syncs to all monitors (0=no,1=yes)                                    |
| tagcrossmon | tag_number,monitor_name  | Move window to specified tag of the specified monitor |
| toggletag | tag_number (0-9,0 means all tags) | Toggle tag on window |
| toggleview | tag_number (1-9) | Toggle tag view |
| comboview | tag_number (1-9) | view multi tags that is press in the same time |
| focusmon | left/right/up/down/[monitorName] | Focus monitor,monitorName is monitor name string |
| tagmon | left/right/up/down/[monitorName],[keeptag] | Move window to monitor, keeptag is 0 or 1 |
| incgaps | +/-value (+10)/(-10) | Adjust gap size |
| togglegaps | - | Toggle gaps |
| smartmovewin | left/right/up/down | Move float window by auto distance |
| smartresizewin | left/right/up/down | Resize float window by auto size |
| centerwin | - | Move window to center |
| movewin | (x,y) (+10,-10)/(10,10) | Move float window |
| resizewin | (width,height) (+10,-10)/(10,10) | Resize window |
| create_virtual_output | - | create a virutal monitor |
| destroy_all_virtual_output | - | destroy all virutal monitors|
| toggle_trackpad_enable | - | Toggle trackpad enable(change the default state of global option `disable_trackpad`) |
| setkeymode | keymode name (default) | Set keymode |
| switch_keyboard_layout | - | Switch keyboard layout |
| setoption | key,value | Set config option temporarily without change config file|
| disable_monitor | monitor_name | shutdown monitor |
| enable_monitor | monitor_name | open monitor |
| toggle_monitor | monitor_name | toggle monitor power|

## Reload Config Bind

```conf
bind=SUPER,r,reload_config
```

## Mouse Bindings

```
mousebind=<MODIFIERS>,<BUTTON>,<COMMAND>,<PARAMETERS>

```
- `<MODIFIERS>`: Comma-separated modifier keys (SUPER,CTRL,ALT,SHIFT,NONE)
- `<BUTTON>`: Mouse button (btn_left, btn_right, btn_middle)
- `<COMMAND>`: The action to execute
- `<PARAMETERS>`: Optional parameters for the command

- Notice
 if the MODIFIERS is `NONE` , only middle button will apply in general mode.
and right and left button with `NONE` MODIFIERS  only work in overview mode.

```conf
mousebind=SUPER,btn_left,moveresize,curmove
mousebind=SUPER,btn_right,moveresize,curresize
mousebind=SUPER+CTRL,btn_right,killclient
mousebind=NONE,btn_middle,togglemaximizescreen,0
mousebind=NONE,btn_left,toggleoverview,-1
mousebind=NONE,btn_right,killclient,0
```

## Axis Bindings

Binds for using the mouse wheel

```
axisbind=<MODIFIERS>,<AXIS_DIRECTION>,<COMMAND>,<PARAMETERS>

```

- `<MODIFIERS>`: Comma-separated modifier keys
- `<AXIS_DIRECTION>`: UP/DOWN/LEFT/RIGHT
- `<COMMAND>`: The action to execute
- `<PARAMETERS>`: Optional parameters for the command

```conf
axisbind=SUPER,UP,viewtoleft_have_client
axisbind=SUPER,DOWN,viewtoright_have_client
```


##  Switch Bindings

Binds for lid fold toggle

you need to disable system lidhandle in `/etc/systemd/logind.conf`

```conf
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```
switchbind=<FOLD_STATE>,<COMMAND>,<PARAMETERS>

```

- `<FOLD_STATE>`: fold/unfold
- `<COMMAND>`: The action to execute
- `<PARAMETERS>`: Optional parameters for the command

```conf
switchbind=fold,spawn,swaylock -f -c 000000
switchbind=unfold,spawn,wlr-dpms on
```

## Gesture Bindings

Touchpad gesture binds 

```
gesturebind=<MODIFIERS>,<DIRECTION>,<FINGERS>,<COMMAND>,<PARAMETERS>

```

- `<MODIFIERS>`: Comma-separated modifier keys
- `<DIRECTION>`: up/down/left/right
- `<FINGERS>`: Number of fingers (3,4)
- `<COMMAND>`: The action to execute
- `<PARAMETERS>`: Optional parameters for the command


```conf
gesturebind=none,left,3,focusdir,left
gesturebind=none,right,3,focusdir,right
gesturebind=none,up,3,focusdir,up
gesturebind=none,down,3,focusdir,down
gesturebind=none,left,4,viewtoleft_have_client
gesturebind=none,right,4,viewtoright_have_client
gesturebind=none,up,4,toggleoverview
gesturebind=none,down,4,toggleovervie
```

## Keyboard layout and IME
| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `xkb_rules_rules` | string | - | Specifies the name of XKB keyboard mapping rules (e.g., `evdev` or `base`). Usually auto-detected by the system and rarely needs manual configuration. |
| `xkb_rules_model` | string | - | Defines the keyboard hardware model (e.g., `pc104`, `macbook`), used to match physical layouts of specific keyboards. |
| `xkb_rules_layout` | string | - | Sets the country/region code for the keyboard layout (e.g., `us`, `de`, `fr`), determining the base language key mapping. |
| `xkb_rules_variant` | string | - | Specifies layout variants (e.g., `dvorak`, `colemak`, or `intl`) to extend or modify standard layouts. |
| `xkb_rules_options` | string | - | Additional options (e.g., `ctrl:nocaps`, `compose:prsc`) to enable specific features or further customize behavior. |

- example
you can use `switch_keyboard_layout` to switch layout.
```conf
xkb_rules_layout=us,us
xkb_rules_variant=dvorak,
xkb_rules_options=grp:lalt_lshift_toggle
```

### ime env for fcitx5
```conf
env=GTK_IM_MODULE,fcitx
env=QT_IM_MODULE,fcitx
env=SDL_IM_MODULE,fcitx
env=XMODIFIERS,@im=fcitx
env=GLFW_IM_MODULE,ibus
```

## Waybar for mango

- 1.you can also use the dwl moudle in waybar to show tags and window title
  refer to waybar wiki: [dwl-module](https://github.com/Alexays/Waybar/wiki/Module:-Dwl)

- you can also use [workspace module](https://github.com/Alexays/Waybar/wiki/Module:-Workspaces) to replace dwl-tag module.(suggest,need waybar > 0.14.0)

[waybar rice for mango](https://github.com/DreamMaoMao/waybar-config)

### config
```json
"modules-left": [
    "ext/workspaces",
    // "dwl/tags",
    "dwl/window"
],
  "ext/workspaces": {
    "format": "{icon}",
    "ignore-hidden": true,
    "on-click": "activate",
    "on-click-right": "deactivate",
    "sort-by-id": true,
  },
  "dwl/tags": {
      "num-tags":9,
  },
  "dwl/window": {
      "format": "[{layout}]{title}"
  },

```
### style.css
```css
#workspaces {
  border-radius: 4px;
  border-width: 2px;
  border-style: solid;
  border-color: #c9b890;
  margin-left: 4px;
  padding-left: 10px;
  padding-right: 6px;
  background: rgba(40, 40, 40, 0.76);

}

#workspaces button {
  border: none;
  background: none;
  box-shadow: inherit;
  text-shadow: inherit;
  color: #ddca9e;
  padding: 1px;
  padding-left: 1px;
  padding-right: 1px;
  margin-right: 2px;
  margin-left: 2px;
}

#workspaces button.hidden {
  color: #9e906f;

  background-color: transparent;
}

#workspaces button.visible {
  color: #ddca9e;
}

#workspaces button:hover {
  color: #d79921;
}

#workspaces button.active {
  background-color: #ddca9e;
  color: #282828;
  margin-top: 5px;
  margin-bottom: 5px;
  padding-top: 1px;
  padding-bottom: 0px;
  border-radius: 3px;
}

#workspaces button.urgent {
  background-color: #ef5e5e;
  color: #282828;
  margin-top: 5px;
  margin-bottom: 5px;
  padding-top: 1px;
  padding-bottom: 0px;
  border-radius: 3px;
}

#tags {
  background-color: transparent;
}

#tags button {
  background-color: #fff;
  color: #a585cd;
}

#tags button:not(.occupied):not(.focused) {
  font-size: 0;
  min-width: 0;
  min-height: 0;
  margin: -17px;
  padding: 0;
  color: transparent;
  background-color: transparent;
}

#tags button.occupied {
  background-color: #fff;
  color: #cdc885;
}

#tags button.focused {
  background-color: rgb(186, 142, 213);
  color: #fff;
}

#tags button.urgent {
  background: rgb(171, 101, 101);
  color: #fff;
}

#window {
  background-color: rgb(237, 196, 147);
  color: rgb(63, 37, 5);
}

```

## Custom animation

```
animation_curve_open=0.46,1.0,0.29,1.1
animation_curve_move=0.46,1.0,0.29,1
animation_curve_tag=0.46,1.0,0.29,1
animation_curve_close=0.46,1.0,0.29,1

```

You can design your animaition curve [here, at cssportal.com](https://www.cssportal.com/css-cubic-bezier-generator/),

or you can just choose a curve at [easings.net](https://easings.net).


## More Monitor Settings

- you can use `wlr-randr` to set ratio and vertrefresh.
```bash
yay -S wlr-randr
```
- you can use `wlr-dpms` to toggle monitor power off or on.
```bash
yay -S wlr-dpms
```

- you can also use mmsg to trun on/off monitor power.
```bash
mmsg -d enable_monitor,eDP-1
mmsg -d disable_monitor,eDP-1
mmsg -d toggle_monitor,eDP-1
```

- you can also use `wlr-randr` to remove monitor or enable monitor.
```bash
# remove monitor
wlr-randr --output eDP-1 --off

# enable monitor
wlr-randr --output eDP-1 --on
```

- It cannot be displayed correctly or just shows a black screen,you can try to use
  another gpu to run mango.
```bash
# set one card
WLR_DRM_DEVICES=/dev/dri/card1 mango

# set multi card
WLR_DRM_DEVICES=/dev/dri/card0:/dev/dri/card1 mango

```
## Tearing(Game mode)
|      force_tearing   \allow_tearing           | DISABLED（0）  | ENABLED（1） | FULLSCREEN_ONLY（2） |
|--------------------|-----------------------------------|----------------------------------|------------------------------------------|
| UNSPECIFIED  （0）| ❌ Not Allowed                    | ✅ Follows tearing_hint | ✅ Only fullscreen follows tearing_hint |
| ENABLED   （1）   | ❌ Not Allowed                    | ✅ Allowed  | ✅  Only fullscreen allowed                               |
| DISABLED   （2）  | ❌ Not Allowed                    | ❌ Not Allowed                   | ❌ Not Allowed                           |

```conf
allow_tearing=1
windowrule=force_tearing:1,appid:.*
```
```
# Some graphics cards need to set this  `WLR_DRM_NO_ATOMIC` environment variable before mango starts in order to successfully tear.you can put it in `/etc/environment` and reboot your computer once.

WLR_DRM_NO_ATOMIC=1 mango
```

## Screen Scale
### not use global scale(recommended)
- If you do not use xwayland apps, you can just use monitor rule or wlr-randr to set a global 
monitor scale.

- If you are using some xwayland apps, I don't suggest you to set monitor scale.

you can set scale like this , such as 1.4 factor.

Dependencies:
```bash
yay -S xorg-xrdb
```
In config file.
```conf
env=QT_AUTO_SCREEN_SCALE_FACTOR,1
env=QT_WAYLAND_FORCE_DPI,140
```
In autostart.
```sh
echo "Xft.dpi: 140" | xrdb -merge
gsettings set org.gnome.desktop.interface text-scaling-factor 1.4
```

- 3.edit autostart.sh
```bash
# start xwayland
/usr/sbin/xwayland-satellite :11 &
# scale 1.4 for xwayland
sleep 0.5s && echo "Xft.dpi: 140" | xrdb -merge
```



## Scratchpad
### sway like scratchpad
```conf
# put a window in scratchpad link
bind=SUPER,i,minimized,

# Go through all the bookmarks
bind=ALT,z,toggle_scratchpad

# move out a window from scratchpad link
# you can also you togglefloating move out
bind=SUPER+SHIFT,I,restore_minimized

```

### Named Scratchpad
You can bind a named scratchpad by fixing the titile or appid of a window. In this way, whether the window is launched in advance or not, as long as you press this shortcut key, it will toggle show or hide.

The application you use needs to have the ability to set an appid or title, such as `kitty-T` or `st -c` to fix the title or appid.


```conf
# toggle_named_scratchpad,[appid],[title],[cmd]
bind=alt,h,toggle_named_scratchpad,st-yazi,none,st -c st-yazi -e yazi
windowrule=isnamedscratchpad:1,width:1280,height:800,appid:st-yazi

```


## Ipc
you can use `mmsg` command to send ipc message to control mango or get message from mango.
example:
```bash
# get message from mango
mmsg -g
# reload config
mmsg -d reload_config
# quit mango
mmsg -d quit
```
more details refer to [ipc](https://github.com/DreamMaoMao/mangowc/wiki/mango-ipc-(mmsg))

## Virtual Monitor

- You can quickly create and destroy a virtual display through ipc

```bash
mmsg -d create_virtual_output
mmsg -d destroy_all_virtual_output
```

- You can set option to the virutal monitor by `wlr-randr`
```bash
# show all monitor
wlr-randr 
# set virtual monitor
wlr-randr  --output HEADLESS-1 --pos 1921,0  --scale 1 --custom-mode 1920x1080@60Hz
```

You can connect to mango's virtual monitor through some tools, allowing other devices to become your extended monitor.
sucn as .[sunshine](https://github.com/LizardByte/Sunshine) and [moonlight](https://github.com/moonlight-stream/moonlight-android)


## screen record or share(obs or wemeet)
- 1. You need to install some dependencies
```bash
yay -S pipewire pipewire-pulse xdg-desktop-portal-wlr
```
- 2. Put this in your autostart script
```bash
dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP=wlroots
# The next line of command is not necessary. It is only to avoid some situations where it cannot start automatically
/usr/lib/xdg-desktop-portal-wlr &

```
- 3. Restart your computer 

## clipboard
- Dependencies

```bash
yay -S wl-clip-persist wl-clipboard cliphist

```

- Put this in you autostart script
```bash
# keep clipboard content
wl-clip-persist --clipboard regular --reconnect-tries 0 &

# clipboard content manager
wl-paste --type text --watch cliphist store & 

```

## file picker(file selector)
- Dependencies
```bash
yay -S xdg-desktop-portal  xdg-desktop-portal-gtk
```
`reboot your computer once to apply`

## Keyring
- Dependencies
```bash
yay -S gnome-keyring
```
- create portal config file(~/.config/xdg-desktop-portal/portals.conf)
```conf
[preferred]
default=gtk
org.freedesktop.impl.portal.ScreenCast=wlr
org.freedesktop.impl.portal.Screenshot=wlr
org.freedesktop.impl.portal.Secret=gnome-keyring
org.freedesktop.impl.portal.Inhibit=none
```

reboot your computer once to apply.

## some config I suggest.

- autostart.sh

```bash
#! /bin/bash

set +e

# obs
dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP=wlroots

# notify
swaync &

# night light
wlsunset -T 3501 -t 3500 &

# wallpaper
swaybg -i ~/.config/mango/wallpaper/room.png &

# top bar
waybar -c ~/.config/mango/waybar/config -s ~/.config/mango/waybar/style.css &

# keep clipboard content
wl-clip-persist --clipboard regular --reconnect-tries 0 &

# clipboard content manager
wl-paste --type text --watch cliphist store & 

# xwayland dpi scale
echo "Xft.dpi: 140" | xrdb -merge #dpi缩放
gsettings set org.gnome.desktop.interface text-scaling-factor 1.4

# Permission authentication
/usr/lib/xfce-polkit/xfce-polkit &

```

- config.conf
```conf
# cursor size
cursor_size=24
env=XCURSOR_SIZE,24

# fcitx5 im
env=GTK_IM_MODULE,fcitx
env=QT_IM_MODULE,fcitx
env=SDL_IM_MODULE,fcitx
env=XMODIFIERS,@im=fcitx
env=GLFW_IM_MODULE,ibus

# scale factor about qt (herr is 1.4)
env=QT_QPA_PLATFORMTHEME,qt5ct
env=QT_AUTO_SCREEN_SCALE_FACTOR,1
env=QT_QPA_PLATFORM,Wayland;xcb
env=QT_WAYLAND_FORCE_DPI,140
```
## Question and Answer(High-frequency)

- how to use pipe in spawn
 >you can use `spawn_shell` to run a command in shell

- why blur show the wallpaper in background
 >you can use `blur_optimized` to disable it but will consume more gpu

- Certain key combinations do not work on certain keyboard layouts
 >you can use keycode to bind it,like `code:24` to replace `q`


- How do I arrange tiles with my mouse
 >you can use `drag_tile_to_tile` to enalbe it.


- Some of my games are lagging or freezing
> try set `syncobj_enable` to `1` to enable syncobj and set `adaptive_sync` to `1` to enable variable refresh rate.

- Some of my games have very high latency
> try enable tearing, refer to [tearing](#tearinggame-mode)
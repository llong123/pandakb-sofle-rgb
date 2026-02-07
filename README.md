# Sofle RGB ZMK Firmware

A ZMK firmware configuration for the Sofle split mechanical keyboard with RGB underglow, OLED display, and rotary encoder support.

## Features

- Bluetooth connectivity with multi-profile support (BT1-BT5)
- RGB underglow with auto-off on idle
- OLED display on both sides with status screens
- Bongo cat animation on left side showing typing activity
- Rotary encoder support (volume/page up/down by default)
- ZMK Studio support with keymap customization
- Configurable idle and deep sleep timeouts
- Adjustable BLE transmit power for improved split communication

## Hardware Requirements

- Sofle keyboard kit
- nice_nano_v2 or compatible microcontroller
- WS2812 RGB LEDs for underglow
- OLED display (SSD1306)
- Rotary encoders (optional)

## Building

### Local Build

1. Install ZMK dependencies:
   ```bash
   west init -m https://github.com/zmkfirmware/zmk --mr main
   west update
   ```

2. Build the firmware:
   ```bash
   west build -b nice_nano_v2 -- -DSHIELD=sofle_left
   west build -b nice_nano_v2 -- -DSHIELD=sofle_right
   ```

   Built firmware will be in `build/zephyr/zmk.uf2`.

### GitHub Actions

Pushes to the `main` branch automatically trigger builds via GitHub Actions. Download built firmware from the Actions tab.

## Keymap

### Layer Overview

| Layer | Name | Description |
|-------|------|-------------|
| 0 | BASE | Default QWERTY layer |
| 1 | LOWER | Function keys and numbers |
| 2 | RAISE | Navigation and Bluetooth |
| 3 | ADJUST | RGB controls and Bluetooth management |

### Default Layer (BASE)

```
,-----------------.               ,-----------------.
| GRA | 1  | 2  | 3  |  4  |  5  |               |  6  |  7  |  8  |  9  |  0  |     |
| ESC | Q  | W  | E  |  R  |  T  |               |  Y  |  U  |  I  |  O  |  P  | BSPC|
| TAB | A  | S  | D  |  F  |  G  |               |  H  |  J  |  K  |  L  | ;  | '   |
|LSHFT| Z  | X  | C  |  V  |  B  | MUTE |RGB_TOG|  N  |  M  | ,  | .  | /  |RSHFT|
     |LGUI|LALT|LCTRL|LOWER|RET  |               |SPACE|RAISE|RCTRL|RALT |RGUI|
     `-----------------'               `-----------------'
```

### Lower Layer (LOWER)

```
,-----------------.               ,-----------------.
|    | F1 | F2 | F3 |  F4 |  F5 |               |  F6 |  F7 |  F8 |  F9 | F10 | F11 |
| `  | 1  | 2  | 3  |  4  |  5  |               |  6  |  7  |  8  |  9  |  0  | F12 |
|EP_TOG| !  | @  | #  |  $  |  %  |               |  ^  |  &  |  *  |  (  |  )  |  |  |
|    |=  | -  | +  |  {  |  }  |        |        |  [  |  ]  |  ;  |  :  |  \  |    |
     |    |    |    |    |    |        |        |    |    |    |    |
     `-----------------'               `-----------------'
```

### Raise Layer (RAISE)

```
,-----------------.               ,-----------------.
|BTCLR|BT1 |BT2 |BT3 |BT4 |BT5 |               |     |     |     |     |     |     |
|     |INS |PSCR| App|    |    |               |PGUP |     | UP  |     |  0  |     |
|     |LALT|LCTRL|LSHF|    |LCK |               |PGDN |LEFT |DOWN |RIGHT| DEL | BSPC|
|     |UNDO| CUT| COPY|PASTE|    |        |        |     |     |     |     |     |     |
     |    |    |    |    |    |        |        |     |     |     |     |
     `-----------------'               `-----------------'
```

### Adjust Layer (ADJUST)

```
,-----------------.               ,-----------------.
|BTCLR|BT1 |BT2 |BT3 |BT4 |BT5 |               |     |     |     |     |     |     |
|EP_TOG|HUD |HUI |SAD |SAI |EFF |               |     |     |     |     |     |     |
|     |BRD |BRI |    |    |    |               |     |     |     |     |     |     |
|     |    |    |    |    |    |        |        |     |     |     |     |     |     |
     |    |    |    |    |    |        |        |     |     |     |     |
     `-----------------'               `-----------------'
```

## Encoders

- Left encoder: Volume up/down
- Right encoder: Page up/down

## OLED Display

### Left Side (Central)

The left side displays the built-in status screen which includes:
- Current layer
- Bluetooth connection status
- Bongo cat animation (shows typing activity)
- Words per minute (WPM)

### Right Side (Peripheral)

The right side displays a basic status screen with:
- Layer indicator
- Battery status
- Connection status

Note: Bongo cat animation only works on the left (central) side because WPM calculations happen on the central side in ZMK split keyboards.

## Configuration

Edit `config/boards/shields/sofle/sofle.conf` to customize:

- Battery reporting interval
- Key debounce timing
- BLE transmit power
- Keyboard name
- Display settings
- Bongo cat animation (`CONFIG_ZMK_WIDGET_BONGO_CAT=y`)
- Sleep timeouts
- RGB settings
- Encoder settings

### Bongo Cat Animation

The bongo cat animation is enabled by default on the left side. To disable it, comment out:
```
CONFIG_ZMK_WIDGET_BONGO_CAT=y
```

## License

MIT License - See individual files for details.

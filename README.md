**USE AT YOUR OWN RISK**

**I AM NOT HELD RESPONSIBLE IF ANYTHING HAPPENS TO YOUR DISPLAY**

I modified the original component to allow quick refresh wich means that you have the option to update the display without it flashing black and white

The original update function that refreshes the display and flashed black and white is still present in this fork

The function to update the display can be called from lambda:
```yaml
- lambda: |
            // Will do a full refresh, but not flash the screen
            my_display->update_from_framebuffer();

            // Will do a full refresh and flash the screen, this method works with the original component too
            my_display->update();
```

Credits to [Nickolay](https://github.com/nickolay) and thanks for creating this component!

This repository contains a Display component for [ESPHome](https://esphome.io/)
to support the ESP32-S3 [LILYGO T5 4.7" Plus E-paper display](https://www.lilygo.cc/products/t5-4-7-inch-e-paper-v2-3).

(Do not confuse it with the original ESP32-based Lilygo T5 4.7 board.)

For more info in the display components, see the [ESPHome display documentation](https://esphome.io/#display-components)

## Usage

To use the board with [ESPHome](https://esphome.io/) **you have to put quite a
number of options in your esphome config**:
* Configure the aprpopriate board, variant, and framework versions in the
[esp32 platform](https://esphome.io/components/esp32.html)
* Set a bunch of `platformio_options`
* Include the component from this repository as `external_components` 

If you clone this repository, a working example is included:

    git clone https://github.com/PrototypeSomething/esphome-lilygo-t547plus.git
    cd esphome-lilygo-t547plus
    esphome run basic.yaml

If you don't want to clone, copy the necessary pieces from [basic.yaml](./basic.yaml)
and adapt the `external_components` configuration as follows:

```yaml
# ... required esp32, platformio_options configuration omitted for brevity ...

external_components:
  - source: github://PrototypeSomething/esphome-lilygo-t547plus
    components: ["t547"]

## for those using ESPHome 2023.6.5 and earlier:
# external_components:
#   - source: github://PrototypeSomething/esphome-lilygo-t547plus@2023.6.5 # Not tested by me but provided by nickolay (github://nickolay/esphome-lilygo-t547plus@2023.6.5)
#     components: [t547]


display:
- platform: t547
  id: t5_display
  update_interval: 30s # Remember to set to "update_interval: never" if using LVGL
```

## Discussion

https://github.com/esphome/feature-requests/issues/1960

# Vendor Configurations Bundled With This Repository

The `config` directory contains machine-specific profiles that are known to
build against the checked-in Marlin source. Use these configurations as a
starting point for your machine or as a reference when creating your own.

To use a configuration, copy the pair of files into `Marlin/Configuration.h`
and `Marlin/Configuration_adv.h`, then rebuild the firmware.

## Available Profiles

| Vendor      | Machine | Profile Path                                                   | Notes |
|-------------|---------|----------------------------------------------------------------|-------|
| FlyingBear  | Ghost 6 | `config/FlyingBear/Ghost6/` | Derived from Marlin `bugfix-2.1.x`, tuned for the FlyingBear Ghost 6. Optional build-time feature flags described below. |

### Build-Time Variations

The bundled configurations can be toggled into several variants without editing the sources. For the Ghost 6 profile, the key feature switches are:

- `BLTOUCH` — enables the BLTouch probe configuration
- `FT_MOTION` — enables the fast-tuned motion parameters

There are two convenient ways to inject these flags:

- **Reuse PlatformIO environments.** `ini/stm32f4.ini` provides ready-made entries such as `env:mks_nano4_v3_1_ft_motion`, `env:mks_nano4_v3_1_bltouch`, and `env:mks_nano4_v3_1_bltouch_ft_motion`. Pick the one you need and run `platformio run -e <env-name>`.
- **Pass custom build flags.** Stay on a single environment and export the desired macros before building:

```
export PLATFORMIO_BUILD_FLAGS="-DBLTOUCH -DFT_MOTION"
platformio run
```

You can also add other overrides, e.g. `-DMOTHERBOARD=BOARD_FLYING_BEAR` or any Marlin compile-time option your setup requires. Omit flags you don’t need and combine them as required for your firmware build.

If you add or update a machine profile, please expand the table above and
include a short note describing the source branch or any special tuning.

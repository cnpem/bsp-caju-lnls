# CAJU Board Support Package (BSP)

This repository provides the **CAJU board support package** for projects based on **Mbed OS CE (Community Edition)**. The CAJU target is based on the **STM32H743** microcontroller.

The BSP defines the CAJU custom target and includes board-specific pin definitions and peripheral configuration sources. It is intended to be used with the CNPEM [Mbed OS CE `ce-master` branch](https://gitlab.cnpem.br/GIE/libraries/mbed-os/-/tree/ce-master).

## Repository structure

| Path | Purpose |
| --- | --- |
| `custom_targets.json` | Defines the `CAJU` custom target and its STM32H743 inheritance. |
| `TARGET_CAJU/CMakeLists.txt` | Defines the `mbed-caju` CMake interface library. |
| `TARGET_CAJU/PinNames.h` | Board pin names and mappings. |
| `TARGET_CAJU/PeripheralPins.c` | Pin maps for supported peripherals. |
| `TARGET_CAJU/system_clock.c` | Board-specific clock configuration source. |
| `TARGET_CAJU/stm32h7_eth_init.c` | Board-specific Ethernet initialization source. |

## 1. Add the BSP as a Git submodule

From the root directory of the firmware project:

```bash
git submodule add https://github.com/cnpem/bsp-caju-lnls.git lib/bsp-caju-lnls
git submodule update --init --recursive
```

The examples below assume that the BSP is checked out at `lib/bsp-caju-lnls`. Adjust the paths if you use another location.

## 2. Configure CMake

In the project's root `CMakeLists.txt`, set the custom target definition path **before Mbed OS processes target configuration**:

```cmake
set(CUSTOM_TARGETS_JSON_PATH
    "${CMAKE_CURRENT_SOURCE_DIR}/lib/bsp-caju-lnls/custom_targets.json"
)
```

Once the Mbed OS CMake targets are available, add the CAJU board library:

```cmake
add_subdirectory(lib/bsp-caju-lnls/TARGET_CAJU)
```

Link `mbed-caju` to your firmware target in the appropriate part of the project's CMake configuration:

```cmake
target_link_libraries(<your-firmware-target> PRIVATE mbed-caju)
```

Replace `<your-firmware-target>` with the actual CMake target name. The exact ordering of these commands depends on the firmware project's Mbed OS integration.

## 3. Configure `mbed_app.json` (if needed)

For a CAJU board without an external low-speed crystal (LSE), add the following target override to the project's `mbed_app.json`:

```json
{
    "target_overrides": {
        "CAJU": {
            "target.lse_available": "0"
        }
    }
}
```

Merge this entry with any existing `target_overrides`; do not replace unrelated application settings.

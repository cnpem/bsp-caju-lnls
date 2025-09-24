# CAJU Board Support Package

This repository provides the CAJU Board Support Package for Mbed OS CE.
It is designed to work with the [Mbed OS CE (Community Edition)](https://gitlab.cnpem.br/GIE/libraries/mbed-os/-/tree/ce-master) branch `ce-master`. 

---

## 1. Add as a Git submodule

In the root of your project:

```bash
git submodule add https://gitlab.cnpem.br/GIE/libraries/mbed-os-caju .
```
----

## 2. Update `CMakeLists.txt`

In your project’s root CMakeLists.txt, add:

```cmake
set(CUSTOM_TARGETS_JSON_PATH custom_targets.json)
add_subdirectory(lib/mbed-os-caju/TARGET_CAJU)

```
---

## 3. Configure `mbed_app.json` (if needed)

If your board does not have an LSE (Low-Speed External) clock source, add the following override in mbed_app.json:

```json
{
    "target_overrides": {
        "CAJU": {
            "target.lse_available": "0"
        }
    }
}

```
---



<p align="center">
<img src="https://github.com/Project-Actinides/manifest/blob/Baklava/ProjectActinides-Logo.png">
</p>

What is ActiniumOS
----------------------
ActiniumOS is Closed source Aftermarket Android Operating System that aims to bring unique and fresh user experience

Base Firmware
----------------------
[**RisingOS Android**](https://github.com/RisingOS-Revived)

Getting Started
----------------------
**Initialize local repository**
```bash
repo init -u https://github.com/Project-Actinides/manifest -b Baklava
```

**Sync up with this command**
```bash
repo sync -c --no-clone-bundle --optimized-fetch --prune --force-sync -j$(nproc --all)
```

Preparing device for building ActiniumOS
-----------------------
**Inherit lineageOS vendor stuff**
```bash
$(call inherit-product, vendor/lineage/config/common_full_phone.mk)
```

Buiilding Flags
-----------------------
```bash
Add the following variables:

#Lunch banner maintainer variable
ACTINIUM_MAINTAINER="Shiru"

# Chipset/Maintainer properties (ro.actinium.chipset/ro.actinium.maintainer)
# Set ACTINIUM_MAINTAINER for version control
# (Optional if builder is setting properties via init_<device>.cpp)
PRODUCT_BUILD_PROP_OVERRIDES += \
  ActiniumChipset="Google Tensor 2" \
  ActiniumMaintainer="Accrese"

ACTINIUM_MAINTAINER := Shiru

# Disable/enable blur support, false by default
TARGET_ENABLE_BLUR := true/false

#Whether to ship aperture camera, false by default
PRODUCT_NO_CAMERA := true/false

#Whether to ship lawnchair launcher, false by default
TARGET_PREBUILT_LAWNCHAIR_LAUNCHER :=true/false
```

GMS Flags
-----------------------
```bash
# GMS build flags, true by default
# Ship with GMS packages, replaces default AOSP packages with Gooogle manufactured packages
WITH_GMS := true/false

#CORE build flags
WITH_GMS := true
TARGET_USES_PICO_GAPPS := true

# VANILLA only build flags
WITH_GMS := false

# VANILLA build with MICROG
WITH_GMS := false
WITH_MICROG := true
```

Building the firmware
-----------------------
**Setting up environment**
```bash
. build/envsetup.sh
```

**riseup uses all available cores to assign jobs hence making -jX no-op, to utilize -jX use:**
```bash
riseup <device> <build-type>
```
```bash
rise b
```

**Building fastboot update package**
```bash
riseup <device> <build-type>
```
```bash
rise fb
```

**Signed build(Repacking with releasekey for play integrity, certification etc.)**
```bash
riseup <device> <build-type>
```
```bash
# Perform manual key generation
# 'gk' will include keys from vendor/lineage-priv/keys
# after generating keys
gk -s

# For more info about gk (generate keys)
gk -h/--help

# Build the firmware with the preferred method except for 'rise sb'
rise/rise b/mka bacon etc.
```

**Building fully signed ota package**
```bash
riseup <device> <build-type>
```
```bash
# 'rise sb' is an attempt to automate LineageOS builds signing.
# Reference: https://wiki.lineageos.org/signing_builds
# In case of errors or any other difficulties, avoid using 'rising sb'
# If the builder wants to simply replace the testkey certificate with the releasekey
# Please refer to 'Replacing testkey to releasekey'
# (Automatic generation of keys will be performed if keys do not exist).
# For manual key generation, please use "gk":
gk -f (to regenerate old keys, rise sb automatically generate keys for full build signing if no keys exists)
rise sb
```

**Opting out of signed builds**
```bash
riseup <device> <build-type>
```
```bash
remove_keys # This will remove generated keys so the system will revert back to test keys.
```

**For more information about rise build command:**
```bash
rise help
```

Credits
---------------
* [**AOSPA**](https://github.com/AOSPA)
* [**AICP**](https://github.com/AICP)
* [**Bootleggers**](https://github.com/BootleggersROM)
* [**crDroid**](https://github.com/crdroidandroid)
* [**Corvus-AOSP**](https://github.com/Corvus-AOSP)
* [**Derpfest**](https://github.com/DerpFest-AOSP)
* [**DivestOS**](https://github.com/Divested-Mobile)
* [**DotOS**](https://github.com/DotOS)
* [**Evolution-X**](https://github.com/Evolution-X)
* [**Flamingo-OS**](https://github.com/Flamingo-OS)
* [**LeafOS**](https://github.com/LeafOS-Project)
* [**LineageOS**](https://github.com/LineageOS)
* [**Octavi-OS**](https://github.com/Octavi-OS)
* [**Omnirom**](https://github.com/omnirom)
* [**PixelDust Caf**](https://github.com/pixeldust-project-caf)
* [**Project-Fluid**](https://github.com/Project-Fluid)
* [**Project Kaleidoscope**](https://github.com/Project-Kaleidoscope)
* [**Project Radiant**](https://github.com/ProjectRadiant)
* [**RisingOS-Revived**](https://github.com/RisingOS-Revived)
* [**minaripenguin**](https://github.com/minaripenguin)
* [**AxionAOSP**](https://github.com/AxionAOSP)
* [**SparkOS**](https://github.com/Spark-Rom)
* [**StagOS**](https://github.com/StagOS)
* [**Xdroid-OSS**](https://github.com/xdroid-oss)

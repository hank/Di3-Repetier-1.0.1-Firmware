This is Repetier firmware, version 1.0.1 configured for the Wanhao Duplicator i3 boards.
In order to use the firmware, a lot of features had to be disabled to fit on the Sanguino 1248P Melzi mainboard.

This firmware is in alpha; use at your own risk. It is open for pull-requests and similar functionality in order to fix any issues.

Please use descriptive descriptions when submitting a pull-request.

If you find a new issue, please report it to the Issues for this repository.

This repository was started as part of the discussions [here](https://groups.google.com/forum/#!topic/wanhao-printer-3d/ZhPeAmiLRak).

Please use that thread as a guide on how to install the firmware on your Di3 as well as how it should be configured.

# Compilation settings

The default Arduino AVR avr-g++ settings use -Os, but there are various optimizations left out of -Os that can help get code size down. The greatest optimization is detailed [here](https://www.microchip.com/webdoc/AVRLibcReferenceManual/FAQ_1faq_optflags.html), and manages to shave off **2,108** bytes on its own! The only possible ill effects are a slight (a few percent) difference in performance when calling functions. Most of this project is written such that inline functions and other optimizations mitigate this issue.

```
## DEFAULT ARDUINO SETTINGS
## Sketch uses 130468 bytes (100%) of program storage space. Maximum is 130048 bytes.
# compiler.cpp.flags=-c -g -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto
## Sketch uses 127424 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -finline-limit=3 -fno-inline-small-functions -mcall-prologues -Wl,--relax -fno-tree-scev-cprop -fno-split-wide-types
## Sketch uses 127814 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -finline-limit=3 -fno-inline-small-functions -mcall-prologues -Wl,--relax -fno-tree-scev-cprop
## Sketch uses 127870 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -finline-limit=3 -fno-inline-small-functions -mcall-prologues -Wl,--relax
## Sketch uses 127870 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -finline-limit=3 -fno-inline-small-functions -mcall-prologues
## Sketch uses 129974 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -finline-limit=3 -fno-inline-small-functions
## Sketch uses 130444 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -finline-limit=3
## mcall-prologues can slightly decrease performance, but is generally safe
## More information: https://www.microchip.com/webdoc/AVRLibcReferenceManual/FAQ_1faq_optflags.html
## Sketch uses 128280 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -mcall-prologues
## Sketch uses 128308 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -fpack-struct -mcall-prologues
## Sketch uses 128308 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -funsigned-bitfields -mcall-prologues
## Sketch uses 128308 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -funsigned-char -mcall-prologues
## Sketch uses 128360 bytes
# compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -mcall-prologues

### FINAL VALUE, must change in Arduino/hardware/arduino/avr/platform.txt
compiler.cpp.flags=-c -Os {compiler.warning_flags} -std=gnu++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics -MMD -flto -mcall-prologues

```


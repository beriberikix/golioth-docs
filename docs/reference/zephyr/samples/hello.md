---
title: Golioth Hello sample
---

# Overview

This sample application demonstrates how to connect with Golioth and
publish simple Hello messages.

# Requirements

-   Golioth credentials
-   Network connectivity

# Building and Running

Configure the following Kconfig options based on your Golioth
credentials:

-   GOLIOTH_SERVER_DTLS_PSK_ID - PSK ID of registered device
-   GOLIOTH_SERVER_DTLS_PSK - PSK of registered device

by adding these lines to configuration file (e.g. `prj.conf`):

``` {.cfg}
CONFIG_GOLIOTH_SERVER_DTLS_PSK_ID="my-psk-id"
CONFIG_GOLIOTH_SERVER_DTLS_PSK="my-psk"
```

## Platform specific configuration

### QEMU

This application has been built and tested with QEMU x86 (qemu_x86) and
QEMU ARM Cortex-M3 (qemu_cortex_m3).

On your Linux host computer, open a terminal window, locate the source
code of this sample application (i.e., `samples/hello`) and type:

``` {.console}
$ west build -b qemu_x86 samples/hello
$ west build -t run
```

See [Networking with
QEMU](https://docs.zephyrproject.org/latest/guides/networking/qemu_setup.html#networking-with-qemu)
on how to setup networking on host and configure NAT/masquerading to
access Internet.

### ESP32

Configure the following Kconfig options based on your WiFi AP
credentials:

-   ESP32_WIFI_SSID - WiFi SSID
-   ESP32_WIFI_PASSWORD - WiFi PSK

by adding these lines to configuration file (e.g. `prj.conf` or
`board/esp32.conf`):

``` {.cfg}
CONFIG_ESP32_WIFI_SSID="my-wifi"
CONFIG_ESP32_WIFI_PASSWORD="my-psk"
```

On your host computer open a terminal window, locate the source code of
this sample application (i.e., `samples/hello`) and type:

``` {.console}
$ west build -b esp32 samples/hello
$ west flash
```

See
[ESP32](https://docs.zephyrproject.org/latest/boards/xtensa/esp32/doc/index.html)
for details on how to use ESP32 board.

## Sample output

This is the output from the serial console:

``` {.console}
[00:00:00.000,000] <inf> golioth_hello: Initializing golioth client
[00:00:00.000,000] <inf> golioth_hello: Golioth client initialized
[00:00:00.000,000] <inf> golioth_hello: Sending hello! 0
[00:00:00.000,000] <wrn> golioth_hello: Failed to send hello!
[00:00:00.000,000] <inf> golioth_hello: Starting connect
[00:00:00.000,000] <inf> golioth_hello: Client connected!
[00:00:05.010,000] <inf> golioth_hello: Sending hello! 1
[00:00:05.020,000] <dbg> golioth_hello: Payload
                                        48 65 6c 6c 6f 20 6d 61  72 6b                   |Hello ma rk
[00:00:10.030,000] <inf> golioth_hello: Sending hello! 2
[00:00:10.030,000] <dbg> golioth_hello: Payload
                                        48 65 6c 6c 6f 20 6d 61  72 6b                   |Hello ma rk
```

Responses to Hello messages are printed above as a hexdump of \"Hello
mark\". This means that communication with Golioth is working.

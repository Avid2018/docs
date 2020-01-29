---
title: Troubleshooting Tools
layout: support.hbs
columns: two
devices: [ photon,electron,core,argon,boron,xenon ]
order: 10
---

# Troubleshooting Tools

Here are some tools to help you as you troubleshoot your {{device}}.

{{#if has-listening}}

## Listening Mode Commands

It is possible to put your {{device}} in [Listening Mode](/tutorials/device-os/led/#listening-mode) to get some information about its system, version, and MAC address, and Device ID. {{#if has-wifi}}You can even add Wi-Fi credentials with this method.{{/if}}

### Setup

#### For Windows

For Windows users, we recommend downloading [PuTTY](http://www.putty.org/). 

Plug your device into your computer over USB. When the {{device}} is in [Listening Mode](/tutorials/device-os/led/#listening-mode), open a serial port over USB using the standard settings, which should be:

- Baud rate: 9600
- Data Bits: 8
- Parity: none
- Stop Bits: 1


#### For macOS or Linux

On macOS (OS X) and Linux systems, you can access the serial monitor through the terminal.

For macOS, open the terminal and type:

```screen /dev/tty.u```

and pressing tab to autocomplete.

On Linux, you can accomplish the same thing by using:

```screen /dev/ttyACM```

and pressing tab to autocomplete.

Now you are ready to type some commands to get info about your device.

{{#if has-wifi}}
### Display MAC Address

To display the MAC address of your device, type `m`

This will give an output something like:

```
Your device MAC address is
1a:2b:34:5c:6d:78
```
{{/if}} {{!-- has-wifi --}}

### Get Device ID [deviceID] CLI method
_Using the Particle CLI_
* Put your device into [Listening Mode](/tutorials/device-os/led/#listening-mode) mode while being plugged into a computer via USB
* Issue `particle serial identify` from the [Particle CLI](/tutorials/developer-tools/cli)
	and it should return the deviceID.

### Get Device ID

To display the device ID of your {{device}}, type `i`

This will give an output that looks like:

```
Your device id is 1a2345678912345678901234
```

{{#if has-cellular}}
The IMEI of the cellular modem will also be printed.
{{/if}} {{!-- has-cellular --}}

### Display Device OS Version

To get the Device OS (previously called system firmware) version of your device, type `v`

This will give you an output indicating the [firmware](https://github.com/particle-iot/device-os/blob/develop/CHANGELOG.md) that your device is using.

Sample output:

```
system firmware version: 0.4.6
```

### Display System Information

For debugging purposes, sometimes it helps to get a dump of all the system information. For this, you can press `s`

The output will be a big confusing mess, which is why most of the time you won't need to use it. Occasionally, though, Particle Support might ask you for it. It looks something like this:

```
{"p":6,"m":[{"s":16384,"l":"m","vc":30,"vv":30,"f":"b","n":"0","v":4,"d":[]},{"s":262144,"l":"m","vc":30,"vv":30,"f":"s","n":"1","v":7,"d":[]},{"s":262144,"l":"m","vc":30,"vv":30,"f":"s","n":"2","v":7,"d":[{"f":"s","n":"1","v":7,"_":""}]},{"s":131072,"l":"m","vc":30,"vv":30,"u":"5CC350CE567187492F6FA800655CECF42DCFE1236EC7E23CDB17ECBC1774EDAF","f":"u","n":"1","v":3,"d":[{"f":"s","n":"2","v":7,"_":""}]},{"s":131072,"l":"f","vc":30,"vv":0,"d":[]}]}
```

{{#if has-wifi}}
### Configure Wi-Fi

You can also configure your Wi-Fi using this method. The key for Wi-Fi configuration is `w`

The configuration process will be almost identical to the process laid out in the Particle CLI command `particle serial wifi`

{{/if}} {{!-- has-wifi --}}

{{/if}} {{!-- has-listening --}}

{{#if has-dfu}}

## DFU Commands

There are a number of low-level commands that can be used in [DFU mode](/tutorials/device-os/led/#dfu-mode-device-firmware-upgrade-) 

{{#if core}}
### Core DFU commands:

**User firmware**

`dfu-util -d 1d50:607f -a 0 -s 0x08005000 -D user-firmware.bin`

**Factory reset firmware**

`dfu-util -d 1d50:607f -a 1 -s 0x00020000 -D factory-firmware.bin`

**Particle cloud public key**

`dfu-util -d 1d50:607f -a 1 -s 0x00001000 -D cloud_public.der`

**Device private key**

`dfu-util -d 1d50:607f -a 1 -s 0x00002000 -D device-private.der`

{{/if}} {{!-- core --}}

{{#if photon}}

### Photon DFU commands:

**System Part 1**

`dfu-util -d 2b04:d006 -a 0 -s 0x8020000 -D system-part1.bin`

**System Part-2**

`dfu-util -d 2b04:d006 -a 0 -s 0x8060000 -D system-part2.bin`

**User firmware**

`dfu-util -d 2b04:d006 -a 0 -s 0x80A0000 -D user-firmware.bin`

**Factory reset firmware**

`dfu-util -d 2b04:d006 -a 0 -s 0x80E0000 -D factory-firmware.bin`

**Particle cloud public key**

`dfu-util -d 2b04:d006 -a 1 -s 2082 -D cloud_public.der`

**Device private key**

`dfu-util -d 2b04:d006 -a 1 -s 34 -D device-private.der`


### P1 DFU commands:

***

**System Part 1**

`dfu-util -d 2b04:d008 -a 0 -s 0x8020000 -D system-part1.bin`

**System Part-2**

`dfu-util -d 2b04:d008 -a 0 -s 0x8060000:leave -D system-part2.bin`

**User firmware**

`dfu-util -d 2b04:d008 -a 0 -s 0x80A0000 -D user-firmware.bin`

**Factory reset firmware**

`dfu-util -d 2b04:d008 -a 0 -s 0x80E0000 -D factory-firmware.bin`

**Particle cloud public key**

`dfu-util -d 2b04:d008 -a 1 -s 2082 -D cloud_public.der`

**Device private key**

`dfu-util -d 2b04:d008 -a 1 -s 34 -D device-private.der`

{{/if}} {{!-- photon --}}

{{#if electron}}

### Electron DFU commands:

{{!-- TODO: Verify for accuracy! --}}

**System Part 1**

`dfu-util -d 2b04:d00a -a 0 -s 0x8060000 -D system-part1.bin`

**System Part-2**

`dfu-util -d 2b04:d00a -a 0 -s 0x8020000 -D system-part2.bin`

**System Part-3**

`dfu-util -d 2b04:d00a -a 0 -s 0x8040000 -D system-part3.bin`

**User firmware**

`dfu-util -d 2b04:d00a -a 0 -s 0x8080000 -D user-firmware.bin`

**Factory reset firmware**

`dfu-util -d 2b04:d00a -a 0 -s 0x80A0000 -D factory-firmware.bin`

**Particle cloud public key**

`dfu-util -d 2b04:d00a -a 1 -s 3298 -D cloud_public.der`

**Device private key**

`dfu-util -d 2b04:d00a -a 1 -s 3106 -D device-private.der`


{{/if}} {{!-- electron --}}

{{/if}} {{!-- has-dfu --}}

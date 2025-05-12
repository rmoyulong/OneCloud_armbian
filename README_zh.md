# armbian-onecloud

[![build](https://img.shields.io/github/actions/workflow/status/hzyitc/armbian-onecloud/ci.yml)](https://github.com/hzyitc/armbian-onecloud/actions/workflows/ci.yml) [![downloads](https://img.shields.io/github/downloads/hzyitc/armbian-onecloud/total)](https://github.com/hzyitc/armbian-onecloud/releases) [![downloads@latest](https://img.shields.io/github/downloads/hzyitc/armbian-onecloud/latest/total)](https://github.com/hzyitc/armbian-onecloud/releases/latest)

[README](README.md) | [中文文档](README_zh.md)

**所有修改均已提交至[官方仓库](https://github.com/armbian/build)，您可以直接使用[官方仓库](https://github.com/armbian/build)进行编译。**

## 第一次登录

主机名: `onecloud`

账号:  `root`

密码: `1234`

## 编译参数

### `BOARD`=`onecloud`

### `BRANCH`={`edge`,`current`}

| BRANCH    | 内核版本 | eMMC | HDMI | VPU |
| :-:       | :-:     | :-:  | :-:  | :-: |
| `edge`    | `v6.6`  | ✔️¹  | ✔️² | ✔️² |
| `current` | `v6.1`  | ✔️¹  | ✔️² | ✔️² |

> ¹: 需要补丁
>
> ²: 通过补丁支持

## 如何从`u-boot`启动？

### 从`USB`启动

```
setenv bootdev "usb 0"
usb start
fatload ${bootdev} 0x20800000 boot.scr && autoscr 0x20800000
```

### 从`eMMC`启动

```
setenv bootdev "mmc 1"
fatload ${bootdev} 0x20800000 boot.scr && autoscr 0x20800000
```

## `GPIO`

板子上面有一个44脚的空焊盘(推测可能是WiFi模块)。上面有大量直连`SoC`的引脚，可用作`GPIO`。

具体定义参见`dts`(由 `patch/kernel/meson-{edge,current}/onecloud-0001-add-dts.patch` 添加)

注：`dts`中的引脚是在`V1.0的板子`上测量出来的，未在`V1.3的板子`上面验证。

## 相关链接

[`armbian/build`](https://github.com/armbian/build) - Armbian官方仓库

[`xdarklight/linux@meson-mx-integration-5.18-20220516`](https://github.com/xdarklight/linux/commits/meson-mx-integration-5.18-20220516) - `HDMI`补丁源码

[`S805_Datasheet V0.8 20150126.pdf`](https://dn.odroid.com/S805/Datasheet/S805_Datasheet%20V0.8%2020150126.pdf) - S805数据手册

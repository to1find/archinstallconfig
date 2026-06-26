# 引导式安装 — python-archinstall v2.3.0 文档

# 引导式安装

Archinstall 内置了一个预编程的引导式安装程序（Guided Installer），引导您完成必要的步骤以及一些可选配置。

> **注意**
> 其他预编程脚本可以通过执行 `archinstall --script <名称>`（不含 `.py`）来调用。要查看完整的脚本列表，请运行 `archinstall --script list` 或查看源代码中的 scripts 目录。

> **注意**
> 建议从官方 Arch Linux ISO 中运行 `archinstall`。

> **警告**
> 安装程序不会在安装开始前配置 WiFi。在继续之前，您需要先了解 Arch Linux 网络配置的相关知识。

---

## 运行引导式安装

要启动安装程序，请在最新的 Arch Linux ISO 中运行以下命令：

---


```bash
archinstall
```

由于引导式安装程序是默认脚本，因此这等同于运行 `archinstall guided`。

引导式安装还支持使用预先配置好的答案进行安装。这在需要重复运行一次或多次安装时是一种快速便捷的方式。

共有两个配置文件，均为可选。

---

### --config

该参数接受一个本地 `.json` 文件作为参数，其中包含引导式安装程序的整体配置和菜单答案。

### --config-url

该参数接受一个远程 `.json` 文件作为参数，其中包含引导式安装程序的整体配置和菜单答案。

> **注意**
> 您始终可以通过 `archinstall --dry-run` 获取该文件的最新选项，该命令以安全模式运行引导式安装程序，不会对系统执行任何永久性操作，但会模拟运行并将配置保存到磁盘。

### 使用示例

```bash

archinstall --config config.json

```

```bash

archinstall --config-url https://domain.lan/config.json

```

`https://domain.lan/config.json` 的内容：

```json
{
  "additional-repositories": [],
  "archinstall-language": "English",
  "audio_config": null,
  "bootloader_config": {
    "bootloader": "Systemd-boot",
    "uki": false,
    "removable": false
  },
  "bootloader": "Systemd-boot",
  "debug": false,
  "disk_config": {
    "config_type": "manual_partitioning",
    "device_modifications": [
      {
        "device": "/dev/sda",
        "partitions": [
          {
            "btrfs": [],
            "flags": ["boot"],
            "fs_type": "fat32",
            "length": {
              "sector_size": null,
              "total_size": null,
              "unit": "B",
              "value": 99982592
            },
            "mount_options": [],
            "mountpoint": "/boot",
            "obj_id": "369f31a8-2781-4d6b-96e7-75680552b7c9",
            "start": {
              "sector_size": {
                "sector_size": null,
                "total_size": null,
                "unit": "B",
                "value": 512
              },
              "total_size": null,
              "unit": "sectors",
              "value": 34
            },
            "status": "create",
            "type": "primary"
          },
          {
            "btrfs": [],
            "flags": [],
            "fs_type": "fat32",
            "length": {
              "sector_size": null,
              "total_size": null,
              "unit": "B",
              "value": 100000000
            },
            "mount_options": [],
            "mountpoint": "/efi",
            "obj_id": "13cf2c96-8b0f-4ade-abaa-c530be589aad",
            "start": {
              "sector_size": {
                "sector_size": null,
                "total_size": null,
                "unit": "B",
                "value": 512
              },
              "total_size": {
                "sector_size": null,
                "total_size": null,
                "unit": "B",
                "value": 16106127360
              },
              "unit": "MB",
              "value": 100
            },
            "status": "create",
            "type": "primary"
          },
          {
            "btrfs": [],
            "flags": [],
            "fs_type": "ext4",
            "length": {
              "sector_size": null,
              "total_size": null,
              "unit": "B",
              "value": 15805127360
            },
            "mount_options": [],
            "mountpoint": "/",
            "obj_id": "3e75d045-21a4-429d-897e-8ec19a006e8b",
            "start": {
              "sector_size": {
                "sector_size": null,
                "total_size": null,
                "unit": "B",
                "value": 512
              },
              "total_size": {
                "sector_size": null,
                "total_size": null,
                "unit": "B",
                "value": 16106127360
              },
              "unit": "MB",
              "value": 301
            },
            "status": "create",
            "type": "primary"
          }
        ],
        "wipe": false
      }
    ]
  },
  "disk_encryption": {
    "encryption_type": "luks",
    "partitions": ["3e75d045-21a4-429d-897e-8ec19a006e8b"]
  },
  "hostname": "archlinux",
  "kernels": ["linux"],
  "locale_config": {
    "kb_layout": "us",
    "sys_enc": "UTF-8",
    "sys_lang": "en_US"
  },
  "mirror_config": {
    "custom_servers": [
      {
        "url": "https://mymirror.com/$repo/os/$arch"
      }
    ],
    "mirror_regions": {
      "Australia": [
        "http://archlinux.mirror.digitalpacific.com.au/$repo/os/$arch"
      ]
    },
    "optional_repositories": ["testing"],
    "custom_repositories": [
      {
        "name": "myrepo",
        "url": "https://myrepo.com/$repo/os/$arch",
        "sign_check": "Required",
        "sign_option": "TrustAll"
      }
    ]
  },
  "network_config": {},
  "no_pkg_lookups": false,
  "ntp": true,
  "offline": false,
  "packages": [],
  "parallel downloads": 0,
  "profile_config": null,
  "save_config": null,
  "script": "guided",
  "silent": false,
  "swap": true,
  "timezone": "UTC",
  "version": "2.6.0"
}
```

---

### --config 选项

> **警告**
> 所有键和值条目必须符合 JSON 标准。下表中给出的是可读的示例并附有链接，实际上可能违反 JSON 语法。请根据您的需要和 JSON 格式调整以下描述。

> **注意**
> 向右滚动表格可查看必填选项。

| 键 | 值 | 描述 | 必填 |
| --- | --- | --- | --- |
| `additional-repositories` | `[multilib, testing]` | 在继续安装前启用 testing 和/或 multilib 仓库 | 否 |
| `archinstall-language` | 语言代码 | 设置 TUI 使用的语言（请使用 `lang` 值而非 `abbr`） | 否 |
| `audio_config` | 音频服务器对象 | 要安装的音频服务器 | 否 |
| `bootloader_config` | `{ bootloader: Systemd-boot/grub/limine, uki: true/false, removable: true/false }` | 引导加载程序配置。`bootloader` 选择安装哪个引导加载程序（BIOS 上必须使用 grub/limine）。`uki` 启用统一内核镜像（仅 UEFI，仅 systemd-boot/limine）。`removable` 安装到默认可移动介质路径 /EFI/BOOT/ 而非 NVRAM（仅 UEFI，仅 grub/limine） | 是 |
| `debug` | `true`, `false` | 启用调试输出 | 否 |
| `disk_config` | 磁盘配置对象 | 包含安装期间要使用的磁盘设置 | 否 |
| `disk_encryption` | 磁盘加密对象 | 应用于 `disk_config` 之上的磁盘加密参数 | 否 |
| `hostname` | `str` | 定义机器在网络上的主机名（默认为 `archinstall`） | 否 |
| `kernels` | `["linux", "linux-lts", ...]` | 定义应安装哪些内核并设置到引导加载程序选项中 | 是 |
| `custom_commands` | 自定义命令列表 | 安装后在 chroot 环境中运行的命令 | 否 |
| `locale_config` | `{kb_layout: lang, sys_enc: 字符编码, sys_lang: locale}` | 定义键盘布局、系统编码和系统语言环境 | 否 |
| `mirror_config` | `{custom_mirrors: [https://…], mirror_regions: { "Worldwide": ["https://geo.mirror.pkgbuild.com/$repo/os/$arch"] } }` | 设置各种镜像源（如未定义，则默认使用 ISO 中的 `/etc/pacman.d/mirrors`） | 否 |
| `network_config` | 网络配置对象 | 设置应使用的网络配置类型 | 否 |
| `no_pkg_lookups` | `true`, `false` | 禁用向 https://archlinux.org/packages/ 的软件包检查 | 否 |
| `ntp` | `true`, `false` | 安装期间启用或禁用 NTP | 否 |
| `offline` | `true`, `false` | 启用或禁用某些在线检查（如镜像可达性等） | 否 |
| `packages` | `[<包名>, <包名>, ...]` | 安装期间需要安装的软件包列表 | 否 |
| `parallel downloads` | `0-∞` | 设置 pacman 使用的并行下载数量 | 否 |
| `profile_config` | 配置文件对象 | 如果定义了配置文件，则安装该配置文件 | 否 |
| `script` | `guided`（默认）, `minimal`, `only_hdd` | 用于自动运行安装时，设置要自动运行的脚本 | 否 |
| `silent` | `true`, `false` | 启用或禁用 TUI 用户交互 | 否 |
| `swap` | `true`, `false` | 启用或禁用 swap | 否 |
| `timezone` | 时区字符串 | 为安装的系统设置时区 | 否 |

#### JSON 选项

> **注意**
> 如果 `disk_config` 中未定义任何内容，archinstall 引导式安装将使用当前挂载在 `/mnt/archinstall` 下的内容，而不执行任何磁盘操作。

---

## --creds 选项

Creds 是一个独立的配置文件，用于将普通选项与密码等敏感数据分开。以下是设置 root 密码的示例，以及可设置的其他值的说明。

```json
{
    "root_enc_password": "SecretSanta2022"
}
```

| 键 | 值 | 描述 | 必填 |
| --- | --- | --- | --- |
| `!encryption-password` | `str` | 磁盘加密密码；如不提供密码则不加密 | 否 |
| `root_enc_password` | `str` | root 账户密码 | 否 |
| `users` | `{ "username": "<用户名>", "enc_password": "<密码哈希>", "sudo": false }` | 普通用户凭据列表 | 否 |


# 运行命令

```bash
archinstall --config-url https://raw.githubusercontent.com/to1find/archinstallconfig/main/config.json
```

| OKI<br>内核 | 6.12 | 6.6 | 6.1 | 5.15 | 5.10
|:---:|:---:|:---:|:---:|:---:|:---:|
| 状态 | ✅完美运行 | ✅完美运行 | ✅完美运行 | ✅完美运行 | ✅完美运行 |
| 说明 | Droidspaces≥v5.9.5 | Droidspaces全版本支持 | • Droidspaces≥v5.9.5：仅打04.sysvipc_task_struct.patch<br>• 更低版本：打全所有补丁 | • Droidspaces≥v5.9.5：仅打04.sysvipc_task_struct.patch<br>• 更低版本：打全所有补丁 |Droidspaces≥v5.9.5 |
| NTsync所需补丁 | 仅打android16-6.12.patch | ntsync_base.patch<br>+<br>android15-6.6.patch | ntsync_base.patch<br>+<br>android14-6.1.patch | ntsync_base.patch<br>+<br>android13-5.15.patch | ntsync_base.patch<br>+<br>android12-5.10.patch(对应版本) |
| 测试通过的机型 | <div align="left">• 一加15<br>• 一加Pad3Pro</div> | <div align="left">• 一加Pad2Pro<br>• 一加13<br>• 一加Ace6<br>• 一加Ace5Pro<br>• 一加13T<br>• 一加Ace5至尊版(系统更新)<br>• 华硕rog9pro</div> | <div align="left">• 一加Ace3Pro<br>• 一加12<br>• 一加PadPro<br>• 真我GT5Pro</div> | <div align="left">• 一加Ace3</div> |<div align="left">• 一加Ace 竞速版</div> |

| GKI<br>内核 | 6.12 | 6.6 | 6.1 | 5.15 | 5.10 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 状态 | ✅完美运行 | ✅完美运行 | ✅完美运行 | ✅完美运行 | ✅完美运行 |
| 说明 | Droidspaces全版本支持 | Droidspaces≥v5.9.5 | Droidspaces≥v5.9.5 | Droidspaces≥v5.9.5 | Droidspaces≥v5.9.5 |
| NTsync所需补丁 | 仅打android16-6.12.patch <br>• 米系设备使用可能会造成无法开热点等问题 | ntsync_base.patch<br>+<br>android15-6.6.patch | ntsync_base.patch<br>+<br>android14-6.1.patch | ntsync_base.patch<br>+<br>android13-5.15.patch | ntsync_base.patch<br>+<br>android12-5.10.patch |
| 测试通过的机型 | <div align="left">• 红米K90ProMax<br>• 小米17 系列<br>• 红魔11<br>• 荣耀magicPad3Pro</div> | <div align="left">• 小米Pad8Pro<br>• 小米15</div> | <div align="left">• 小米14<br>• 小米Pad7<br>• 小米mix Flip<br>• 红魔9SPro+<br>• 红魔9Pro<br>• 掌玩Mini 3 Ultra</div> | <div align="left">• 小米Pad6SPro<br>• 红米K70</div> | <div align="left">• 小米Pad6Max<br>• 小米Pad6Pro<br>• 红米K50Ultra<br>• 红米K60<br>• 摩托罗拉x30Pro</div> |


> `⚠️ 测试中` 代表的是可能出现不定时重启
> 
> `✅ 完美运行 ` 代表的是经过多数设备的长期验证，可以稳定运行
> 
> `❓ 未测试` 代表的是无设备验证，不确定是否稳定
>
> `GKI` 只代表米系设备经过验证,但其他设备应该也可以
>
> `💡Droidspaces` 所要文件 [点我跳转](https://cdn.goldzxcbug.top/%E7%A7%BB%E5%8A%A8-Droidspaces-OSS)

# 内核编译指南
> [!IMPORTANT]
> 如果你是新手，你可以按照下面两个指南来编译属于你自己的内核
>- [OKI内核云编译指南](./doc/OKI_kernel.md)
>
>- [GKI内核云编译指南](./doc/GKI_kernel.md)


## Droidspaces ≥ v5.9.5 所要配置
```txt
# IPC
CONFIG_SYSVIPC=y
CONFIG_POSIX_MQUEUE=y

# 命名空间
CONFIG_IPC_NS=y
CONFIG_PID_NS=y

# 硬件访问
CONFIG_DEVTMPFS=y

# 用户命名空间(不是必备，但是docker,KDE桌面必须要开)
CONFIG_USER_NS=y
```

## Droidspaces < v5.9.5 所要配置
```txt
# 修复 [✗] PID namespace 和 [✗] IPC
CONFIG_SYSCTL=y
CONFIG_SYSVIPC=y
CONFIG_POSIX_MQUEUE=y
CONFIG_NAMESPACES=y
CONFIG_PID_NS=y
CONFIG_IPC_NS=y
CONFIG_UTS_NS=y
CONFIG_USER_NS=y
# 修复 [✗] devtmpfs support
CONFIG_DEVTMPFS=y
CONFIG_DEVTMPFS_MOUNT=y
# 修复 cgroup devices support
CONFIG_CGROUPS=y
CONFIG_CGROUP_DEVICE=y
CONFIG_CGROUP_PIDS=y
CONFIG_MEMCG=y
```
## Droidspaces 格外配置（可选）
```txt
#网络（Docker/NAT支持）
CONFIG_NETFILTER_XT_MATCH_ADDRTYPE=y

#UFW 支持
CONFIG_NETFILTER_XT_TARGET_REJECT=y
CONFIG_NETFILTER_XT_TARGET_LOG=y
CONFIG_NETFILTER_XT_MATCH_RECENT=y

#Fail2ban 支持
CONFIG_IP_SET=y
CONFIG_IP_SET_HASH_IP=y
CONFIG_IP_SET_HASH_NET=y
CONFIG_NETFILTER_XT_SET=y

# 在 tmpfs 上启用 xattr 支持
# (运行 NixOS 必备选项)
CONFIG_TMPFS_XATTR=y
```
## NTsync 所要配置
```txt
CONFIG_NTSYNC=y
```

## Patch 补丁来源
- [Droidspaces](https://github.com/ravindu644/Droidspaces-OSS/tree/main/Documentation/resources/kernel-patches)
- [WildKernels](https://github.com/WildKernels/kernel_patches/tree/main/common)

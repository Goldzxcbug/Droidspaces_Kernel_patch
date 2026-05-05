# GKI内核 云端编译指南 
- 适用设备：小米，红米
- 适用内核版本：6.1-6.12
>[!TIP]
>
>本教程仅适用于编译支持 **Droidspaces** 和 **NTsync** 的内核
>
>请严格按照教学，以确保内核编译不出错并完美运行


## 前提准备：
- 知道 [Droidspaces项目](https://github.com/ravindu644/Droidspaces-OSS) 是干什么的
- 一台解了 Bootloader 锁的设备，设备建议高通骁龙(否则没有GPU加速)
- 查看 `设置－>我的设备->全部参数与信息->内核版本` 是否为 `5.10.xxx~6.12.xxx` 内核版本
- 备份好你的手机对应的原 `Boot` 文件
- 系统必须是 `MIUI` `HyperOS`

## 配置
### 1.查看本项目主页的表格的GKI系列的内核版本状态是否有 ✅完美运行
- 如果你的机型正好是测试通过的机型，那么恭喜你，你只要严格按照本教程来，100%获得完美支持DroidSpaces的内核
- 你的机型如果不是测试通过的机型，那也不用慌张，打上内核版本相同的补丁，大概率也可以获得完美支持DroidSpaces的内核
### 2.Fork [zzh20188](https://github.com/zzh20188) 的内核项目
- GKI内核5.10~6.12 https://github.com/zzh20188/GKI_KernelSU_SUSFS

>[!WARNING]
>我在写这个教程的时候，作者已经添加了对 `Droidspaces` 的实验性支持，我看了看代码，基本没有问题
>
>但还是要备份好你的手机对应的原 `Boot` 文件

![例子](./Image/GKI_1.png)
### 3.

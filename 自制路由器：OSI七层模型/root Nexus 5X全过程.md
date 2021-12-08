# 名词解释：
https://forum.xda-developers.com/t/nexus-4-guide-unlock-bootloader-root-install-custom-recoveries-custom-roms-kernel.2266654/
  1. **What is Bootloader and Why do we need to Unlock?**
     A bootloader is a boot initializing component which is generally locked by the device manufacturer to avoid any messing around with the OS. We need to unlock it for the same reason. Once unlocked it will allow us to change the boot sequence and modify the OS in accordance of our needs.

  2. two ways of root:

  3. either by manual method (using Recoveries) or by automatic method (using toolkit or software) . Here, I am going to follow the manual method  .

# 原网站:
r0ysue https://mp.weixin.qq.com/s?__biz=Mzg3MjU3NzU1OA==&mid=2247496397&idx=2&sn=52455f90262683278013f4cc09ced831&source=41#wechat_redirect

# 步骤
1. 步骤一： 安装Android 8.0.1版本。一般咱们买回来的nexus 5X是Android 6.0.1的，但是咱们一般都不用这个版本系统进行root，咱们一般使用8.1.0版本系统进行root。

   1. 首先，进入官方网站：https://developers.google.com/android/images#bullhead，复制下载8.1.0 (OPM7.181205.001, Dec 2018)的链接，这里直接贴上：https://dl.google.com/dl/android/aosp/bullhead-opm7.181205.001-factory-5f189d84.zip；

    2. 进入kali虚拟机，wget下载8.1.0系统 wget https://dl.google.com/dl/android/aosp/bullhead-opm7.181205.001-factory-5f189d84.zip. 下载完毕后使用命令：openssl dgst -sha256 bullhead-opm7.181205.001-factory-5f189d84.zip   查看sha256是否为 SHA256(bullhead-opm7.181205.001-factory-5f189d84.zip)= 5f189d84781a26b49aca0de84a941a32ae0150da0aab89f1d7709d56c31b3c0a 。如果是，证明下载的系统没有损坏。

     3. 将手机进入fastboot模式：

     4. 1. 断开手机USB线；

        2. 关机

        3. 手机电量必须大于80%

        4. 持续按住音量下键和电源键

        5. 这里必须保证fastboot状态的DEVICE STATE一栏为: unlock，证明咱们解锁了。至于如何解锁请看：https://developer.android.com/studio/debug/dev-options?hl=zh-cn

        6. 注意：手机进入fastboot除了按键这种方法外还有别的方法：

        7. 1. ``adb reboot bootloader``
           2. ``adb reboot -bootloader``
           3. ``adb reboot fastboot``

     5. 如何把Android8.1.0刷入手机具体查看原网站https://mp.weixin.qq.com/s?__biz=Mzg3MjU3NzU1OA==&mid=2247496397&idx=2&sn=52455f90262683278013f4cc09ced831&source=41#wechat_redirect

  2. 步骤二：下载twrp关于bullhead的镜像：

   3. 下载最新版twrp地址：https://dl.twrp.me/bullhead/，记住这里面的链接时地址链接，不是下载链接。

            2. adb传输Magisk到手机上sdcard卡上。注意这里传输的是Magisk的zip文件。https://github.com/topjohnwu/Magisk/releases/tag/v23.0找链接中最新版的Magisk页面，往下翻，找到Source Code(Zip)，进行下载。下载完之后，要进行**校验md5**。

         >如果最后在用twrp刷入Magisk的时候报错:**Zip file is corrupt!**那就说明刷入的文件有问题，一定要在下载完后校验md5。如果v23.0出错，那就试试经典的v17.3版本吧。注意：不知到为什么nexus5(Android 9 pie) root之后，输入命令``adb shell``直接进入``root``模式了，不用再输入``su``。

            3. fastboot命令刷入:
                 1. 注意：
                    1. 误区一：这里刷入命令时，可能会报错等待命令，这里可能是因为手机连的是你的实机或虚拟机，与你使用系统不同，又或者可以拔下手机，再次连接。
                     2. 误区二：你有时候会发现。你已经在fastboot模式下把twrp.img刷入了，第二次进入fastboot，正当你想进入到twrp时，发现显示no commend，这样的话，你还是进入到你使用的系统里面，再次把twrp.img刷入好了。
                     3. 误区三：注意刷入twrp.img时，手机必须处于fastboot状态，就是屏幕上显示一个Android机器人和Start图标。

  4. 步骤三：在twrp中刷入Magisk

  5. 1. 注意 
        1. 误区一：这里的Magisk不是说那一版都可以用的，我用了新版的一直报错说Invalid file，因此我这里推荐这一版的Magsik：https://github.com/topjohnwu/Magisk/releases/tag/v17.3 下载里面的那个Magisk-v17.3.zip，就那个3.99MB，41万左右byte的zip文件。
          2. 误区二：你下载上面的Magisk后，想用adb push到手机中(在push的过程中)却显示找不到指定文件。这是因为，咱们下载下来的文件叫Magisk-v17.3 .zip，注意看“3”于“.zip”之间有一个空格，你下载下来文件后，要把那个zip文件名字中间的空格去掉。

  6. 步骤四：在下载好的Magisk manager中打开超级用户权限。
     . 在设置好开发者选项，且连接电脑后，就可以，打开manager,点击左边的超级用户，这样超级用户权限就打开了。

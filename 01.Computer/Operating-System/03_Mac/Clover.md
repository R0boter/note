### 文件夹结构

1. ACPI
   - ORIGIN：存放提取到的原始DSDT文件
   - PATCHED：存放修改好的用户DSDT.aml和SSDT.aml
2. CLOVERX64.efi：64位CLOVER的主启动文件
3. Config.plist：CLOVER的配置文件
4. DOC：CLOVER的帮助文档
5. DRIVERS64UEFI：使用UEFI模式加载64位CLOVER所需的驱动文件
6. KEXTS：使用驱动注入时，CLOVER加载的驱动文件的存放位置
7. MISC：存放CLOVRER环境下的截图文件
8. OEM：分文件夹存放ACPI、config.plist等文件。用以加载，实现单个U盘引导多个黑苹果
9. ROM：存放提取到的显卡OROM文件
10. THEMES：存放CLOVER主题
11. TOOLS：EFI Shell存放的位置，放置用于进入shell环境的.efi文件，不能用来引导OSX，但可以执行一些.efi程序

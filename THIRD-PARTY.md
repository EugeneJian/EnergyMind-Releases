# 第三方组件、许可与对应源码

EnergyMind 5.2.16 使用 Qt、PySide6 Essentials 和 Shiboken6 6.12.0 动态库，适用 LGPL v3。Pi 独立进程内嵌 Bun 1.4.4，其中 JavaScriptCore/WebKit 和 TinyCC 的相应文件适用 LGPL。第三方组件的使用、修改、替换和分发依各自原许可证办理。 [本版本下载](https://github.com/EugeneJian/EnergyMind-Releases/releases/tag/v5.2.16)

## 从哪里取得材料

- 在 Finder 中右键点击应用，选择「显示包内容」，打开 `Contents/Resources/ThirdParty/`。其中有 GPL/LGPL 原文、Qt 及内嵌组件署名、Python/原生库许可、Rust 依赖表，以及 Pi、Bun、Mermaid 和 ELK 的许可资料。
- 同一发布页另提供 `EnergyMind-5.2.16-ThirdParty-Sources.zip` 和 `WebKit-JSC-d6375c72-source.tar.gz`，以及校验这两份下载的 `ThirdParty-SHA256SUMS.txt`。把这三个文件放在同一目录后执行 `shasum -a 256 -c ThirdParty-SHA256SUMS.txt`。无需登录或安装 EnergyMind 即可获取。
- 第一个归档内的 `SOURCE-ARCHIVES.sha256` 可校验各上游原始归档。Qt 源码包括 qtbase、qtsvg、qtimageformats、qttranslations 和 PySide/Shiboken 的 pyside-setup。也包含 Pi、Bun 和 TinyCC 的指定源码，以及随包 certifi 和 python-calamine 的同版源发行包。
- WebKit 归档取自 Bun 构建锁定的提交，包含 JavaScriptCore、WebCore、WTF、bmalloc、构建脚本及使用的配套源码。上游完整 Git 历史和测试集可从对应提交取得。 [WebKit 源码提交](https://github.com/oven-sh/WebKit/tree/d6375c72affe0f70222cdcb45012b10f0bf3a9d5)

## 在自己的 Mac 上替换 Qt

复制整个应用到自己可写的目录，保留可随时使用的官方版本。Qt 框架位于副本的 `Contents/Frameworks/PySide6/Qt/lib/`，绑定与运行库位于 `Contents/Frameworks/PySide6/` 和 `Contents/Frameworks/shiboken6/`。使用相同架构和兼容 ABI，保留文件名、符号链接以及原来的动态库加载路径（可用 `otool -L` 查看）。

以下示例假定终端当前目录包含你的测试副本 `EnergyMind.app`，已将自编译的 arm64 QtCore 替换进该框架。安装 Xcode 命令行工具后可运行：

```sh
framework="EnergyMind.app/Contents/Frameworks/PySide6/Qt/lib/QtCore.framework"
install_name_tool -id @rpath/QtCore "$framework/Versions/A/QtCore"
codesign --force --sign - "$framework"
codesign --force --sign - EnergyMind.app
codesign --verify --deep --strict EnergyMind.app
EnergyMind.app/Contents/MacOS/EnergyMind
```

如更换多个框架或插件，先给改动的每个嵌套组件签名，再签整个副本。在本机使用兼容的 QtCore 替换件和上述本地签名方式已验证可以进入应用大厅。自行签名的副本使用本地身份，原发行者的 Apple 公证票据和专属 iCloud 容器权限仅用于官方签名版本。

## 重建 Pi 及其运行时

Pi 与 EnergyMind 通过独立进程通信。包中 `Contents/Frameworks/connectors/pi` 为 Pi 1.6.0。归档提供 Pi 源码、依赖锁文件和构建脚本，Bun 1.4.4、它使用的 WebKit 分支及 TinyCC 均按对应版本提供。 [Pi 源码](https://github.com/earendil-works/pi/tree/faac585884ae2c013a6b1400f3e9e77f10b34bac) · [Bun 源码](https://github.com/oven-sh/bun/tree/38afee6c84fcf48c0edb2466aa4b27d287a59c30)

1. 按 Bun 源包内的构建文档安装编译依赖。把 WebKit 归档解压至 Bun 的 `vendor/WebKit`，使其包含 `Source/JavaScriptCore`。在该目录修改所需库。Bun 的 `scripts/build/deps/tinycc.ts` 指定了 TinyCC 源码和补丁。
2. 在 Bun 源码目录运行 `bun run build:local`，构建使用本地 WebKit 的 Bun。将新构建的 Bun 放在测试 shell 的 PATH 首位。
3. 在 Pi 源码根目录执行 `npm ci`、`npm run build` 和 `npm --workspace @earendil-works/pi-coding-agent run build:binary`。把生成的 `packages/coding-agent/dist/pi` 放到测试副本的原位置，保留同目录的运行时资源。可先执行 `pi --version` 核对。
4. 给更换的 Pi 可执行文件和测试应用依次本地签名，再启动测试副本。使用第三方库修改版本或为调试这些修改进行逆向工程时，按相应第三方许可行使权利。

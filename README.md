# OpenCore UEFI 安全啟動

OpenCore 旨在提供固件和操作系統之間的安全引導。在大多數 x86 平台上可信加載是通過 UEFI 安全啟動模型實現的。不僅 OpenCore 完全支持這個模型，而且擴展了其功能，以通過 Vault 確保密封配置，並為操作提供可信加載使用自定義驗證的系統，例如 Apple Secure Boot。 正確的安全啟動需要幾個步驟及仔細配置某些設置，如下所述：

1. 通過設置 `SecureBootModel` 來運行 macOS 以啟用 Apple 安全啟動。請注意，並非每個 macOS 版本都兼容使用 Apple 安全啟動，並有其他限制，請查閱 [Apple 安全啟動部分](opencore-setting/apple-secure-boot.md)。
2. 如用戶擔心加載易受攻擊的 DMG，可以將 `DmgLoading` 設置為 Disabled。注意，這不是必須的，但建議遵從。有關實際的權衡，請查閱 [DMG 加載部分](opencore-setting/dmg-loading.md)。
3. 確保 APFS JumpStart 功能已設置 `MinDate` 及 `MinVersion` 至 0 來限制加載易受攻擊的驅動。或通過手動安裝 `apfs.efi` 驅動程序達致相同功能。
4. 確保不需要強制加載驅動程序，並且所有的操作系統仍然可以啟動。
5. 確保 `ScanPolicy` 限制了從不需要的設備上加載。禁止所有可移動的驅動程序或未知的文件系統將有效保證安全性。
6. 使用私鑰簽署所有已安裝的驅動程序和工具。不要簽署提供管理權限的工具，例如 UEFI Shell。
7. 對設定檔進行 Vault。請查閱 [Vaulting 部分](opencore-setting/vaulting.md)。
8. 使用相同的私鑰簽署本系統上使用的所有OpenCore 二進制文件（`BOOTX64.efi`、`BOOTIa32.efi`、`OpenCore.efi`、自定義啟動程序）
9.  如果需要的話，簽署所有第三方操作系統（非微軟或蘋果公司製造）的引導程序。對於Linux，可以選擇安裝微軟簽名的 Shim 引導程序。請查閱 [Shim 引導部分]()。
10. 在固件首選項中啟用 UEFI 安全啟動，並安裝帶有私鑰的證書。如果需要 Windows，還需要添加Microsoft Windows Production CA 2011。要啟動選項 ROM 或使用簽名的 Linux 驅動程序，也需要 Microsoft UEFI Driver Signing CA。 關於如何生成證書的細節可以在各種文章中找到，比如這篇，不在本文的討論範圍之內
11. 對改變固件設置進行密碼保護，以確保 UEFI 安全啟動不能在用戶不知情的情況下被禁用。




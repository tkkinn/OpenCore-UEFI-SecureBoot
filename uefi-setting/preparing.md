# 事前準備

在開始執行 UEFI 安全啟動的工作之前，你應該對你的 EFI 檔案進行備份，此操作將可能導致您的 EFI 損毀。

## 辨別你的 UEFI 製造商

目前主要有三間製造商，分別為：

1. AMI \(American Megatrends\)
2. Insyde
3. Phoenix

以上製造商都聲稱支持 UEFI SecureBoot 技術，但設置它的界面因系統而異。幸運的是，這不是一個很大的問題，因為在 UEFI 2.3.1C（和更新的）兼容固件的 Setup 中沒有配置 SecureBoot 的接口，除了刪除當前 PK 的能力（即轉移 SecureBoot 到所謂的設置模式） 不是必需的，然後您可以使用任何可以使用用戶提供的數據調用 gRS -&gt; SetVariable UEFI 服務的 EFI 應用程序，包括 efitools ****包中的`KeyTool.efi`，這是專為管理密鑰而設計的，您只需要學習如何使用它。

## 檔案

你最少需要一個使用 Linux 內核所運行的操作系統，不論是安裝於系統，或是 Live USB，甚至是適用於 Linux 的 Windows 子系統 \(WSL\) 均可接受。

除了 Linux，我們還需要一些東西：  
1. **openssl**，用於生成密鑰對並將證書從 DER 轉換為 PEM。  
2. **efitools**，或者更確切地說是`cert-to-efi-sig-list`、`sign-efi-sig-list`用於將證書轉換為 ESL 格式並以此格式簽署文件，以及 `KeyTool.efi` 用於在 SetupMode 中管理系統密鑰。  
3. **sbsigntool**，或者更確切地說是用於使用您的密鑰簽署 UEFI 可執行文件（即加載程序、DXE 驅動程序、OptionROM 和 UEFI Shell 應用程序）的 sbsign 程序。

啟動 Linux，安裝上述軟件包，在您的主目錄中打開一個終端並繼續下一步。




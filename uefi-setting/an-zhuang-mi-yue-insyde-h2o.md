# 安裝密鑰 - Insyde H2O

準備一隻容量大於 200 MB 的 USB，並格式化為 FAT32。

1. 將 `KeyTool-signed.efi` 放入 USB `/EFI/BOOT` 並重新命名為 `BOOTX64.efi`
2. 將 `DB.auth` `KEK.auth` `PK.auth` 放入 USB 根目錄
3. 重新啟動並進入 UEFI

## Insyde H2O

1.設置 Supervisor Password

2.打開 SecureBoot

![](../.gitbook/assets/9c59591db861481f8df8b84c437632c1.jpg)

3. 選擇 "Erase all Secure Boot Setting"

4. 從 USB 啟動 KeyTool

![](../.gitbook/assets/3d3979c9efa341b0b2083231503e4200.png)

5. 選擇 "Edit Keys"

![](../.gitbook/assets/e8de0f240698400c83946a67a906aa0a.png)

6. 首先選擇 db，然後選擇 "Replace Keys"，然後選擇 USB 設備

![](../.gitbook/assets/e06e5f5768484b6ba922d6dcad09cda7.png)

7. 選擇 `DB.auth`

8. 對 KEK 及 PK 重複相同的操作

9. 添加密鑰並重新啟動後，嘗試重新啟動`KeyTool-signed.efi`確定 SecureBoot 正確運作


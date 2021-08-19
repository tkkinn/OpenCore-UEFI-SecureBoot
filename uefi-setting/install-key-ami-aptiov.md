# 安裝密鑰 - AMI AptioV

準備一隻容量大於 200 MB 的 USB，並格式化為 FAT32。

1. 將 `KeyTool-signed.efi` 放入 USB `/EFI/BOOT` 並重新命名為 `BOOTX64.efi`
2. 將 `DB.auth` `KEK.auth` `PK.auth` 放入 USB 根目錄
3. 重新啟動並進入 UEFI

## **AMI AptioV**

對於大多數基於 AMI 代碼的固件，SecureBoot 管理位於 “Security” 選項，如下所示：

![](../.gitbook/assets/a7f6482675fc4c5da37337beca5f47d0.png)

1.進入 "Key Management"

![](../.gitbook/assets/b5c0f74cb4d74ba294c8b980c3c726ff.png)

2. 選擇我們需要的變量

![](../.gitbook/assets/f070999c4b004270b0d5226b2a8aadfa.png)

3. 選擇 "Set New Key"

![](../.gitbook/assets/e29d7e68322c48ffbe0960bc6b89b1d6.png)

4. 選擇 "Authenticated Variable"

![](../.gitbook/assets/2e361195f6d64124bffa80921df71c20.png)

5. 你需要確認文件的更新，如果之前一切順利，結果將是一條簡明的信息

![](../.gitbook/assets/1cbb003f826d44928f83ee5365881da6.png)

6. 對 KEK 和 PK 重複相同的操作

![](../.gitbook/assets/273d345026784de290d92ec2b6684d33.png)

7. 用 Esc 鍵返回上一級菜單，啟用 SecureBoot

8. 添加密鑰並重新啟動後，嘗試重新啟動`KeyTool-signed.efi`確定 SecureBoot 正確運作


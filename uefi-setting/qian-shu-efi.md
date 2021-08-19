# 簽署 EFI

打開 Linux，使用 sbsigntool 簽署本系統上使用的所有 EFI

在 OpenCore 中，你需要簽署以下文件夾中的 EFI

1. `/OC/Driver`
2. `/OC/Tools`
3. `/BOOT`

```text
sbsign --key DC.key --cert DB.crt --output <EFI> <EFI>
```




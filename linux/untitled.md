# Shim

Shim 是一個簡單的軟件包，旨在用作 UEFI 系統上的第一階段引導加載程序。

它是由來自不同發行版的一組 Linux 開發人員開發的，他們共同努力使 SB 使用自由軟件工作。它是一段安全、易於理解和經過審核的通用代碼，因此可以使用平台密鑰對其進行信任和簽名。這意味著 Microsoft（或其他潛在的固件 CA 提供商）只需擔心簽署 shim，而不是發行版供應商可能想要支持的所有其他程序。

Shim 將成為所有其他發行版提供的 UEFI 程序的信任根。它嵌入了另一個發行版特定的 CA 密鑰，該密鑰本身用於對其他程序（例如 Linux、GRUB、fwupdate）進行簽名。這允許乾淨的信任委託 - 然後發行版負責簽署其餘的包。理想情況下，Shim 本身不需要經常更新，從而減少中央審計和 CA 團隊的工作量。

為了獲得額外的信任和安全，從版本 15 開始，shim 二進制構建是 100% 可重現的 - 您可以自己重建 Debian shim 二進制以驗證在這個關鍵的安全軟件中沒有嵌入任何意外的更改。

### MOK - 機器所有者密鑰

Shim 設計的一個關鍵部分是允許用戶控制他們自己的系統。 發行版 CA 密鑰內置於 Shim 二進制文件本身，但還有一個額外的密鑰數據庫可供用戶管理，即所謂的機器所有者密鑰（簡稱 MOK）。

用戶可以在 MOK 列表中添加和刪除密鑰，完全獨立於發行版 CA 密鑰。 `mokutil`實用程序可用於幫助管理 Linux 用戶空間中的密鑰，但對 MOK 密鑰的更改只能在啟動時直接從控制台確認。 這消除了用戶級惡意軟件可能註冊新密鑰並因此繞過整個 SB 點的風險。

網上有更多關於如何使用 MOK 的文檔，例如：

* [https://www.rodsbooks.com/efi-bootloaders/secureboot.html\#initial\_shim](https://www.rodsbooks.com/efi-bootloaders/secureboot.html#initial_shim)

#### 生成新密鑰

```bash
openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out MOK.der -days 36500 -subj "/CN=My Name/" -nodes
openssl x509 -inform der -in MOK.der -out MOK.pem
```

#### 註冊您的密鑰




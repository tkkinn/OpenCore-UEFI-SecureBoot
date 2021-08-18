# 為 SecureBoot 生成密鑰

### 安裝所需軟件包及下載所需文件

```bash
sudo apt-get install -y gnu-efi help2man sbsigntool uuid-runtime libfile-slurp-unicode-perl
git clone https://github.com/vathpela/efitools.git && cd efitools
```

### 加入 Microsoft 密鑰 \(可選\)

如果您不想失去啟動 Windows 和使用 Microsoft 密鑰簽名的可執行組件的能力，例如，用於外部顯卡的 GOP 驅動程序和用於外部網卡的 PXE 驅動程序，那麼您需要添加另一對密鑰 - [Microsoft Windows Production CA 2011](https://translate.google.com/website?sl=ru&tl=zh-TW&ajax=1&prev=search&elem=1&se=1&u=http://go.microsoft.com/fwlink/?LinkID%3D321192) 的密鑰 ，MS 用它簽署自己的引導加載程序和 [Microsoft UEFI 驅動程序簽名 CA](https://translate.google.com/website?sl=ru&tl=zh-TW&ajax=1&prev=search&elem=1&se=1&u=http://go.microsoft.com/fwlink/?LinkId%3D321194) 密鑰 ，它簽署第三方組件。另外，他們簽署的 Shim 引導加載程序，它現在可以啟動各種支持 SecureBoot 的 Linux 發行版。

```bash
wget https://www.dropbox.com/s/un9q4ryu9il0ynd/MicWinProPCA2011_2011-10-19.crt?dl=1 -O MicWinProPCA2011_2011-10-19.crt
wget https://www.dropbox.com/s/qwbi3gk7h9qc716/MicCorUEFCA2011_2011-06-27.crt?dl=1 -O MicCorUEFCA2011_2011-06-27.crt

openssl x509 -in MicWinProPCA2011_2011-10-19.crt -inform DER -out MsWin.pem -outform PEM
openssl x509 -in MicCorUEFCA2011_2011-06-27.crt -inform DER -out UEFI.pem -outform PEM
cert-to-efi-sig-list -g "$(uuidgen)" MsWin.pem MsWin.esl
cert-to-efi-sig-list -g "$(uuidgen)" UEFI.pem UEFI.esl
cat MsWin.esl UEFI.esl > platform.esl

make DB.esl
cat platform.esl DB.esl > newDB.esl
mv newDB.esl DB.esl
```

### 生成密鑰及 EFI

```bash
make
```




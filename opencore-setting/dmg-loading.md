# DMG 加載

一個相當簡單的設置，但對於 Apple 安全啟動很重要。 此設置允許您在 OpenCore 中設定 DMG 加載策略。 默認情況下，我們建議使用 `Signed`，但為了獲得最佳安全性，首選 `Disabled`。

Misc -&gt; Security -&gt; DmgLoading 的選項：

| 值 | 註釋 |
| :--- | :--- |
| Any | 允許在 OpenCore 中加載所有 DMG，但是如果啟用了 Apple 安全啟動，此選項將導致啟動失敗 |
| Signed | 僅允許加載 Apple 簽名的 DMG，如 macOS 安裝程序 |
| Disabled | 禁用所有外部 DMG 加載，但是使用此選項仍然允許使用內部恢復模式 |




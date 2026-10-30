# 小手機私人後台（Cloudflare 版）

把小手機的「跨裝置同步」架在你自己的 Cloudflare 帳號上。資料只存在你自己的帳號裡，用 Cloudflare 免費方案就夠。

跟官方 HF 同步伺服器是同一套 API，在 App 裡換個網址就能切換。

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/Mikaluotuo/aguaphone-CF-backend)

## 目前能做什麼

| 功能 | 狀態 |
|---|---|
| 跨裝置同步（推送、拉取、即時通知其他裝置） | ✅ 可以用 |
| 裝置之間互傳資料（「傳到這台」「從這台下載」） | ✅ 可以用 |
| 後台生成 | 🚧 還沒做好，暫時請把 App 裡的「HF 後台生成」保持關閉 |

## 怎麼架

1. 註冊一個 [Cloudflare](https://dash.cloudflare.com/sign-up) 帳號（免費，不用信用卡）。
2. 按上面的「Deploy to Cloudflare」按鈕，照畫面登入 Cloudflare 和 GitHub，按部署。
3. 部署完會拿到一個網址，長得像 `https://aguaphone-backend.你的名字.workers.dev`。
4. 打開小手機 → 設定 → 跨裝置同步 → 「伺服器 URL」貼上這個網址。
5. 在 App 裡**註冊**一個帳號。

### 註冊只開放第一個帳號

這是你的私人後台，第一個帳號註冊完就會自動關閉註冊，別人拿到網址也註冊不了。

想開給朋友一起用：Cloudflare 後台 → Workers & Pages → `aguaphone-backend` → Settings → Variables，把 `ALLOW_MORE_ACCOUNTS` 改成 `true`。每個帳號的資料是分開的。

### 在中國大陸

`workers.dev` 的網址在大陸通常連不上，要在 Cloudflare 幫這個 Worker 綁一個自己的網域（Settings → Domains & Routes → Add → Custom domain）。

## 免費額度夠嗎

Cloudflare 免費方案每天：10 萬次請求、10 萬筆寫入、約 28 小時的運作時間（WebSocket 閒置時不算），總儲存 5GB。一般一個人一天聊幾千則都用不完。超過的話當天的請求會失敗，UTC 0 點（台灣早上 8 點）重置。

## 設定

| 變數 | 預設 | 說明 |
|---|---|---|
| `ALLOW_MORE_ACCOUNTS` | `false` | 改成 `true` 允許註冊更多帳號 |
| `CLOUD_PUSH_NOTIFY_URL` | 小手機的推播服務 | 後台生成完成時發推播用；設成空字串就不發 |

部署時不用填任何密鑰，登入用的金鑰會在第一次啟動時自動產生，存在你自己的 Cloudflare 裡。

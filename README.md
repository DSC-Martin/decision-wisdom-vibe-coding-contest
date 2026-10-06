# 《決策智慧》10 週年 Vibe Coding 競賽｜活動說明頁

單頁靜態 HTML，介紹電通《決策智慧》10 週年內部競賽：邀請同事用 AI 輔助的 vibe coding，
把《決策智慧》刊物做成互動閱讀體驗。頁面內容包含辦賽理由、三種讀法示範（第一個範例即
[卡牌遊戲版](https://github.com/DSC-Martin/dentsu-intelligent-decision-gaming)）、
五週賽程、評分方式與獎項說明。

無建置流程、無相依套件——單一 `index.html`，直接用瀏覽器打開或丟上任何靜態頁面託管
（例如 GitHub Pages）即可。

## 報名表單：已接上 Google 表單

`#join` 區塊的報名表單介面是自己刻的（跟全頁同一套視覺），送出後直接 POST 進下面這個
Google 表單的提交端點，回應寫進隱藏的 iframe、頁面不會跳走（實作見 `index.html` 裡
`#joinForm` 那段 `<script>`）。資料會進這個表單連動的 Sheet，不用另外開資料庫。

對應的 Google 表單：[AI 競賽作品提交表單](https://docs.google.com/forms/d/e/1FAIpQLSd7Tuwtb0v_xNK-45TvChMlnJabu7j7kt_uNVuhW17JCbJ70g/viewform)

**欄位對照表**（之後要調整題目、或表單要搬到新的 Google 表單時對照用）：

| 頁面欄位 | Google 表單題目 | entry 代碼 |
|---|---|---|
| 聯絡人姓名 | 姓名 | `entry.1472149434` |
| Email | Email | `entry.2094976213` |
| 部門或單位 | 部門或單位 | `entry.875895866` |
| 品牌／隊伍名稱 | 品牌或隊伍名稱 | `entry.1120320214` |
| 作品名稱 | 作品名稱 | `entry.56693621` |
| 對應題目／文章 | 對應題目或文章 | `entry.882066575` |
| 作品描述 | 作品描述 | `entry.1870608224` |
| 使用的 AI 工具 | 使用的 AI 工具 | `entry.492762493` |
| 作品連結 | 作品連結 | `entry.769394164` |
| 同意條款（勾選框） | 同意條款 | `entry.387974922`（value 固定是選項全文：「我已詳閱並同意比賽規則與資料安全規範」） |

**如果以後要換成另一個 Google 表單**：開新表單、題目與型別對齊上表，從公開填寫頁
（`.../viewform`）直接檢視原始碼（Ctrl+U）搜尋 `entry.` 或 `FB_PUBLIC_LOAD_DATA_`，
照題目順序對出新代碼，連同 `<form>` 的 `action`（`viewform` 換成 `formResponse`）
一起換掉即可，不用再跑「打假資料取得預先填寫連結」那套。

**已知落差**：目前 Google 表單本身沒有把任何題目設為必填——必填是靠這個頁面的 HTML
`required` 擋，所以只要使用者是透過這個頁面填寫就沒問題；但如果有人直接打開 Google
表單原始連結填寫，會發現全部都能留空送出。如果在意這點，去 Google 表單裡把每一題
切成必填即可，不影響這裡接好的 entry 代碼。

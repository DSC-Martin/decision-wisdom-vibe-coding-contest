# 《決策智慧》10 週年 Vibe Coding 競賽｜活動說明頁

單頁靜態 HTML，介紹電通《決策智慧》10 週年內部競賽：邀請同事用 AI 輔助的 vibe coding，
把《決策智慧》刊物做成互動閱讀體驗。頁面內容包含辦賽理由、三種讀法示範（第一個範例即
[卡牌遊戲版](https://github.com/DSC-Martin/dentsu-intelligent-decision-gaming)）、
五週賽程、評分方式與獎項說明。

無建置流程、無相依套件——單一 `index.html`，直接用瀏覽器打開或丟上任何靜態頁面託管
（例如 GitHub Pages）即可。

## 上線前要做的事：接上報名表單

`index.html` 裡 `#join` 區塊的報名表單目前是空殼——介面是刻好的，但 `name="entry.XXXXXXXXX"`
都還是佔位值，`<form>` 的 `action` 也還指向一個不存在的表單 ID。資料不用自己開資料庫收，
直接送進 Google 表單連動的 Sheet：使用者填的介面是自己刻的（跟全頁同一套視覺），但送出
的目的地是 Google 表單的提交端點——submit 之後瀏覽器不會離開這一頁，回應寫進隱藏的
iframe（實作見 `index.html` 裡 `#joinForm` 那段 `<script>`）。

**設置步驟：**

1. 去 [forms.google.com](https://forms.google.com) 開一個新表單，依序加下面幾題（型別建議
   一致，方便等一下對照）：
   - 姓名（簡答）／Email（簡答）／部門或單位（簡答，非必填）
   - 品牌或隊伍名稱（簡答）／作品名稱（簡答）／對應題目或文章（簡答）
   - 作品描述（段落）／使用的 AI 工具（簡答）／作品連結（簡答）
   - 同意條款（核取方塊，一個選項：「我已詳閱並同意比賽規則與資料安全規範」）
2. 每一題都先打一個好認的字串進去（例如姓名那題打 `AAA_NAME`），再點右上角「⋮」→
   「取得預先填寫的連結」→「取得連結」，複製那串網址。
3. 網址裡會有一串 `entry.123456789=AAA_NAME&entry.987654321=AAA_EMAIL...`，照你剛剛打的
   字串，把 `index.html` 裡對應欄位的 `entry.XXXXXXXXX` 換成正確的數字。
4. 把同一串網址裡 `viewform` 改成 `formResponse`，整串貼到 `<form id="joinForm">` 的
   `action` 屬性。
5. 核取方塊那題如果 Google 表單顯示的是 `entry.XXXXXXXXX_sentinel` 之類的隱藏欄位，保留
   不要刪，勾選框本身另外還有一個 `entry.XXXXXXXXX`（有打勾才會送出那個值）。

卡住的話把 Google 表單的網址丟給負責串接的人，對一下每題的代碼就好。

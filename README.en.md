cqie Schedule · CQIE Course Schedule
Android Class Schedule Query App: Embedded Official Login Page → Capture OAuth Token → Directly Connect to Academic Affairs to Fetch **My** Class Schedule.

No self-built server, no third-party SDK, data flows only between your phone and the academic affairs server.
| | |
|---|---|
| Platform | Android 7.0+ (minSdk 26 / targetSdk 34) |
| Data Source | Chongqing Engineering College Academic Affairs `njw.cqie.edu.cn` (official OAuth2 + Bearer API) |
| Mode | Direct connection to academic affairs · Single machine, single account (others using = they log in with their own account) |
| Privacy | Read-only personal schedule; this device only stores token (approximately 7 days, self-maintained silent renewal), no password stored |
Function
**Official Login**: Open the unified authentication CAS page within the app to enter account/password/verification code, automatically complete OAuth to obtain the token; expire silently renew, prompt login page only if failed.
**Weekly Schedule / Today** Dual-view automatically定位当前教学周, 今天整列高亮(Weekly Schedule); 今日 page 显示 正在上 / 下一节 / 已结束 + 30s 自动刷新
Schedule automatically reads from the official academic 12 periods
Click any blank space to manually record the course/task (dashed card, saved locally)
**Offline Instant Access**: Class schedules for the current semester are cached locally, so you can view them even without an internet connection; with a network connection, the background automatically refreshes.
**One Screen for All on Mobile**: Narrow screen weekly schedule with adaptive column width, 7 days fully铺满无需左右滑动
**Account Center**(Top Bar 👤): View Current Account / Clear Local Cache / **Log Out**(Logout including official CAS session, return to the "Not Logged In" landing page, click "Go to Official Login Page" to switch accounts, preventing SSO from silently logging you back into your original account)
Table of Contents
android/    原生壳(Kotlin + WebView + OkHttp): 登录链、token 存储、JS 桥
prototype/  网页原型 = 唯一 UI 真源(H5 三件套, 复用于 APK 内嵌)
docs/       需求文档
Packaging APK
The packaging script will sync the H5 from `prototype/` into assets and then package it with Gradle.
android\build_apk.bat
Product: `android/app/build/outputs/apk/release/app-release.apk` (with R8 minify + resource shrinking enabled).
Debug the pure frontend by editing `prototype/index.html`; `prototype/server.py` is a backend proxy for local debugging and is not committed to the repository.
Compliance Boundaries
Only log in to your own account and read your own schedule; do not aggregate others' accounts or batch scrape. The repository does not contain any accounts/passwords/tokens.

🔧 作業ルーティン：ひもロボット実験 手順まとめ
2025-08-30夜の記録
1. PC（Windows）で準備
コマンドプロンプトを2つ開く（ロガー用・Web配信用）

(A) ロガー起動
cd C:\Users\Admin\Desktop\himo_robot_dual_send
node server.js

成功すると
[logger] ws server listening on ws://0.0.0.0:8080
と表示される

スマホからのデータをCSVに保存する

(B) Webサーバー起動
cd C:\Users\Admin\Desktop\himo_robot_dual_send
npx http-server -p 3000 .

成功するとAvailable on: http://192.168.2.101:3000と出る
スマホが index.html を取得する窓口になる

---

2. スマホ（Android）で操作

同じWi-Fiに接続（モバイルデータOFF）
ブラウザ（Chrome推奨）でアドレスバーに入力：
http://192.168.2.101:3000/index.html

ページが開いたら：
宛先A（PCロガー）：ws://192.168.2.101:8080
宛先B（ESP32）：まだ未使用、空欄でOK

FPS：10
「センサー許可」→「送信開始」をタップ
---
3. 確認
PC側の node server.js 実行窓に [logger] client connected ... が出る
logs/ フォルダに YYYY-MM-DD.csv ができ、センサー値が行として追記される
---
4. 次の拡張（ESP32連携）
宛先Bに
ws://<ESP32のIP>:81
を入力すると、ESP32でもデータを受信できる
まずはESP32のスケッチにWi-Fi設定を入れて書き込み、シリアルモニタでIPを確認する

---
👉 この手順を毎回繰り返せば、スマホの傾き → PCログ保存 → 将来的にESP32制御 まで一気に動かせます。
---
これを「作業ルーティン」ノートブックの最初のノートに貼っておくと、今後参照が楽になります。
Uta、このノートのタイトルは「ひもロボット実験 手順まとめ」でいいですか？

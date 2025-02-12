<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>顔認識＆画像・動画撮影機能付き（可愛いボタン版・レスポンシブ対応）</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background: #f0e6f7;
    }
    /* カメラ映像用のコンテナ。画面全体に広がり、中央に配置 */
    #camera-container {
      position: relative;
      width: 100%;
      height: 100vh;
      background: black;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    /* video と canvas はコンテナ内で自動サイズ（縦横比維持） */
    video, canvas {
      position: absolute;
      top: 0;
      left: 0;
      max-width: 100%;
      max-height: 100%;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }
    /* 撮影用コントロール（画面下部中央） */
    #controls {
      position: absolute;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 10;
    }
    button {
      font-size: 16px;
      padding: 10px 20px;
      margin: 5px;
      border: none;
      border-radius: 20px;
      cursor: pointer;
      background-color: #ef6076;
      color: white;
      box-shadow: 0 2px 4px rgba(0,0,0,0.3);
      transition: background-color 0.3s, transform 0.3s;
    }
    button:hover {
      transform: scale(1.05);
    }
    /* 録画中はボタン背景色変更 */
    .recording {
      background-color: #ff4444 !important;
    }
    /* video 要素は表示する */
  </style>
  <!-- tracking.js と顔検出用データ -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/tracking.js/1.1.3/tracking-min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/tracking.js/1.1.3/data/face-min.js"></script>
</head>
<body>
  <!-- カメラ映像用コンテナ -->
  <div id="camera-container">
    <!-- カメラ映像（表示する） -->
    <video id="video" autoplay playsinline></video>
    <!-- 合成表示用 canvas（映像＋オーバーレイ） -->
    <canvas id="canvas"></canvas>
  </div>
  <!-- 撮影用コントロール -->
  <div id="controls">
    <button id="captureImage">📸 画像撮影</button>
    <button id="toggleRecording">🎥 動画撮影開始</button>
  </div>
  
  <script>
    const video = document.getElementById('video');
    const canvas = document.getElementById('canvas');
    const context = canvas.getContext('2d');
    const captureImageBtn = document.getElementById('captureImage');
    const toggleRecordingBtn = document.getElementById('toggleRecording');

    // カメラ映像の取得（await を使わず Promise で取得）
    navigator.mediaDevices.getUserMedia({ video: true })
      .then(stream => {
        video.srcObject = stream;
        video.play();
        // ここで stream を使って必要ならカメラ設定を確認できます
        const track = stream.getVideoTracks()[0];
        const settings = track.getSettings();
        console.log("Camera resolution: " + settings.width + "x" + settings.height);
      })
      .catch(err => console.error("カメラアクセスエラー:", err));

    // video のメタデータ読み込み時に、実際の解像度で canvas のサイズを設定
    video.addEventListener('loadedmetadata', function() {
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
    });
    window.addEventListener('resize', function() {
      // ここでは video のサイズに依存するため、loadedmetadata で更新済みならそれでOK
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
    });

    // tracking.js による顔検出設定
    const tracker = new tracking.ObjectTracker('face');
    tracker.setInitialScale(4);
    tracker.setStepSize(2);
    tracker.setEdgesDensity(0.1);
    tracking.track('#video', tracker);

    // 顔検出結果保持
    let trackedFaces = [];
    const matchThreshold = 50;
    const updateThreshold = 1500; // 1500ms に設定

    // colon モード用ラベル
    const colonLabels = ["SEXした回数", "イッた回数", "抜いた回数", "オカズにされた数"];
    // heart モード用ラベル
    const heartLabels = ["毛の濃さ", "感度", "声の大きさ", "メスガキ", "ツンデレ", "ムッツリ"];

    tracker.on('track', function(event) {
      const now = Date.now();
      event.data.forEach(function(rect) {
        const centerX = rect.x + rect.width / 2;
        const centerY = rect.y + rect.height / 2;
        let matched = false;
        trackedFaces.forEach(function(face) {
          const faceCenterX = face.x + face.width / 2;
          const faceCenterY = face.y + face.height / 2;
          const distance = Math.hypot(centerX - faceCenterX, centerY - faceCenterY);
          if (distance < matchThreshold) {
            face.x = rect.x;
            face.y = rect.y;
            face.width = rect.width;
            face.height = rect.height;
            face.lastSeen = now;
            matched = true;
          }
        });
        if (!matched) {
          const mode = Math.random() < 0.5 ? "colon" : "heart";
          let labelData = {};
          if(mode === "colon") {
            const randomLabel = colonLabels[Math.floor(Math.random() * colonLabels.length)];
            const randomNum = Math.floor(Math.random() * 10000);
            labelData = { text: randomLabel, number: randomNum };
          } else {
            const randomLabel = heartLabels[Math.floor(Math.random() * heartLabels.length)];
            const heartCount = Math.floor(Math.random() * 5) + 1;
            labelData = { text: randomLabel, hearts: heartCount };
          }
          trackedFaces.push({
            x: rect.x,
            y: rect.y,
            width: rect.width,
            height: rect.height,
            mode: mode,
            label: labelData,
            lastSeen: now
          });
        }
      });
      trackedFaces = trackedFaces.filter(face => (now - face.lastSeen) < updateThreshold);
    });

    // composite 描画ループ（video とオーバーレイを合成）
    function drawComposite() {
      // 最新の canvas サイズに合わせて video を描画
      context.drawImage(video, 0, 0, canvas.width, canvas.height);
      context.textAlign = "center";
      context.font = 'bold 24px sans-serif';
      const textStrokeWidth = 3;
      trackedFaces.forEach(function(face) {
        // 顔枠描画
        context.strokeStyle = '#00FF00';
        context.lineWidth = 2;
        context.strokeRect(face.x, face.y, face.width, face.height);
        
        const textX = face.x + face.width / 2;
        if(face.mode === "colon") {
          context.lineWidth = textStrokeWidth;
          context.strokeStyle = 'white';
          context.strokeText(face.label.text, textX, face.y - 50);
          context.strokeText(face.label.number, textX, face.y - 20);
          context.fillStyle = 'red';
          context.fillText(face.label.text, textX, face.y - 50);
          context.fillText(face.label.number, textX, face.y - 20);
        } else {
          context.lineWidth = textStrokeWidth;
          context.strokeStyle = 'white';
          context.strokeText(face.label.text, textX, face.y - 50);
          const heartsStr = "🧡".repeat(face.label.hearts);
          context.strokeText(heartsStr, textX, face.y - 20);
          context.fillStyle = 'red';
          context.fillText(face.label.text, textX, face.y - 50);
          context.fillText(heartsStr, textX, face.y - 20);
        }
      });
      requestAnimationFrame(drawComposite);
    }
    drawComposite();

    // 画像撮影機能
    captureImageBtn.addEventListener('click', function() {
      const dataURL = canvas.toDataURL('image/png');
      const win = window.open();
      win.document.write('<img src="' + dataURL + '" style="max-width:100%;">');
    });

    // 動画撮影機能（MediaRecorder 使用）
    let recorder;
    let recordedChunks = [];
    let isRecording = false;
    toggleRecordingBtn.addEventListener('click', function() {
      if (!isRecording) {
        const stream = canvas.captureStream(30);
        recorder = new MediaRecorder(stream, { mimeType: 'video/webm; codecs=vp9' });
        recorder.ondataavailable = function(e) {
          if (e.data.size > 0) {
            recordedChunks.push(e.data);
          }
        };
        recorder.onstop = function() {
          const blob = new Blob(recordedChunks, { type: 'video/webm' });
          const url = URL.createObjectURL(blob);
          const a = document.createElement('a');
          a.href = url;
          a.download = 'recorded_video.webm';
          a.click();
          recordedChunks = [];
        };
        recorder.start();
        isRecording = true;
        toggleRecordingBtn.textContent = '⏹️ 動画撮影停止';
        toggleRecordingBtn.classList.add('recording');
      } else {
        recorder.stop();
        isRecording = false;
        toggleRecordingBtn.textContent = '🎥 動画撮影開始';
        toggleRecordingBtn.classList.remove('recording');
      }
    });
  </script>
</body>
</html>

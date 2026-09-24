<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>AR Hand Tracking Game</title>
  <style>
    body { margin: 0; font-family: sans-serif; background: #111; color: white; text-align: center; overflow: hidden; }
    #webcam { transform: scaleX(-1); position: absolute; top: 0; left: 0; width: 100vw; height: 100vh; object-fit: cover; }
    #canvas { position: absolute; top: 0; left: 0; width: 100vw; height: 100vh; pointer-events: none; }
    .ui-overlay { position: absolute; top: 10px; width: 100%; z-index: 10; font-size: 24px; font-weight: bold; text-shadow: 2px 2px 4px #000; }
  </style>
  <!-- โหลด MediaPipe Vision Libraries -->
  <script src="https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision/vision_bundle.js" crossorigin="anonymous"></script>
</head>
<body>

  <div class="ui-overlay">AR Game: ใช้มือจีบนิ้วเพื่อจับสิ่งของบนหน้าจอ</div>
  <video id="webcam" autoplay playsinline></video>
  <canvas id="canvas"></canvas>

  <script>
    const video = document.getElementById('webcam');
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');

    // ตั้งค่ากล้อง
    navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
      video.srcObject = stream;
    });

    // ปรับขนาด Canvas ให้เต็มจอ
    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    // ตัวอย่างเป้าหมายในเกม
    let item = { x: 300, y: 300, radius: 40, isGrabbed: false };

    // หมายเหตุ: โครงสร้างเกมนี้ใช้ MediaPipe Hands ในการดึงพิกัดนิ้วโป้ง (Landmark 4) 
    // และนิ้วชี้ (Landmark 8) เพื่อวัดระยะห่าง หากคำนวณระยะห่างได้ใกล้กัน = จีบนิ้ว (Pinch/Grab)
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GitHub YouTube Player</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0f172a;
      color: #e5e7eb;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }

    header {
      width: 100%;
      padding: 16px;
      box-sizing: border-box;
      text-align: center;
      background: #020617;
      border-bottom: 1px solid #1f2937;
    }

    h1 {
      margin: 0;
      font-size: 20px;
    }

    main {
      flex: 1;
      width: 100%;
      max-width: 900px;
      padding: 16px;
      box-sizing: border-box;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 16px;
    }

    .player-container {
      position: relative;
      width: 100%;
      max-width: 800px;
      padding-top: 56.25%; /* 16:9 */
      background: #000;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    }

    .player-container iframe {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      border: 0;
    }

    .info {
      font-size: 14px;
      color: #9ca3af;
      text-align: center;
      max-width: 700px;
    }

    .input-box {
      width: 100%;
      max-width: 700px;
      margin-top: 8px;
      text-align: center;
    }

    .input-box input {
      width: 100%;
      padding: 8px;
      border-radius: 4px;
      border: 1px solid #4b5563;
      background: #020617;
      color: #e5e7eb;
      box-sizing: border-box;
    }

    .input-box button {
      margin-top: 8px;
      padding: 8px 16px;
      border: none;
      border-radius: 4px;
      background: #2563eb;
      color: white;
      cursor: pointer;
    }

    .input-box button:hover {
      background: #1d4ed8;
    }
  </style>
</head>
<body>
  <header>
    <h1>YouTube in GitHub URL</h1>
  </header>

  <main>
    <div class="player-container">
      <!-- Default video: Call Aundi (OIv0FLrbnGE) -->
      <iframe
        id="ytPlayer"
        src="https://www.youtube.com/embed/OIv0FLrbnGE"
        title="YouTube video player"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
      </iframe>
    </div>

    <p class="info">
      This page is hosted on GitHub Pages. The video plays from YouTube using an embedded player.
    </p>

    <div class="input-box">
      <p class="info">
        To change the video, paste any YouTube link (or just the video ID) below and click <strong>Load Video</strong>.
      </p>
      <input id="ytInput" type="text" placeholder="Paste YouTube link or ID here">
      <button onclick="changeVideo()">Load Video</button>
    </div>
  </main>

  <script>
    function getVideoId(url) {
      if (!url) return null;
      url = url.trim();

      // If user pasted only the ID
      if (!url.startsWith('http') && url.length >= 8 && url.length <= 20) {
        return url;
      }

      try {
        // Short link: https://youtu.be/ID
        if (url.includes('youtu.be/')) {
          return url.split('youtu.be/')[1].split(/[?&]/)[0];
        }

        // Normal link: https://www.youtube.com/watch?v=ID&...
        if (url.includes('v=')) {
          return url.split('v=')[1].split('&')[0];
        }

        return null;
      } catch (e) {
        return null;
      }
    }

    function changeVideo() {
      const input = document.getElementById('ytInput').value;
      const id = getVideoId(input);
      if (!id) {
        alert('Please paste a valid YouTube link or video ID.');
        re

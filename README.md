<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My YouTube Viewer</title>
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
      /* 16:9 aspect ratio */
      padding-top: 56.25%;
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

    a {
      color: #60a5fa;
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <header>
    <h1>My YouTube Viewer (GitHub Pages)</h1>
  </header>

  <main>
    <div class="player-container">
      <!-- CHANGE ONLY THE VIDEO_ID PART BELOW -->
      <iframe
        src="https://www.youtube.com/embed/VIDEO_ID"
        title="YouTube video player"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
      </iframe>
    </div>

    <p class="info">
      This page is hosted on GitHub Pages.  
      The video is streamed directly from YouTube using an embedded player.
    </p>

    <p class="info">
      To change the video, replace <code>VIDEO_ID</code> in the iframe URL with the ID from your YouTube link.  
      Example: for <code>https://www.youtube.com/watch?v=JLMbpiywVxQ</code>, the ID is
      <code>JLMbpiywVxQ</code>.
    </p>
  </main>
</body>
</html>

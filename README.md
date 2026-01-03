<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My YouTube on GitHub</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Simple styling to make the video fill the screen -->
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background-color: #000;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .video-wrapper {
      width: 100%;
      max-width: 960px;
      aspect-ratio: 16 / 9; /* keeps video proportion */
    }
    .video-wrapper iframe {
      width: 100%;
      height: 100%;
      border: 0;
    }
  </style>
</head>
<body>
  <div class="video-wrapper">
    <iframe
      src="https://www.youtube.com/embed/YOUTUBE_VIDEO_ID_HERE"
      title="YouTube video player"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
      allowfullscreen>
    </iframe>
  </div>
</body>
</html>

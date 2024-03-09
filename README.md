# Jaydeep-s-Downloader
this is a downloader app 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>YouTube Downloader</title>
<style>
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
    background-color: #555;
  }
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
  }
  h2 {
    margin-bottom: 20px;
  }
  
  input[type="text"] {
    width: calc(100% - 40px);
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-bottom: 10px;
  }
  .download-button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    margin-top: 10px;
  }
  .video-thumbnail {
    max-width: 200px;
    height: auto;
    display: none;
  }
</style>
</head>
<body>

<div class="container">
  <h2 id="welcomeMessage">
    <span class="word">Welcome</span> 
    <span class="word">to</span>
    <span class="word">Jaydeep</span>
    <span class="word">Omprakash</span>
    <span class="word">Sharma's</span>
    <span class="word">YT</span>
    <span class="word">Downloader</span>
  </h2>
  
  <input type="text" id="videoUrl" placeholder="Paste YouTube video URL here">
  <select id="resolution">
    <option value="1080">1080p</option>
    <option value="720">720p</option>
    <option value="480">480p</option>
    <option value="360">360p</option>
    <option value="240">240p</option>
  </select>
  <button class="download-button" onclick="downloadVideo()">Download</button>
  <br>
  <img class="video-thumbnail" id="thumbnail" src="" alt="Video Thumbnail">
</div>

<script>
function downloadVideo() {
  var videoUrl = document.getElementById('videoUrl').value;
  var resolution = document.getElementById('resolution').value;
  var xhr = new XMLHttpRequest();
  xhr.open('POST', '/download', true);
  xhr.setRequestHeader('Content-Type', 'application/json');
  xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var response = JSON.parse(xhr.responseText);
      if (response.success) {
        alert('Video downloaded successfully!');
      } else {
        alert('Failed to download video. Please try again.');
      }
    }
  };
  xhr.send(JSON.stringify({ videoUrl: videoUrl, resolution: resolution }));
}

document.getElementById('videoUrl').addEventListener('input', function() {
  var url = this.value.trim();
  if (url !== '') {
    var videoId = getVideoId(url);
    var thumbnailUrl = 'https://img.youtube.com/vi/' + videoId + '/maxresdefault.jpg';
    document.getElementById('thumbnail').src = thumbnailUrl;
    document.getElementById('thumbnail').style.display = 'block';
  } else {
    document.getElementById('thumbnail').style.display = 'none';
  }
});

function getVideoId(url) {
  var videoId = '';
  var patterns = [
    /(?:https?:\/\/)?(?:www\.)?youtube\.com\/(?:watch\?v=)?([^&\n]+)/,
    /(?:https?:\/\/)?(?:www\.)?youtu\.be\/([^&\n]+)/
  ];
  for (var i = 0; i < patterns.length; i++) {
    var match = url.match(patterns[i]);
    if (match && match[1]) {
      videoId = match[1];
      break;
    }
  }
  document.addEventListener('DOMContentLoaded', function() {
  var words = document.querySelectorAll('.word');
  words.forEach(function(word, index) {
    setTimeout(function() {
      word.classList.add('word-animate');
      word.style.color = getRandomColor();
    }, index * 500);
  });
});

function downloadVideo() {
  var words = document.querySelectorAll('.word');
  words.forEach(function(word) {
    word.style.color = getRandomColor();
  });
}

function getRandomColor() {
  var letters = '0123456789ABCDEF';
  var color = '#';
  for (var i = 0; i < 6; i++) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
  return videoId;
}
}
</script>

</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MyEditor</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #101014;
  color: white;
  font-family: Arial, sans-serif;
}

header {
  padding: 20px;
  background: #1b1b23;
  border-bottom: 1px solid #333;
}

header h1 {
  margin: 0;
  color: #a78bfa;
}

header p {
  color: #aaa;
  margin-bottom: 0;
}

.container {
  padding: 20px;
  max-width: 600px;
  margin: auto;
}

.card {
  background: #1b1b23;
  border-radius: 16px;
  padding: 20px;
  margin-bottom: 20px;
  border: 1px solid #333;
}

.preview {
  background: #09090c;
  border-radius: 12px;
  min-height: 220px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  color: #aaa;
  text-align: center;
}

.preview video {
  width: 100%;
  max-height: 350px;
}

button, .upload {
  display: block;
  width: 100%;
  padding: 14px;
  margin-top: 15px;
  border: none;
  border-radius: 10px;
  background: #8b5cf6;
  color: white;
  font-size: 16px;
  text-align: center;
  cursor: pointer;
}

input {
  display: none;
}

h2 {
  margin-top: 0;
}

footer {
  text-align: center;
  padding: 20px;
  color: #888;
}
</style>
</head>

<body>

<header>
  <h1>MyEditor ✨</h1>
  <p>Your creative video studio</p>
</header>

<main class="container">

  <section class="card">
    <h2>Video Preview 🎬</h2>

    <div class="preview" id="preview">
      <p>Your video will appear here</p>
    </div>

    <label class="upload" for="videoInput">
      📁 Choose a Video
    </label>

    <input type="file" id="videoInput" accept="video/*">
  </section>

  <section class="card">
    <h2>AI Background Remover 🤖</h2>
    <p>Remove the background from your videos.</p>
    <button id="removeBg">Remove Background</button>
    <p id="status"></p>
  </section>

  <section class="card">
    <h2>Export Video 📥</h2>
    <p>Export your video when ready.</p>
    <button id="exportBtn">Export Video</button>
  </section>

</main>

<footer>
  Made with ❤️ using MyEditor
</footer>

<script>
const input = document.getElementById("videoInput");
const preview = document.getElementById("preview");
const status = document.getElementById("status");

let videoURL = null;

input.addEventListener("change", function () {
  const file = this.files[0];

  if (!file) return;

  if (videoURL) URL.revokeObjectURL(videoURL);

  videoURL = URL.createObjectURL(file);
  preview.innerHTML = "";

  const video = document.createElement("video");
  video.src = videoURL;
  video.controls = true;
  video.playsInline = true;

  preview.appendChild(video);
  status.textContent = "Video loaded successfully!";
});

document.getElementById("removeBg").onclick = function () {
  status.textContent =
    "AI background removal is not connected yet.";
};

document.getElementById("exportBtn").onclick = function () {
  if (!videoURL) {
    alert("Please choose a video first.");
    return;
  }

  const a = document.createElement("a");
  a.href = videoURL;
  a.download = input.files[0].name;
  a.click();
};
</script>

</body>
</html>

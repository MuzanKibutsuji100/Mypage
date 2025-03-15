<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Free Movies & Anime</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #111;
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        h1 {
            margin: 20px 0;
        }
        .movie-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
            padding: 20px;
        }
        .movie {
            background-color: #222;
            padding: 15px;
            border-radius: 10px;
            width: 200px;
            cursor: pointer;
            transition: 0.3s;
        }
        .movie:hover {
            background-color: #333;
        }
        img {
            width: 100%;
            border-radius: 10px;
        }
        #videoPlayer {
            width: 80%;
            height: 400px;
            margin-top: 20px;
            display: none;
            border-radius: 10px;
        }
    </style>
</head>
<body>

    <h1>Watch Free Movies & Anime</h1>
    <p>Click on a movie or anime to start watching!</p>

    <div class="movie-container">
        <div class="movie" onclick="playMovie('https://www.sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4')">
            <img src="https://via.placeholder.com/200x300?text=Movie+1" alt="Movie 1">
            <p>Movie 1</p>
        </div>
        <div class="movie" onclick="playMovie('https://www.sample-videos.com/video123/mp4/720/sample-mp4-video.mp4')">
            <img src="https://via.placeholder.com/200x300?text=Anime+1" alt="Anime 1">
            <p>Anime 1</p>
        </div>
        <div class="movie" onclick="playMovie('https://www.sample-videos.com/video123/mp4/720/sample-mp4-file.mp4')">
            <img src="https://via.placeholder.com/200x300?text=TV+Show+1" alt="TV Show 1">
            <p>TV Show 1</p>
        </div>
    </div>

    <video id="videoPlayer" controls></video>

    <script>
        function playMovie(videoUrl) {
            let player = document.getElementById("videoPlayer");
            player.src = videoUrl;
            player.style.display = "block";
            player.play();
        }
    </script>

</body>
</html>

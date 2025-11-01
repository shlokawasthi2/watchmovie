<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MovieWatch - Watch Movies Online</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 0; background-color: #f4f4f4; }
        header { background-color: #333; color: white; padding: 1rem; text-align: center; }
        .search { margin: 1rem; text-align: center; }
        .search input { padding: 0.5rem; width: 300px; }
        .admin-btn { margin: 1rem; text-align: center; }
        .upload-form { display: none; margin: 1rem; padding: 1rem; background: white; border: 1px solid #ccc; }
        .upload-form input, .upload-form select, .upload-form button { display: block; margin: 0.5rem 0; padding: 0.5rem; width: 100%; }
        .movies { display: flex; flex-wrap: wrap; justify-content: center; padding: 1rem; }
        .movie { background: white; margin: 1rem; padding: 1rem; width: 250px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
        .movie img { width: 100%; height: 300px; object-fit: cover; }
        .movie h3 { margin: 0.5rem 0; }
        .movie p { font-size: 0.9rem; }
        .video { margin-top: 1rem; }
        iframe { width: 100%; height: 200px; }
    </style>
</head>
<body>
    <header>
        <h1>MovieWatch</h1>
        <p>Your go-to site for watching movies!</p>
    </header>
    
    <div class="search">
        <input type="text" placeholder="Search for movies..." id="search">
        <button onclick="searchMovies()">Search</button>
    </div>
    
    <div class="admin-btn">
        <button onclick="showUploadForm()">Admin Upload</button>
    </div>
    
    <div class="upload-form" id="uploadForm">
        <h3>Upload a New Movie (Admin Only)</h3>
        <input type="text" id="movieTitle" placeholder="Movie Title" required>
        <select id="movieGenre">
            <option value="Action">Action</option>
            <option value="Comedy">Comedy</option>
            <option value="Drama">Drama</option>
            <option value="Horror">Horror</option>
            <!-- Add more genres -->
        </select>
        <input type="number" id="movieYear" placeholder="Year" required>
        <input type="file" id="moviePoster" accept="image/*" required>
        <input type="file" id="movieVideo" accept="video/*" required>
        <button onclick="uploadMovie()">Upload Movie</button>
        <button onclick="hideUploadForm()">Cancel</button>
    </div>
    
    <div class="movies" id="movieList">
        <!-- Sample movies; new uploads will be added here -->
        <div class="movie">
            <img src="https://via.placeholder.com/250x300?text=Movie+Poster" alt="Movie Poster">
            <h3>Movie Title 1</h3>
            <p>Genre: Action | Year: 2023</p>
            <div class="video">
                <iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ" frameborder="0" allowfullscreen></iframe>
            </div>
        </div>
        <!-- Add more movies here -->
    </div>
    
    <script>
        function searchMovies() {
            const query = document.getElementById('search').value.toLowerCase();
            const movies = document.querySelectorAll('.movie');
            movies.forEach(movie => {
                const title = movie.querySelector('h3').textContent.toLowerCase();
                movie.style.display = title.includes(query) ? 'block' : 'none';
            });
        }
        
        function showUploadForm() {
            const password = prompt("Enter admin password:");
            if (password === "7484") {
                document.getElementById('uploadForm').style.display = 'block';
            } else {
                alert("Incorrect password. Access denied.");
            }
        }
        
        function hideUploadForm() {
            document.getElementById('uploadForm').style.display = 'none';
        }
        
        function uploadMovie() {
            const title = document.getElementById('movieTitle').value;
            const genre = document.getElementById('movieGenre').value;
            const year = document.getElementById('movieYear').value;
            const poster = document.getElementById('moviePoster').files[0];
            const video = document.getElementById('movieVideo').files[0];
            
            if (!title || !year || !poster || !video) {
                alert("Please fill all fields and select files.");
                return;
            }
            
            // In a real app, send this data to a server for processing/storage.
            // For demo, we'll simulate adding to the page (files won't actually upload).
            const posterURL = URL.createObjectURL(poster);  // Temporary local URL
            const videoURL = URL.createObjectURL(video);    // Temporary local URL
            
            const movieList = document.getElementById('movieList');
            const newMovie = document.createElement('div');
            newMovie.className = 'movie';
            newMovie.innerHTML = `
                <img src="${posterURL}" alt="Movie Poster">
                <h3>${title}</h3>
                <p>Genre: ${genre} | Year: ${year}</p>
                <div class="video">
                    <video controls width="100%" height="200">
                        <source src="${videoURL}" type="video/mp4">
                        Your browser does not support the video tag.
                    </video>
                </div>
            `;
            movieList.appendChild(newMovie);
            
            // Reset form
            document.getElementById('movieTitle').value = '';
            document.getElementById('movieYear').value = '';
            document.getElementById('moviePoster').value = '';
            document.getElementById('movieVideo').value = '';
            hideUploadForm();
            alert("Movie uploaded successfully! (Demo only - not saved permanently)");
        }
    </script>
</body>
</html>

# Movieflix
website for watching movies 
git init
git remote add origin https://github.com/YOUR_USERNAME/movieflix.git
git add .
git commit -m "Initial upload"
git branch -M main
git push -u origin main
<!-- index.html (Merged: Home + Movie List + Watch Page) -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MovieFlix | Home</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-900 text-white">
  <header class="bg-[#1e1e1e] flex items-center justify-between px-6 py-4 shadow">
    <div class="text-2xl font-bold text-pink-500">📺 MovieFlix</div>
    <nav class="space-x-6">
      <button onclick="switchToMovies()" class="hover:text-pink-400">Movies</button>
    </nav>
  </header>

  <!-- MOVIE LIST PAGE -->
  <main id="movieSection" class="p-6">
    <div class="flex justify-between items-center mb-4">
      <h1 class="text-3xl font-bold text-pink-500">Now Streaming</h1>
      <button id="toggleTheme" class="bg-gray-700 hover:bg-gray-600 text-white px-4 py-2 rounded">Toggle Theme</button>
    </div>

    <input type="text" id="searchInput" placeholder="Search movies..." class="mb-6 w-full p-2 rounded bg-gray-700 text-white">

    <div id="movieGrid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <!-- Movie cards dynamically inserted here -->
    </div>
  </main>

  <!-- WATCH PAGE -->
  <main id="watchSection" class="hidden flex-grow flex-col items-center justify-center px-4 py-8">
    <div class="w-full max-w-5xl aspect-video">
      <iframe
        id="videoFrame"
        class="w-full h-full rounded-lg shadow-lg"
        src=""
        frameborder="0"
        allowfullscreen
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      ></iframe>
    </div>
    <h2 id="movieTitle" class="mt-6 text-3xl font-semibold text-center text-white"></h2>
    <button onclick="switchToMovies()" class="mt-6 px-4 py-2 bg-pink-500 hover:bg-pink-600 rounded">Back to Movies</button>
  </main>

  <footer class="bg-[#1e1e1e] text-center py-4 text-sm text-gray-400">© 2025 MovieFlix. All rights reserved.</footer>

  <script>
    const defaultMovies = [
      { title: "The Dark Knight", id: "EXeTwQWrcwY" },
      { title: "Inception", id: "YoHD9XEInc0" },
      { title: "Interstellar", id: "zSWdZVtXT7E" },
      { title: "Avengers: Endgame", id: "TcMBFSGVi1c" },
      { title: "Pathaan", id: "vqu4z34wENw" },
      { title: "KGF Chapter 2", id: "JKa05nyUmuQ" },
      { title: "Pushpa: The Rise", id: "Q1NKMPhP8PY" },
      { title: "Spider-Man: No Way Home", id: "JfVOs4VSpmA" },
      { title: "Drishyam 2", id: "lX_2t5fN81g" },
      { title: "Avatar: The Way of Water", id: "d9MyW72ELq0" },

      // Additional movies
      { title: "Jawan", id: "COv52Qyctws" },
      { title: "Gully Boy", id: "JfbXC1_Jv3s" },
      { title: "Brahmastra", id: "gkTzEkQY-fs" },
      { title: "Andhadhun", id: "2iVYI99VGaw" },
      { title: "Shershaah", id: "E6ekB2jUFEY" },
      { title: "Joker", id: "zAGVQLHvwOY" },
      { title: "Black Panther", id: "xjDjIWPwcPU" },
      { title: "No Time to Die", id: "BIhNsAtPbPI" },
      { title: "Tenet", id: "L3pk_TBkihU" },
      { title: "The Batman", id: "mqqft2x_Aa4" }
    ];

    const userUploaded = JSON.parse(localStorage.getItem("movies") || "[]");
    const allMovies = [...defaultMovies, ...userUploaded];

    const grid = document.getElementById("movieGrid");
    const searchInput = document.getElementById("searchInput");

    function renderMovies(filter = "") {
      grid.innerHTML = "";
      allMovies
        .filter(m => m.title.toLowerCase().includes(filter.toLowerCase()))
        .forEach(movie => {
          const card = document.createElement("div");
          card.className = "bg-[#1e1e1e] rounded shadow hover:shadow-lg transition-all";
          card.innerHTML = `
            <div onclick="watchMovie('${movie.id}', '${movie.title}')" class="cursor-pointer">
              <img src="https://img.youtube.com/vi/${movie.id}/0.jpg" alt="${movie.title}" class="w-full rounded-t">
              <div class="p-4">
                <h2 class="text-lg font-semibold">${movie.title}</h2>
              </div>
            </div>
          `;
          grid.appendChild(card);
        });
    }

    function watchMovie(id, title) {
      document.getElementById("movieSection").classList.add("hidden");
      document.getElementById("watchSection").classList.remove("hidden");
      document.getElementById("videoFrame").src = `https://www.youtube.com/embed/${id}?autoplay=1`;
      document.getElementById("movieTitle").textContent = title;
    }

    function switchToMovies() {
      document.getElementById("watchSection").classList.add("hidden");
      document.getElementById("movieSection").classList.remove("hidden");
      document.getElementById("videoFrame").src = "";
    }

    document.getElementById("toggleTheme").addEventListener("click", () => {
      document.body.classList.toggle("bg-white");
      document.body.classList.toggle("text-black");
      document.body.classList.toggle("text-white");
    });

    searchInput.addEventListener("input", (e) => {
      renderMovies(e.target.value);
    });

    renderMovies();
  </script>
</body>
</html>

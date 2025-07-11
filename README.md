# Movieflix
website for watching movies
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MovieFlix | Movies</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-900 text-white">
  <!-- Header -->
  <header class="bg-gray-800 flex items-center justify-between px-6 py-4">
    <div class="text-2xl font-bold">🎬 MovieFlix</div>
    <nav class="space-x-6">
      <a href="index.html" class="hover:text-red-400">Home</a>
      <a href="movies.html" class="hover:text-red-400">Movies</a>
      <a href="#" onclick="showLogin()" class="hover:text-red-400">Login</a>
      <a href="#" onclick="showSignup()" class="hover:text-red-400">Signup</a>
    </nav>
  </header>

  <!-- Movie Grid -->
  <section class="py-16 px-6">
    <h2 class="text-3xl font-semibold mb-8 text-center">Full-Length Movies</h2>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6" id="movie-grid"></div>
  </section>

  <!-- Login Modal -->
  <div id="loginModal" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center hidden z-50">
    <div class="bg-gray-800 p-8 rounded-lg w-full max-w-md">
      <h2 class="text-xl font-bold mb-4">Login</h2>
      <input id="loginEmail" type="email" placeholder="Email" class="w-full mb-4 px-3 py-2 bg-gray-700 rounded">
      <input id="loginPassword" type="password" placeholder="Password" class="w-full mb-4 px-3 py-2 bg-gray-700 rounded">
      <button onclick="loginUser()" class="w-full bg-red-500 hover:bg-red-600 py-2 rounded">Login</button>
      <p class="mt-4 text-sm text-center">Don't have an account? <a href="#" onclick="switchToSignup()" class="text-red-400">Sign up</a></p>
    </div>
  </div>

  <!-- Signup Modal -->
  <div id="signupModal" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center hidden z-50">
    <div class="bg-gray-800 p-8 rounded-lg w-full max-w-md">
      <h2 class="text-xl font-bold mb-4">Sign Up</h2>
      <input id="signupEmail" type="email" placeholder="Email" class="w-full mb-4 px-3 py-2 bg-gray-700 rounded">
      <input id="signupPassword" type="password" placeholder="Password" class="w-full mb-4 px-3 py-2 bg-gray-700 rounded">
      <button onclick="signupUser()" class="w-full bg-red-500 hover:bg-red-600 py-2 rounded">Sign Up</button>
      <p class="mt-4 text-sm text-center">Already have an account? <a href="#" onclick="switchToLogin()" class="text-red-400">Login</a></p>
    </div>
  </div>

  <!-- Footer -->
  <footer class="bg-gray-800 text-center py-4 text-sm text-gray-400">© 2025 MovieFlix. All rights reserved.</footer>

  <!-- JavaScript -->
  <script>
    const movies = [
      { title: "The Dark Knight", id: "EXeTwQWrcwY" },
      { title: "Inception", id: "YoHD9XEInc0" },
      { title: "Zindagi Na Milegi Dobara", id: "tgbNymZ7vqY" },
      { title: "The Matrix", id: "m8e-FF8MsqU" },
      { title: "Doctor Strange", id: "aWzlQ2N6qqg" },
      { title: "Pushpa", id: "Q1NKMPhP8PY" },
      { title: "3 Idiots", id: "K0eDlFX9GMc" },
      { title: "Interstellar", id: "zSWdZVtXT7E" },
      { title: "Drishyam 2", id: "fDbhpk1zBeQ" },
      { title: "Avatar", id: "5PSNL1qE6VY" },
      { title: "Bahubali 2", id: "G62HrubdD6o" },
      { title: "Parasite", id: "SEUXfv87Wpk" },
      { title: "PK", id: "SOXWc32k4zA" },
      { title: "DDLJ", id: "c25GKl5VNeY" },
      { title: "Iron Man", id: "8ugaeA-nMTc" },
      { title: "Transformers", id: "v8ItGrI-Ou0" },
      { title: "Dangal", id: "x_7YlGv9u1g" },
      { title: "Mission Mangal", id: "r9UuNqK9VJw" },
      { title: "Shershaah", id: "Q0FTXnefVBA" },
      { title: "Gully Boy", id: "JfbxcD6biOk" },
      { title: "Uri: The Surgical Strike", id: "HJDW6G6p3Z4" },
      { title: "Titanic", id: "2e-eXJ6HgkQ" },
      { title: "John Wick", id: "2AUmvWm5ZDQ" },
      { title: "Joker", id: "zAGVQLHvwOY" },
      { title: "Fast & Furious 7", id: "Skpu5HaVkOc" },
      { title: "The Avengers", id: "eOrNdBpGMv8" },
      { title: "Baby (Hindi)", id: "OB8xQH_cPVw" },
      { title: "KGF Chapter 2", id: "0pGQUoK3tk8" },
      { title: "Baahubali: The Beginning", id: "sOEg_YZQsTI" },
      { title: "Captain America: Civil War", id: "dKrVegVI0Us" },
      { title: "The Pursuit of Happyness", id: "89Kq8SDyvfg" },
      { title: "Chak De! India", id: "6a0-dSMWm5g" },
      { title: "Avengers: Infinity War", id: "6ZfuNTqbHE8" },
      { title: "Bajrangi Bhaijaan", id: "4nwAra0mz_Q" },
      { title: "The Revenant", id: "LoebZZ8K5N0" },
      { title: "Black Panther", id: "xjDjIWPwcPU" }
    ];

    const grid = document.getElementById('movie-grid');
    movies.forEach(movie => {
      const card = document.createElement('div');
      card.className = "bg-gray-800 rounded-lg overflow-hidden";
      card.innerHTML = `
        <img src="https://img.youtube.com/vi/${movie.id}/0.jpg" alt="${movie.title}" class="w-full">
        <div class="p-4">
          <h3 class="text-lg font-semibold">${movie.title}</h3>
          <a href="https://www.youtube.com/embed/${movie.id}" target="_blank" class="text-red-400 hover:underline">Watch Now</a>
        </div>
      `;
      grid.appendChild(card);
    });

    // Auth functions
    function showLogin() {
      document.getElementById('loginModal').classList.remove('hidden');
    }
    function showSignup() {
      document.getElementById('signupModal').classList.remove('hidden');
    }
    function switchToSignup() {
      document.getElementById('loginModal').classList.add('hidden');
      showSignup();
    }
    function switchToLogin() {
      document.getElementById('signupModal').classList.add('hidden');
      showLogin();
    }
    function signupUser() {
      const email = document.getElementById('signupEmail').value;
      const password = document.getElementById('signupPassword').value;
      if (email && password) {
        localStorage.setItem(email, password);
        alert('Signup successful! Now login.');
        document.getElementById('signupModal').classList.add('hidden');
        showLogin();
      } else {
        alert('Please fill all fields');
      }
    }
    function loginUser() {
      const email = document.getElementById('loginEmail').value;
      const password = document.getElementById('loginPassword').value;
      const storedPassword = localStorage.getItem(email);
      if (storedPassword === password) {
        alert('Login successful!');
        document.getElementById('loginModal').classList.add('hidden');
      } else {
        alert('Invalid credentials!');
      }
    }
  </script>
</body>
</html>

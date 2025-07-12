#Movieflix
website for watching movies
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MovieFlix | Home</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-900 text-white">
  <header class="bg-gray-800 flex items-center justify-between px-6 py-4">
    <div class="text-2xl font-bold">🎬 MovieFlix</div>
    <nav class="space-x-6">
      <a href="index.html" class="hover:text-red-400">Home</a>
      <a href="login.html" class="hover:text-red-400">Login</a>
      <a href="signup.html" class="hover:text-red-400">Sign Up</a>
    </nav>
  </header>

  <!-- Search Bar -->
  <section class="px-6 py-4">
    <input
      type="text"
      id="searchInput"
      placeholder="Search movies..."
      class="w-full p-3 rounded bg-gray-700 text-white focus:outline-none"
    />
  </section>

  <!-- Movie Grid -->
  <section class="py-6 px-6">
    <h2 class="text-3xl font-semibold mb-6 text-center">Now Streaming</h2>
    <div id="movieContainer" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      
      <!-- Add movie cards below -->
      <!-- Example Movie Card (You can repeat for all 50 movies) -->
      <div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="the dark knight">
        <img src="https://img.youtube.com/vi/EXeTwQWrcwY/0.jpg" alt="The Dark Knight" class="w-full">
        <div class="p-4">
          <h3 class="text-lg font-semibold">The Dark Knight</h3>
          <a href="watch.html?id=EXeTwQWrcwY" class="text-red-400 hover:underline">Watch Now</a>
        </div>
      </div>

      <!-- Copy-paste your other 49 movie cards here, use format above -->

    </div>
  </section>

  <footer class="bg-gray-800 text-center py-4 text-sm text-gray-400">
    © 2025 MovieFlix. All rights reserved.
  </footer>

  <script>
    // 🔍 Search functionality
    document.getElementById("searchInput").addEventListener("input", function () {
      const searchTerm = this.value.toLowerCase();
      const cards = document.querySelectorAll(".movie-card");

      cards.forEach((card) => {
        const title = card.getAttribute("data-title").toLowerCase();
        if (title.includes(searchTerm)) {
          card.style.display = "block";
        } else {
          card.style.display = "none";
        }
      });
    });
  </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login - MovieFlix</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-900 text-white flex items-center justify-center h-screen">
  <div class="bg-gray-800 p-8 rounded shadow-md w-full max-w-sm">
    <h2 class="text-2xl font-bold mb-6 text-center">Login to MovieFlix</h2>
    <form onsubmit="return loginUser(event)">
      <input type="email" id="email" placeholder="Email" required class="mb-4 w-full p-2 rounded bg-gray-700 text-white" />
      <input type="password" id="password" placeholder="Password" required class="mb-4 w-full p-2 rounded bg-gray-700 text-white" />
      <button type="submit" class="bg-red-500 hover:bg-red-600 text-white w-full p-2 rounded">Login</button>
    </form>
    <p class="mt-4 text-center text-sm">Don't have an account? <a href="signup.html" class="text-red-400 hover:underline">Sign Up</a></p>
  </div>

  <script>
    function loginUser(e) {
      e.preventDefault();
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;

      const stored = JSON.parse(localStorage.getItem("movieflixUsers")) || [];
      const match = stored.find(user => user.email === email && user.password === password);
      if (match) {
        alert("Login successful!");
        window.location.href = "index.html";
      } else {
        alert("Invalid credentials.");
      }
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sign Up - MovieFlix</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-900 text-white flex items-center justify-center h-screen">
  <div class="bg-gray-800 p-8 rounded shadow-md w-full max-w-sm">
    <h2 class="text-2xl font-bold mb-6 text-center">Create an Account</h2>
    <form onsubmit="return signupUser(event)">
      <input type="text" id="name" placeholder="Full Name" required class="mb-4 w-full p-2 rounded bg-gray-700 text-white" />
      <input type="email" id="email" placeholder="Email" required class="mb-4 w-full p-2 rounded bg-gray-700 text-white" />
      <input type="password" id="password" placeholder="Password" required class="mb-4 w-full p-2 rounded bg-gray-700 text-white" />
      <button type="submit" class="bg-red-500 hover:bg-red-600 text-white w-full p-2 rounded">Sign Up</button>
    </form>
    <p class="mt-4 text-center text-sm">Already have an account? <a href="login.html" class="text-red-400 hover:underline">Login</a></p>
  </div>

  <script>
    function signupUser(e) {
      e.preventDefault();
      const name = document.getElementById("name").value;
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;

      const users = JSON.parse(localStorage.getItem("movieflixUsers")) || [];

      if (users.some(user => user.email === email)) {
        alert("Email already registered.");
        return;
      }

      users.push({ name, email, password });
      localStorage.setItem("movieflixUsers", JSON.stringify(users));
      alert("Signup successful! Please login.");
      window.location.href = "login.html";
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Watch Movie | MovieFlix</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-black text-white">
  <header class="bg-gray-800 flex items-center justify-between px-6 py-4">
    <div class="text-2xl font-bold">🎬 MovieFlix</div>
    <nav class="space-x-6">
      <a href="index.html" class="hover:text-red-400">Home</a>
      <a href="login.html" class="hover:text-red-400">Login</a>
    </nav>
  </header>

  <section class="flex flex-col items-center justify-center py-12 px-4">
    <div class="w-full max-w-5xl">
      <div class="aspect-w-16 aspect-h-9">
        <iframe id="movieFrame" class="w-full h-[80vh]" src="" frameborder="0" allowfullscreen></iframe>
      </div>
    </div>
  </section>

  <script>
    const params = new URLSearchParams(window.location.search);
    const videoId = params.get("id");
    if (videoId) {
      document.getElementById("movieFrame").src = `https://www.youtube.com/embed/${videoId}`;
    } else {
      document.getElementById("movieFrame").outerHTML = "<p class='text-center text-red-500'>Invalid movie link</p>";
    }
  </script>
</body>
</html>
<!-- Movie: Dangal -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="dangal">
  <img src="https://img.youtube.com/vi/x_7YlGv9u1g/0.jpg" alt="Dangal" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Dangal</h3>
    <a href="watch.html?id=x_7YlGv9u1g" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: The Shawshank Redemption -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="shawshank redemption">
  <img src="https://img.youtube.com/vi/NmzuHjWmXOc/0.jpg" alt="The Shawshank Redemption" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">The Shawshank Redemption</h3>
    <a href="watch.html?id=NmzuHjWmXOc" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: Hera Pheri -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="hera pheri">
  <img src="https://img.youtube.com/vi/WC8U5_7dA7s/0.jpg" alt="Hera Pheri" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Hera Pheri</h3>
    <a href="watch.html?id=WC8U5_7dA7s" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: Avengers (Hindi Dubbed) -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="avengers hindi">
  <img src="https://img.youtube.com/vi/eOrNdBpGMv8/0.jpg" alt="Avengers (Hindi)" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Avengers (Hindi)</h3>
    <a href="watch.html?id=eOrNdBpGMv8" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: Bajrangi Bhaijaan -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="bajrangi bhaijaan">
  <img src="https://img.youtube.com/vi/4nvL1V-H9bE/0.jpg" alt="Bajrangi Bhaijaan" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Bajrangi Bhaijaan</h3>
    <a href="watch.html?id=4nvL1V-H9bE" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: Drishyam -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="drishyam">
  <img src="https://img.youtube.com/vi/8eJf6vAX4z8/0.jpg" alt="Drishyam" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Drishyam</h3>
    <a href="watch.html?id=8eJf6vAX4z8" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: Interstellar -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="interstellar">
  <img src="https://img.youtube.com/vi/zSWdZVtXT7E/0.jpg" alt="Interstellar" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Interstellar</h3>
    <a href="watch.html?id=zSWdZVtXT7E" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: RRR -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="rrr">
  <img src="https://img.youtube.com/vi/NgBoMJy386M/0.jpg" alt="RRR" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">RRR</h3>
    <a href="watch.html?id=NgBoMJy386M" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: Parasite -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="parasite">
  <img src="https://img.youtube.com/vi/SEUXfv87Wpk/0.jpg" alt="Parasite" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Parasite</h3>
    <a href="watch.html?id=SEUXfv87Wpk" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie: The Matrix -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="the matrix">
  <img src="https://img.youtube.com/vi/m8e-FF8MsqU/0.jpg" alt="The Matrix" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">The Matrix</h3>
    <a href="watch.html?id=m8e-FF8MsqU" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>
<!-- Movie 11: 3 Idiots -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="3 idiots">
  <img src="https://img.youtube.com/vi/K0eDlFX9GMc/0.jpg" alt="3 Idiots" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">3 Idiots</h3>
    <a href="watch.html?id=K0eDlFX9GMc" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 12: Inception -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="inception">
  <img src="https://img.youtube.com/vi/YoHD9XEInc0/0.jpg" alt="Inception" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Inception</h3>
    <a href="watch.html?id=YoHD9XEInc0" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 13: Zindagi Na Milegi Dobara -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="zindagi na milegi dobara">
  <img src="https://img.youtube.com/vi/tgbNymZ7vqY/0.jpg" alt="Zindagi Na Milegi Dobara" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Zindagi Na Milegi Dobara</h3>
    <a href="watch.html?id=tgbNymZ7vqY" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 14: Bahubali 2 -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="bahubali 2">
  <img src="https://img.youtube.com/vi/G62HrubdD6o/0.jpg" alt="Bahubali 2" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Bahubali 2</h3>
    <a href="watch.html?id=G62HrubdD6o" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 15: Avatar -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="avatar">
  <img src="https://img.youtube.com/vi/5PSNL1qE6VY/0.jpg" alt="Avatar" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Avatar</h3>
    <a href="watch.html?id=5PSNL1qE6VY" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 16: Doctor Strange -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="doctor strange">
  <img src="https://img.youtube.com/vi/aWzlQ2N6qqg/0.jpg" alt="Doctor Strange" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Doctor Strange</h3>
    <a href="watch.html?id=aWzlQ2N6qqg" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 17: Dhoom 3 -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="dhoom 3">
  <img src="https://img.youtube.com/vi/I9zE0xP8Q1I/0.jpg" alt="Dhoom 3" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Dhoom 3</h3>
    <a href="watch.html?id=I9zE0xP8Q1I" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 18: The Dark Knight -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="the dark knight">
  <img src="https://img.youtube.com/vi/EXeTwQWrcwY/0.jpg" alt="The Dark Knight" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">The Dark Knight</h3>
    <a href="watch.html?id=EXeTwQWrcwY" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 19: Pathaan -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="pathaan">
  <img src="https://img.youtube.com/vi/vqu4z34wENw/0.jpg" alt="Pathaan" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Pathaan</h3>
    <a href="watch.html?id=vqu4z34wENw" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 20: The Revenant -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="the revenant">
  <img src="https://img.youtube.com/vi/LoebZZ8K5N0/0.jpg" alt="The Revenant" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">The Revenant</h3>
    <a href="watch.html?id=LoebZZ8K5N0" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>
<!-- Movie 21: Shershaah -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="shershaah">
  <img src="https://img.youtube.com/vi/Q0FTXnefVBA/0.jpg" alt="Shershaah" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Shershaah</h3>
    <a href="watch.html?id=Q0FTXnefVBA" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 22: Iron Man -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="iron man">
  <img src="https://img.youtube.com/vi/8ugaeA-nMTc/0.jpg" alt="Iron Man" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Iron Man</h3>
    <a href="watch.html?id=8ugaeA-nMTc" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 23: Chak De India -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="chak de india">
  <img src="https://img.youtube.com/vi/6a0-dSMWm5g/0.jpg" alt="Chak De India" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Chak De India</h3>
    <a href="watch.html?id=6a0-dSMWm5g" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 24: Joker -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="joker">
  <img src="https://img.youtube.com/vi/zAGVQLHvwOY/0.jpg" alt="Joker" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Joker</h3>
    <a href="watch.html?id=zAGVQLHvwOY" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 25: PK -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="pk">
  <img src="https://img.youtube.com/vi/82ZEDGPCkT8/0.jpg" alt="PK" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">PK</h3>
    <a href="watch.html?id=82ZEDGPCkT8" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 26: The Prestige -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="the prestige">
  <img src="https://img.youtube.com/vi/o4gHCmTQDVI/0.jpg" alt="The Prestige" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">The Prestige</h3>
    <a href="watch.html?id=o4gHCmTQDVI" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 27: War -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="war">
  <img src="https://img.youtube.com/vi/tQ0mzXRk-oM/0.jpg" alt="War" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">War</h3>
    <a href="watch.html?id=tQ0mzXRk-oM" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 28: Forrest Gump -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="forrest gump">
  <img src="https://img.youtube.com/vi/bLvqoHBptjg/0.jpg" alt="Forrest Gump" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Forrest Gump</h3>
    <a href="watch.html?id=bLvqoHBptjg" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 29: Sooryavanshi -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="sooryavanshi">
  <img src="https://img.youtube.com/vi/u5r77-OQwa8/0.jpg" alt="Sooryavanshi" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Sooryavanshi</h3>
    <a href="watch.html?id=u5r77-OQwa8" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 30: Titanic -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="titanic">
  <img src="https://img.youtube.com/vi/kVrqfYjkTdQ/0.jpg" alt="Titanic" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Titanic</h3>
    <a href="watch.html?id=kVrqfYjkTdQ" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>
<!-- Movie 31: Raees -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="raees">
  <img src="https://img.youtube.com/vi/J7_1MU3gDk0/0.jpg" alt="Raees" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Raees</h3>
    <a href="watch.html?id=J7_1MU3gDk0" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 32: John Wick -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="john wick">
  <img src="https://img.youtube.com/vi/C0BMx-qxsP4/0.jpg" alt="John Wick" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">John Wick</h3>
    <a href="watch.html?id=C0BMx-qxsP4" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 33: Gully Boy -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="gully boy">
  <img src="https://img.youtube.com/vi/JfbxcD6biOk/0.jpg" alt="Gully Boy" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Gully Boy</h3>
    <a href="watch.html?id=JfbxcD6biOk" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 34: Gladiator -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="gladiator">
  <img src="https://img.youtube.com/vi/owK1qxDselE/0.jpg" alt="Gladiator" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Gladiator</h3>
    <a href="watch.html?id=owK1qxDselE" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 35: Lagaan -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="lagaan">
  <img src="https://img.youtube.com/vi/4g9rkfyxU2s/0.jpg" alt="Lagaan" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Lagaan</h3>
    <a href="watch.html?id=4g9rkfyxU2s" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 36: The Lion King -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="the lion king">
  <img src="https://img.youtube.com/vi/7TavVZMewpY/0.jpg" alt="The Lion King" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">The Lion King</h3>
    <a href="watch.html?id=7TavVZMewpY" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 37: URI: The Surgical Strike -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="uri">
  <img src="https://img.youtube.com/vi/yu5eW9OzsRs/0.jpg" alt="URI: The Surgical Strike" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">URI: The Surgical Strike</h3>
    <a href="watch.html?id=yu5eW9OzsRs" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 38: Deadpool -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="deadpool">
  <img src="https://img.youtube.com/vi/ONHBaC-pfsk/0.jpg" alt="Deadpool" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Deadpool</h3>
    <a href="watch.html?id=ONHBaC-pfsk" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 39: Sanju -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="sanju">
  <img src="https://img.youtube.com/vi/u2NAuswnTKg/0.jpg" alt="Sanju" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Sanju</h3>
    <a href="watch.html?id=u2NAuswnTKg" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 40: Black Panther -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="black panther">
  <img src="https://img.youtube.com/vi/xjDjIWPwcPU/0.jpg" alt="Black Panther" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Black Panther</h3>
    <a href="watch.html?id=xjDjIWPwcPU" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>
<!-- Movie 41: Andhadhun -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="andhadhun">
  <img src="https://img.youtube.com/vi/2iVYI99VGaw/0.jpg" alt="Andhadhun" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Andhadhun</h3>
    <a href="watch.html?id=2iVYI99VGaw" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 42: Captain Marvel -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="captain marvel">
  <img src="https://img.youtube.com/vi/Z1BCujX3pw8/0.jpg" alt="Captain Marvel" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Captain Marvel</h3>
    <a href="watch.html?id=Z1BCujX3pw8" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 43: Sultan -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="sultan">
  <img src="https://img.youtube.com/vi/wPxqcq6Byq0/0.jpg" alt="Sultan" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Sultan</h3>
    <a href="watch.html?id=wPxqcq6Byq0" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 44: Thor: Ragnarok -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="thor ragnarok">
  <img src="https://img.youtube.com/vi/ue80QwXMRHg/0.jpg" alt="Thor: Ragnarok" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Thor: Ragnarok</h3>
    <a href="watch.html?id=ue80QwXMRHg" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 45: Piku -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="piku">
  <img src="https://img.youtube.com/vi/E_CQYzbMrrU/0.jpg" alt="Piku" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Piku</h3>
    <a href="watch.html?id=E_CQYzbMrrU" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 46: The Avengers -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="the avengers">
  <img src="https://img.youtube.com/vi/eOrNdBpGMv8/0.jpg" alt="The Avengers" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">The Avengers</h3>
    <a href="watch.html?id=eOrNdBpGMv8" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 47: Swades -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="swades">
  <img src="https://img.youtube.com/vi/MlB9VfBZYvI/0.jpg" alt="Swades" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Swades</h3>
    <a href="watch.html?id=MlB9VfBZYvI" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 48: Spider-Man: Homecoming -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="spider man homecoming">
  <img src="https://img.youtube.com/vi/39udgGPyYMg/0.jpg" alt="Spider-Man: Homecoming" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Spider-Man: Homecoming</h3>
    <a href="watch.html?id=39udgGPyYMg" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 49: Dangal -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="dangal">
  <img src="https://img.youtube.com/vi/x_7YlGv9u1g/0.jpg" alt="Dangal" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Dangal</h3>
    <a href="watch.html?id=x_7YlGv9u1g" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>

<!-- Movie 50: Tenet -->
<div class="movie-card bg-gray-800 rounded-lg overflow-hidden" data-title="tenet">
  <img src="https://img.youtube.com/vi/L3pk_TBkihU/0.jpg" alt="Tenet" class="w-full">
  <div class="p-4">
    <h3 class="text-lg font-semibold">Tenet</h3>
    <a href="watch.html?id=L3pk_TBkihU" class="text-red-400 hover:underline">Watch Now</a>
  </div>
</div>


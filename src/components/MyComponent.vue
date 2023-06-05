<template>
  <div>
    <html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Thriller Catalogue</title>
    <link rel="stylesheet" href="style.css" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap"
      rel="stylesheet"
    />
  </head>

  <body>
    <div id="thriller">
      <h1>Thriller Catalogue</h1>
    </div>
    <form>
      <label for="movie">Choose a Thriller Movie:</label>
      <select name="movie" id="movie">
        <option value="475557">Joker</option>
        <option value="458723">Us</option>
        <option value="77">Memento</option>
        <option value="807">Se7en</option>
        <option value="27205">Inception</option>
        <option value="419430">Get Out</option>
        <option value="496243">Parasite</option>
        <option value="11324">Shutter Island</option>
        <option value="157336">Interstellar</option>
        <option value="146233">Prisoners</option>
      </select>
      <br /><br />
      <button type="button">Get</button>
    </form>
    <div id="movie-data"></div>
  </body>
</html>


  </div>
</template>

<script setup>
import axios from 'axios';

const response = await axios.get(
    `https://api.themoviedb.org/3/movie/${selectedMovieId}?api_key=${TMDB_API_KEY}&append_to_response=videos,credits,reviews,similar`
  );
  const movieData = response.data;
  const getMovie = async () => {
  // ...

  const movieDataContainer = document.getElementById("movie-data");
  movieDataContainer.innerHTML = "";
  movieDataContainer.classList.add("movie-data-container");

  const movieTitle = document.createElement("h2");
  movieTitle.innerText = movieData.title;
  movieTitle.classList.add("movie-title");
  movieDataContainer.appendChild(movieTitle);

  const tagline = document.createElement("h4");
  tagline.innerText = `"${movieData.tagline}"`;
  tagline.classList.add("tagline");
  movieDataContainer.appendChild(tagline);

  const moviePoster = document.createElement("img");
  moviePoster.src = `https://image.tmdb.org/t/p/w500${movieData.poster_path}`;
  moviePoster.classList.add("movie-poster");
  movieDataContainer.appendChild(moviePoster);

  const movieOverview = document.createElement("p");
  movieOverview.innerText = movieData.overview;
  movieOverview.classList.add("movie-overview");
  movieDataContainer.appendChild(movieOverview);

  const releaseDate = document.createElement("p");
  releaseDate.innerText = `Release Date: ${movieData.release_date}`;
  releaseDate.classList.add("release-date");
  movieDataContainer.appendChild(releaseDate);

  // ...

  if (director) {
    const directorName = document.createElement("p");
    directorName.innerText = `Director: ${director.name}`;
    directorName.classList.add("director-name");
    movieDataContainer.appendChild(directorName);
  }

  // ...

  const trailers = movieData.videos.results.filter(
    (video) => video.type === "Trailer"
  );

  if (trailers.length > 0) {
    // ...

    const trailerTitle = document.createElement("h3");
    trailerTitle.innerText = "Trailer";
    trailerTitle.classList.add("trailer-title");
    movieDataContainer.appendChild(trailerTitle);

    // ...
  }

  return movieDataContainer;
};

// ...

</script>

<style scoped>
.movie-data-container {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f8f8f8;
}

.movie-title {
  font-size: 24px;
}

.tagline {
  font-size: 18px;
  font-style: italic;
  margin-top: 10px;
}

.movie-poster {
  max-width: 100%;
  height: auto;
  margin-top: 20px;
}

.movie-overview {
  margin-top: 20px;
}

.release-date,
.director-name,
.runtime,
.budget,
.revenue {
  margin-top: 10px;
}

.trailer-title {
  margin-top: 20px;
  font-size: 20px;
}

.trailer-embed {
  margin-top: 10px;
}

</style>

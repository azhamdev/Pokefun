<script>
// import HelloWorld from "./components/HelloWorld.vue"
import defaulImage from "./assets/pokerahasia.png"
import Vue3Lottie from "vue3-lottie"
import LoadingLottie from "./assets/loading.json"
import ig from "./assets/ig.png"

export default {
  setup() {
    const name = "Azham"
    const fotoAwal = "./assets/pokerahasia.png"
    const apiData = {
      apiUrl: "https://pokeapi.co/api/v2/",
      endPoint: "pokemon/",
    }
    return {
      name,
      apiData,
    }
  },

  components: {
    Vue3Lottie,
  },

  data() {
    return {
      ig,
      imagePoke: defaulImage,
      count: 24,
      namePoke: "???",
      loading: false,
      height: "???",
      weight: "???",
      LoadingLottie,
      komentar: [
        { name: "Azham", content: "Wuihh aku dapet Pikachu" },
        { name: "Udin", content: "Okelahh" },
        { name: "Budi", content: "Sedappp ih" },
      ],
      komentarBaru: {
        name: "",
        content: "",
      },
    }
  },

  methods: {
    cek() {
      console.log(this.apiData.apiUrl)
    },

    // randomCount() {
    //   var random = Math.floor(Math.random() * 200 + 1)
    //   this.count = random
    //   console.log(random)
    // },

    generatePokemon() {
      this.loading = true
      var random = Math.floor(Math.random() * 400)
      this.count = random
      console.log(random)
      const url = this.apiData.apiUrl + this.apiData.endPoint + `${this.count}`
      fetch(url)
        .then((data) => data.json())
        .then((pokemon) => {
          this.imagePoke = pokemon.sprites.other.dream_world.front_default
          this.namePoke = pokemon.name
          this.height = pokemon.height
          this.weight = pokemon.weight
          this.loading = false
          console.log(this.imagePoke)
        })
        .catch((err) => {
          console.log(err)
        })
    },
    addComment() {
      this.komentar.push({
        id: 3,
        name: this.komentarBaru.name,
        content: this.komentarBaru.content,
      })
      this.komentarBaru.name = ""
      this.komentarBaru.content = ""
    },
  },
}
</script>

<template>
  <div class="wrapper">
    <div class="container-fluid">
      <nav
        class="navbar navbar-expand-lg bg-light navbar-light navbar-bg-custom"
      >
        <div class="container-fluid">
          <a class="navbar-brand customNavbrand" href="#">
            <img src="./assets/pokemonLogo.png" class="pokemonLogoNav" />
          </a>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a href="#" class="nav-link customNavLink" aria-current="page"
                  >Home</a
                >
              </li>
              <li class="nav-item">
                <a
                  class="nav-link customNavLink"
                  aria-current="page"
                  href="#pokeCatch"
                  >Pokemon Generator</a
                >
              </li>
              <li class="nav-item">
                <a
                  class="nav-link customNavLink"
                  aria-current="page"
                  href="#feedback"
                  >What's People Say</a
                >
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>
    <div class="container container-hero">
      <div class="row row-custom">
        <div class="col-lg-6 col-sm-12 col-custom">
          <div class="container-title">
            <h2 class="pokemon-card-title mb-3">
              <span>Pokemon</span> Generator
            </h2>
            <h1 class="title mb-3">
              Catch em ! Collect your Strongest and Rarest Pokemon
            </h1>
            <div class="">
              <a href="#pokeCatch" class="btn btn-primary btn-letscatch mt-4"
                >Let's Catch</a
              >
            </div>
          </div>
        </div>
        <div class="col-lg-6 col-sm-12 col-custom col-pic">
          <!-- <img class="heroPicture" src="./assets/heroPicture.png" /> -->
          <div
            id="carouselExampleFade"
            class="carousel"
            data-bs-ride="carousel"
          >
            <div class="carousel-inner">
              <div class="carousel-item active heroPicture">
                <img
                  src="./assets/heroPicture.png"
                  class="d-block heroContent"
                  alt="..."
                />
              </div>
              <div class="carousel-item heroPicture">
                <img
                  src="./assets/slide1.png"
                  class="d-block heroContent"
                  alt="..."
                />
              </div>
              <div class="carousel-item heroPicture">
                <img
                  src="./assets/slide2.png"
                  class="d-block heroContent"
                  alt="..."
                />
              </div>
              <div class="carousel-item heroPicture">
                <img
                  src="./assets/slide3.png"
                  class="d-block heroContent"
                  alt="..."
                />
              </div>
              <div class="carousel-item heroPicture">
                <img
                  src="./assets/slide4.png"
                  class="d-block heroContent"
                  alt="..."
                />
              </div>
            </div>
            <button
              class="carousel-control-prev"
              type="button"
              data-bs-target="#carouselExampleFade"
              data-bs-slide="prev"
            >
              <span
                class="carousel-control-prev-icon"
                aria-hidden="true"
              ></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button
              class="carousel-control-next"
              type="button"
              data-bs-target="#carouselExampleFade"
              data-bs-slide="next"
            >
              <span
                class="carousel-control-next-icon"
                aria-hidden="true"
              ></span>
              <span class="visually-hidden">Next</span>
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="container container-poke-generator pb-5" id="pokeCatch">
      <div class="content-show">
        <img class="logoShow mb-3" src="./assets/pokemonLogo.png" />
        <div class="show-pokemon mb-2">
          <div class="WrapperPokeImg">
            <img v-bind:src="`${imagePoke}`" class="pokeMonster" />
          </div>
          <div class="detail">
            <h1 class="namePoke">{{ namePoke }}</h1>
            <h2>
              Height : <span>{{ height }}</span> m
            </h2>
            <h2>
              Weight : <span>{{ weight }}</span> kg
            </h2>
          </div>
        </div>
        <p class="instruction">
          Click button Pokeball below to catch your pokemon !
        </p>
        <div v-if="loading">
          <p class="loading">Loading ...</p>
        </div>
        <a v-on:click="generatePokemon">
          <img src="./assets/pokeBall.png" class="pokeButtonCatch" />
        </a>
      </div>
    </div>
    <a href="#" class="toTop">
      <img src="./assets/up.png" class="toTop" />
    </a>
    <div class="container feedback-wrapper" id="feedback">
      <h2 class="peoplesay">What's People Say</h2>
      <div v-for="item in komentar" class="cardFeedback">
        <h5>{{ item.name }}</h5>
        <p>{{ item.content }}</p>
      </div>
      <div class="addComment-wrapper">
        <div class="row">
          <div class="col-lg-5 addComment">
            <label class="peoplesay">Nama</label>
            <input
              placeholder="Nama"
              type="text"
              v-model="komentarBaru.name"
              class="mb-3 inputName"
            />
            <label class="peoplesay">Komentar</label>
            <textarea
              v-model="komentarBaru.content"
              class="mb-3 inputKomentar"
            ></textarea>
          </div>
        </div>
        <div class="row">
          <div class="col-lg-2">
            <div class="btn btn-primary btn-letscatch" v-on:click="addComment">
              kirim
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="container footer">
      <hr />
      <div class="sosmed">
        <a href="https://www.instagram.com/azham.rasyid/" target="_blank">
          <img src="./assets/ig.png" width="30" class="me-2" />
        </a>
        <a
          href="https://www.linkedin.com/in/a-zham-albar-rasyid-958539203/"
          target="_blank"
        >
          <img src="./assets/linkedin.png" width="30" class="me-2" />
        </a>
        <a href="https://github.com/azhamdev" target="_blank">
          <img src="./assets/github.png" width="30" class="me-2" />
        </a>
      </div>
      <p>A'zham Albar Rasyid</p>
    </div>
  </div>
</template>
<style scoped>
.navbar {
  --bs-navbar-toggler-icon-bg: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3e%3cpath stroke='rgba(113, 195, 242, 1)' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e") !important;
}

.navbar-toggler-icon {
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3e%3cpath stroke='rgba(113, 195, 242, 1)' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e") !important;
}
.peoplesay {
  color: #71c3f2 !important;
}
.footer {
  border-top: 1px solid #fff;
  display: flex;
  flex-direction: column;
  margin-top: 100px;
  justify-content: center;
  align-items: center;
}

.loading {
  color: #71c3f2 !important;
}
.footer p {
  margin-top: 0.7em;
  font-size: 1em;
  font-weight: 500;
  color: #fff;
}
.feedback-wrapper {
  margin-top: 100px;
}
.inputKomentar {
  border-radius: 10px;
  padding: 0.5em;
  height: 210px;
  border: solid 2px #005c91;
  background-color: transparent;
  color: #fff;
  margin-top: 15px;
  padding-left: 20px;
}
.inputName {
  border: solid 2px #005c91;
  background-color: transparent;
  height: 3em;
  padding-left: 20px;
  border-radius: 10px;
  color: #fff;
  margin-top: 15px;
}
.cardFeedback {
  background-color: #eeeeee;
  color: #000;
  padding: 0.5em;
  padding-left: 1.2em;
  margin-bottom: 1em;
  border-radius: 10px;
  box-shadow: 10px 10px 341px -91px rgba(207, 207, 207, 0.75);
  -webkit-box-shadow: 10px 10px 341px -91px rgba(207, 207, 207, 0.75);
  -moz-box-shadow: 10px 10px 341px -91px rgba(207, 207, 207, 0.75);
}
.cardFeedback h5 {
  font-weight: 500;
  font-size: 1em;
  color: #5b5b5b;
}

.addComment {
  display: flex;
  flex-direction: column;
}
.toTop {
  width: 40px;
  height: 40px;
  position: fixed;
  right: 10px;
  bottom: 10px;
}

.col-custom {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
span {
  color: #71c3f2 !important;
  font-weight: 900;
}
.wrapper {
  background-color: #011324;
}

.container-title {
  padding-left: 3vw;
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.navbar-bg-custom {
  background-color: #011324 !important;
}

.customNavbrand {
  color: #71c3f2;
}

.customNavLink {
  color: #71c3f2 !important;
  margin-right: 1vw;
  font-weight: 400;
}
.customNavLink:hover {
  color: #005c91 !important;
}

.title {
  color: white;
  font-weight: 700;
  font-size: 3vw;
}

.content-show {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.namePoke {
  text-transform: capitalize;
  color: #011324;
  font-weight: 700;
  font-size: 2em;
}

.instruction {
  color: #71c3f2 !important;
}

@media only screen and (min-width: 992px) {
  .container-hero {
    height: 100vh;
  }

  .instruction {
    color: #71c3f2 !important;
  }

  .pokemon-card-title {
    font-size: 1.2vw;
    color: #71c3f2 !important;
  }

  .pokemonLogoNav {
    width: 70px;
  }

  .heroPicture {
    width: 40vw;
    height: 30vw;
  }

  .heroContent {
    object-fit: contain;
    overflow: hidden;
    height: 100%;
    width: 100%;
  }
  .btn-letscatch {
    border-radius: 0px;
    padding: 0.4em 3em;
    background-color: #71c3f2 !important;
  }

  .btn-letscatch:hover {
    background-color: #1c99e1 !important;
    color: #011324;
  }

  .show-pokemon {
    background-color: #fff;
    border-radius: 10px;
    border: solid #ffba08 8px;
    height: 50vh;
    width: 50vw;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: row;
  }

  .logoShow {
    width: 15%;
  }

  .pokeButtonCatch {
    width: 5vw;
  }
  .pokeButtonCatch:hover {
    cursor: pointer;
    /* width: 5.5vw; */
    /* transform: rotate(54deg); */
    -webkit-animation: spin 4s linear infinite;
    -moz-animation: spin 4s linear infinite;
    animation: spin 0.9s linear infinite;
  }
  @-moz-keyframes spin {
    100% {
      -moz-transform: rotate(360deg);
    }
  }
  @-webkit-keyframes spin {
    100% {
      -webkit-transform: rotate(360deg);
    }
  }
  @keyframes spin {
    100% {
      -webkit-transform: rotate(360deg);
      transform: rotate(360deg);
    }
  }

  .pokeMonster {
    margin-top: 1em;
    width: 200px;
  }
}

.WrapperPokeImg {
  /* background-color: red; */
  flex-grow: 2;
  display: flex;
  justify-content: center;
}

.detail {
  /* background-color: blue; */
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  padding-left: 0.5em;
}

.detail h2 {
  font-size: 1em;
  color: #011324;
  font-weight: 300;
}

.detail span {
  font-weight: 600;
  color: #011324;
}

@media only screen and (max-width: 991px) {
  .col-pic {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 30px;
  }
  .row-custom {
    display: flex;
    flex-direction: column-reverse;
    padding: 4vw;
  }

  .heroPicture {
    width: 60vw;
    height: 70vw;
  }

  .heroContent {
    width: 100%;
  }
  .title {
    font-size: 8vw;
  }

  .pokemon-card-title {
    font-size: 2vw;
    color: #71c3f2 !important;
  }

  .pokemonLogoNav {
    width: 20%;
  }

  .btn-letscatch {
    border-radius: 0px;
    padding: 0.4em 3em;
    background-color: #71c3f2 !important;
  }

  .btn-letscatch:hover {
    background-color: #1c99e1;
  }

  .container-poke-generator {
    height: 100vh;
    margin-top: 100px;
  }

  .show-pokemon {
    background-color: #fff;
    border-radius: 10px;
    border: solid #ffba08 4px;
    height: 50vh;
    width: 80vw;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .instruction {
    font-weight: 200;
    font-size: 0.6em;
    color: #71c3f2 !important;
  }

  .pokeButtonCatch {
    width: 20vw;
  }
  .logoShow {
    width: 40%;
  }

  .pokeMonster {
    width: 70%;
  }
}
</style>

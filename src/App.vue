<script>
// import HelloWorld from "./components/HelloWorld.vue"

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

  data() {
    return {
      imagePoke: "",
      count: 24,
      namePoke: "",
      loading: false,
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
      var random = Math.floor(Math.random() * 200 + 1)
      this.count = random
      console.log(random)
      const url = this.apiData.apiUrl + this.apiData.endPoint + `${this.count}`
      fetch(url)
        .then((data) => data.json())
        .then((pokemon) => {
          this.imagePoke = pokemon.sprites.other.dream_world.front_default
          this.namePoke = pokemon.name
          this.loading = false
          console.log(this.imagePoke)
        })
        .catch((err) => {
          console.log(err)
        })
    },
  },
}
</script>

<template>
  <div class="wrapper">
    <div class="container-fluid">
      <nav class="navbar navbar-expand-lg bg-light navbar-bg-custom">
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
                <a class="nav-link customNavLink" aria-current="page" href="#"
                  >Pokemon Cards</a
                >
              </li>
              <li class="nav-item">
                <a class="nav-link customNavLink" aria-current="page" href="#"
                  >Contact</a
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
              <a href="#pokeCatch" class="btn btn-primary btn-letscatch"
                >Let's Catch</a
              >
            </div>
          </div>
        </div>
        <div class="col-lg-6 col-sm-12 col-custom col-pic">
          <img class="heroPicture" src="./assets/heroPicture.png" />
        </div>
      </div>
    </div>
    <div class="container container-poke-generator pb-5" id="pokeCatch">
      <div class="content-show">
        <img class="logoShow mb-3" src="./assets/pokemonLogo.png" />
        <div class="show-pokemon mb-2">
          <h1 class="namePoke">{{ namePoke }}</h1>
          <img v-bind:src="`${imagePoke}`" class="pokeMonster" />
        </div>
        <p class="instruction">
          Click button Pokeball below to catch your pokemon !
        </p>
        <div v-if="loading">Please wait ...</div>
        <a v-on:click="generatePokemon">
          <img src="./assets/pokeBall.png" class="pokeButtonCatch" />
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.col-custom {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
span {
  color: #71c3f2;
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
  background-color: none;
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
  font-size: 1em;
}

@media only screen and (min-width: 992px) {
  .container-hero {
    height: 100vh;
  }

  .pokemon-card-title {
    font-size: 1.2vw;
  }

  .pokemonLogoNav {
    width: 70px;
  }
  .btn-letscatch {
    border-radius: 0px;
    padding: 0.4em 3em;
  }

  .btn-letscatch:hover {
    background-color: #1c99e1;
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
    flex-direction: column;
  }

  .logoShow {
    width: 15%;
  }

  .pokeButtonCatch {
    width: 5vw;
  }
  .pokeButtonCatch:hover {
    cursor: pointer;
    width: 5.5vw;
  }

  .pokeMonster {
    margin-top: 1em;
    width: 23%;
  }
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
  }
  .title {
    font-size: 8vw;
  }

  .pokemon-card-title {
    font-size: 2vw;
  }

  .pokemonLogoNav {
    width: 20%;
  }

  .btn-letscatch {
    border-radius: 0px;
    padding: 0.4em 3em;
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

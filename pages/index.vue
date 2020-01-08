<template>
  <section class="home">
    <nav class="nav">
      <div class="nav-logo">
        <nuxt-link to="/#">
          <span>D</span>
          <span>PAJĄK</span>
        </nuxt-link>
      </div>

      <ul class="nav-list">
        <li class="nav-list-item">
          <a class="nav-link" href="#main">O MNIE</a>
        </li>

        <li class="nav-list-item">
          <a class="nav-link" href="#">PROJEKTY</a>
        </li>

        <li class="nav-list-item">
          <a class="nav-link" href="#">SKILLE</a>
        </li>

        <li class="nav-list-item">
          <a class="nav-link" href="#">KONTAKT</a>
        </li>
      </ul>
    </nav>

    <main class="main">
      <div class="brand-info">
        <div class="name">Daniel Pająk</div>

        <TextScroller />

        <div class="icons">
          <a :href="icon.link" target="_blank" v-for="(icon, i) in iconLinks" :key="i">
            <i class="icon" :class="`${icon.type} fa-${icon.name}`"></i>
          </a>
        </div>

        <div class="actions">
          <div class="action">
            <span class="highlight">Skontaktuj</span>
            się ze mną!
          </div>
          <div class="action">
            <span class="highlight">Sprawdź</span>,
            co już umiem!
          </div>
        </div>
      </div>

      <div class="brand-image">
        <img src="thumbnail.jpg" alt />
      </div>
    </main>
  </section>
</template>

<script>
import TextScroller from "@/components/TextScroller";

export default {
  components: {
    TextScroller
  },
  data: () => ({
    iconLinks: [
      {
        type: "fab",
        name: "facebook",
        link: "https://www.facebook.com/pajak.daniel"
      },
      {
        type: "fab",
        name: "youtube",
        link: "https://www.youtube.com/channel/UCvzki2AmZE4H_op0_ALEsZg"
      },
      {
        type: "fab",
        name: "github",
        link: "https://github.com/Spiderous"
      },
      {
        type: "fas",
        name: "envelope",
        link: "mailto:spiderous@protonmail.com"
      }
    ]
  })
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Nunito&display=swap");

@import "@/assets/scss/variables";
@import "@/assets/scss/responsive";

body,
html {
  font-family: "Nunito", sans-serif;
}

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

.highlight {
  color: $primary;
}

a {
  color: $text;
  outline: none;
  text-decoration: none;

  a:hover,
  a:focus {
    color: $primary;
  }
}

.home {
  display: grid;

  grid-template-columns: 30px 1fr 30px;
  grid-template-rows: 80px 1fr;

  color: $text;

  min-height: 100vh;

  background: linear-gradient(rgba(black, 0.8), rgba(black, 0.8)),
    url(/main-bg.jpg);
  background-size: cover;
}

.nav {
  grid-column: 2 / 3;
  grid-row: 1 / 2;

  display: flex;
  justify-content: space-between;
  align-items: center;

  &-logo {
    span:nth-child(1) {
      color: $primary;
      font-weight: $boldFont;
      font-size: 3.5rem;
    }

    span:nth-child(2) {
      letter-spacing: 2px;
      margin-left: -5px;

      font-size: 1.3rem;
      font-weight: $regularFont;
    }
  }

  &-list {
    list-style: none;
    text-decoration: none;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  &-list-item {
    font-size: 2.5rem;
    font-weight: $lightFont;
    padding: 1rem;
  }

  &-link {
    transition: color 250ms;

    &:hover {
      color: $primary;
    }
  }
}

.main {
  grid-column: 2 / 3;
  grid-row: 2 / 3;

  display: grid;
  grid-template-areas: "brand image";

  align-content: center;
  grid-gap: 5rem;

  .brand-info {
    display: flex;
    justify-content: center;
    // align-items: center;
    flex-direction: column;

    grid-area: brand;

    .name {
      position: relative;

      font-size: calc(1.5rem + 5vw);
      padding: 0 1rem;

      &::before {
        position: absolute;
        content: "";

        background-color: $primary;

        top: 50%;
        left: 0;
        transform: translateY(-50%);

        width: 0.3rem;
        height: 70%;
        border-radius: 1rem;
      }
    }

    .text-scroller {
      font-size: calc(10px + 1.5vw);
      // margin-left: 0.5rem;
      opacity: 0.8;

      span {
        font-weight: $boldFont;
      }
    }

    .icons {
      margin: 1.5rem 0;

      .icon {
        color: grey;
        font-size: calc(0.5rem + 1.5vw);
        padding-right: calc(1rem + 0.2vw);

        transition: color 250ms;

        &.fa-facebook:hover {
          color: #1688e6;
        }

        &.fa-youtube:hover {
          color: #f62233;
        }

        &.fa-github:hover {
          color: #c9ccd1;
        }

        &.fa-envelope:hover {
          color: #ec9f48;
        }
      }
    }

    .actions {
      display: none;
      margin-top: 2rem;
    }
  }

  .brand-image {
    display: flex;
    justify-content: center;
    align-items: center;

    grid-area: image;

    img {
      max-width: 20rem;

      border: 5px solid $primary;
      border-radius: 50%;
      box-shadow: 0 0 1.5rem $primary;
    }
  }
}

// Responsive
@include large() {
  .nav-list-item {
    font-size: 1.6rem;
  }
}

@include medium() {
  .nav {
    display: none;
  }

  .main {
    grid-template-areas: "image" "brand";

    .brand-info {
      align-items: center;

      .name {
        font-size: 5rem;

        &::before {
          display: none;
        }
      }

      .text-scroller {
        font-size: 2rem;
      }

      .icons > a > i.icon {
        font-size: 2rem;
        padding: 1rem;
      }
    }

    .brand-image {
      img {
        width: 55vw;
      }
    }
  }
}
</style>

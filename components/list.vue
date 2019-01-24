
<template>
  <section>
    <div class="container-hex">
      <div 
        v-for="event in events" 
        :key="event.id" 
        class="item">
        <div class="hexagon">
          <div class="card">
            <header class="card-header">
              <img 
                v-if="event.Twitter" 
                :src="`https://avatars.io/twitter/${event.Twitter}/small`">
              <p class="card-header-title">{{ event.Nombre }}</p>
            </header>
            <div class="card-content">
              <div class="content">{{ event.Tipo }}</div>
            </div>
            <footer class="card-footer">
              <a
                v-if="event.Contacto.length"
                :href="`mailto:${event.Contacto}`"
                class="card-footer-item"
              >
                <i class="icon ion-md-mail"/>
              </a>
              <a
                v-if="event.Twitter.length"
                :href="`https://twitter.com/${event.Twitter}`"
                class="card-footer-item"
              >
                <i class="icon ion-logo-twitter"/>
              </a>
              <a
                v-if="event.Grupo.length"
                :href="event.Grupo"
                class="card-footer-item"
                target="_blank"
              >
                <i class="icon ion-md-link"/>
              </a>
            </footer>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import { db } from '~/plugins/firebase.js'
export default {
  data() {
    return {
      events: []
    }
  },
  mounted() {
    db.ref('result')
      .once('value')
      .then(snapshot => {
        this.events = snapshot.val()
      })
  }
}
</script>
<style lang="scss">
.card {
  padding: 20% 8px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  color: var(--color-lightBlack);
  position: relative;
  .card-header {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      border-radius: 50%;
    }
    .card-header-title {
      font-weight: bold;
      text-align: center;
    }
  }
  .card-content {
    display: flex;
    justify-content: center;
  }
  .card-footer {
    display: flex;
    font-size: 20px;
    justify-content: center;
    i {
      color: black;
      margin: 0 20%;
    }
  }
}
body {
  padding-top: 30px;
}
h1,
h2,
h3 {
  font-weight: 100;
  text-align: center;
}
h1,
h2 {
  line-height: 20pt;
}
h1 {
  font-size: 30pt;
}
h2 {
  font-size: 24pt;
}

h3 {
  font-family: 'Open Sans', serif;
  font-size: 10pt;
}

.container-hex {
  display: grid;
  grid-template-columns: repeat(10, 100px);
  grid-column-gap: 5px;
  margin-top: 100px;
  margin-bottom: 100px;
  margin-left: 50px;
  width: 1040px;
  position: relative;
  margin-left: auto;
  margin-right: auto;
}

.item {
  grid-column: span 2;
  width: 200px;
  padding: 0 0 231px 0;
  -o-transform: rotate(-60deg) skewY(30deg);
  -moz-transform: rotate(-60deg) skewY(30deg);
  -webkit-transform: rotate(-60deg) skewY(30deg);
  -ms-transform: rotate(-60deg) skewY(30deg);
  transform: rotate(-60deg) skewY(30deg);
  overflow: hidden;
  visibility: hidden;
  margin-top: -50px;
}

.item:nth-child(9n + 1) {
  grid-column-start: 1;
}
.item:nth-child(9n + 2) {
  grid-column-start: 3;
}
.item:nth-child(9n + 3) {
  grid-column-start: 5;
}
.item:nth-child(9n + 4) {
  grid-column-start: 7;
}
.item:nth-child(9n + 5) {
  grid-column-start: 9;
}
.item:nth-child(9n + 6) {
  grid-column-start: 2;
}
.item:nth-child(9n + 7) {
  grid-column-start: 4;
}
.item:nth-child(9n + 8) {
  grid-column-start: 6;
}
.item:nth-child(9n) {
  grid-column-start: 8;
}

.hexagon {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: goldenrod;
  -o-transform: skewY(-30deg) rotate(60deg);
  -moz-transform: skewY(-30deg) rotate(60deg);
  -webkit-transform: skewY(-30deg) rotate(60deg);
  -ms-transform: skewY(-30deg) rotate(60deg);
  transform: skewY(-30deg) rotate(60deg);
  overflow: hidden;
}

.item * {
  visibility: visible;
}

/**** Responsive wizardry ****/

@media (max-width: 1100px) {
  .container-hex {
    grid-template-columns: repeat(8, 100px);
    width: 830px;
  }
  .item:nth-child(7n + 1) {
    grid-column-start: 1;
  }
  .item:nth-child(7n + 2) {
    grid-column-start: 3;
  }
  .item:nth-child(7n + 3) {
    grid-column-start: 5;
  }
  .item:nth-child(7n + 4) {
    grid-column-start: 7;
  }
  .item:nth-child(7n + 5) {
    grid-column-start: 2;
  }
  .item:nth-child(7n + 6) {
    grid-column-start: 4;
  }
  .item:nth-child(7n) {
    grid-column-start: 6;
  }
}

@media (max-width: 850px) {
  .container-hex {
    grid-template-columns: repeat(6, 100px);
    width: 620px;
  }
  .item:nth-child(5n + 1) {
    grid-column-start: 1;
  }
  .item:nth-child(5n + 2) {
    grid-column-start: 3;
  }
  .item:nth-child(5n + 3) {
    grid-column-start: 5;
  }
  .item:nth-child(5n + 4) {
    grid-column-start: 2;
  }
  .item:nth-child(5n) {
    grid-column-start: 4;
  }
}

@media (max-width: 720px) {
  .container-hex {
    grid-template-columns: repeat(4, 100px);
    width: 410px;
  }
  .item:nth-child(3n + 1) {
    grid-column-start: 1;
  }
  .item:nth-child(3n + 2) {
    grid-column-start: 3;
  }
  .item:nth-child(3n) {
    grid-column-start: 2;
  }
}
</style>

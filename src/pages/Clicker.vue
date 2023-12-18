<template>
  <div class="row">
    <div class="col">
      <h1>GONG CLICKER</h1>
      <audio controls>
        <source :src="import ('../assets/music.mp3')" type="audio/mpeg" controls autoplay>
        Your browser does not support the audio tag.
      </audio>
      <img src="https://cdn.dribbble.com/users/1226119/screenshots/6271830/____400300.gif" class="img-fluid" alt="">
    </div>
    <div class="col">
      <h3 class="text-center">Hits {{ cookies }}</h3>
      <img src="https://www.thegongshop.com/cdn/shop/products/the-gong-shop-12-chinese-chau-gong-set-with-stand-and-mallet-cg12-p0561-28137294200906.png?v=1628019965" class="img-fluid" @click="cookies++">
    </div>
    <div id="click" class="col">
      <button v-for="(upgrade, name) in upgrades"
        v-on:click="play" type="button"
        class="btn btn-outline-primary py-3 mt-3"
        :disabled="cookies<upgrade.price"
        @click="buyUpgrade(upgrade)">
        Buy {{ name }} for 
        {{ upgrade.price }} hits ({{upgrade.cps}} hits per second)
        {{ upgrade.count }}
      </button>
    </div>
  </div>
</template>

<style>
body {
  background-image: url("../assets/background.jpg");
  background: cover;
  background-size: cover;
  background-repeat: no-repeat;
}

.row {
  margin: 4em;
}

.btn {
  padding: 1em;
  background-color: blanchedalmond;
  color: black;
  border: none;
}

</style>

<script>
import music from '../assets/music.mp3';
import MusicPlayer from '../components/MusicPlayer.vue';

export default {
    created() {
        this.music = music;
        setInterval(() => {
            for (const upgrade in this.upgrades) {
                this.cookies = (parseFloat(this.cookies) + this.upgrades[upgrade].cps * this.upgrades[upgrade].count).toFixed(1);
            }
        }, 1000);
    },
    data() {
        return {
            music:null,
            cookies: 0,
            upgrades: {
                mallet: { price: 10, cps: 0.1, count: 0 },
                dancers: { price: 100, cps: 1, count: 0 },
                titanium_mallet: { price: 1000, cps: 10, count: 0 },
                dragon: { price: 10000, cps: 100, count: 0 },
                temple: { price: 100000, cps: 1000, count: 0 },
            }
        };
    },
    methods: {
        buyUpgrade(upgrade) {
            if (this.cookies >= upgrade.price) {
                this.cookies -= upgrade.price;
                upgrade.price += Math.ceil(upgrade.price * 0.25);
                upgrade.count++;
            }
        }
    },
    components: { MusicPlayer }
};
</script>

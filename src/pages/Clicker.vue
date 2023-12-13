<template>
  <div class="row">
    <div class="col">
      <h1>GONG CLICKER</h1>
      <audio controls>
        <source src="../assets/music.m4a" type="audio/x-m4a" controls autoplay>
        Your browser does not support the audio tag.
      </audio>
      <MusicPlayer src="../assets/music.m4a" playerid="audio-player" > </MusicPlayer>
      <img src="https://cdn.dribbble.com/users/1226119/screenshots/6271830/____400300.gif" class="img-fluid" alt="">
    </div>
    <div class="col">
      <h3 class="text-center">Hits {{ cookies }}</h3>
      <img src="https://assets.stickpng.com/images/5a9d5c039fc609199d0ff0c8.png" class="img-fluid" @click="cookies++">
    </div>
    <div class="col ">
      <button v-for="(upgrade, name) in upgrades"
        @click.prevent="playSound('http://soundbible.com/mp3/Air Plane Ding-SoundBible.com-496729130.mp3')"
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
import MusicPlayer from '../components/MusicPlayer.vue';

export default {
  build: {
    loaders: {
      vue: {
        transformAssetUrls: {
          audio: 'src'
        }
      }
    },

    extend (config, ctx) {
      config.module.rules.push({
        test: /\.(ogg|mp3|wav|mpe?g)$/i,
        loader: 'file-loader',
        options: {
          name: '[path][name].[ext]'
        }
      })
    }
  },
    created() {
        setInterval(() => {
            for (const upgrade in this.upgrades) {
                this.cookies = (parseFloat(this.cookies) + this.upgrades[upgrade].cps * this.upgrades[upgrade].count).toFixed(1);
            }
        }, 1000);
    },
    data() {
        return {
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
}

</script>

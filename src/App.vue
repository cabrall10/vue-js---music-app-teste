<template>
  <div id="app">

    <header>
      <h1>Spotify de Pobre</h1>
    </header>
    <main>
      <section class="player"> 
        <h2 class="song-title">{{ current.title }} - <span> {{ current.artist }} </span></h2>
      </section>
      <div class="contro">
        <button class="prev">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next">Next</button>
      </div>
    </main>

  </div>
</template>

<script>
export default {
  name: 'app',
    data () {
      return {
        current: {},
        index: 0,
        isPlaying: false,
        songs: [
          {
            title: 'Far Away',
            artist: 'Breaking Benjamin',
            src: require('./assets/breakingBenjamin-far-away.mp3')
          },
          {
            title: 'Killing me slowly',
            artist: 'Bad Wolves',
            src: require('./assets/badWolves-killing-me-slowly.mp3')
          }
        ],
        player: new Audio()
      }
    },
    methods: {
      play (song) {
        if (typeof song.src != "undefined"){
          this.current = song;
          
          this.player.src = this.current.src;
        }

        this.player.play();
        this.isPlaying = true;
      },

      pause () {
        this.player.pause();
        this.isPlaying = false;
      }
    },
    created () {
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
    }
}

</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #FFF;
}
</style>

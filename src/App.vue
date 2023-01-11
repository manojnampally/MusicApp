<template>
  <div class="app">
    <div class="header">
      <h1>Let's Groove in</h1>
    </div>
    <div>
      <div class="player">
        <h2 class="bgm-title">
          {{ current.title }} - <span>{{ current.singer }}</span>
        </h2>
        <div>
           <div class="img-section">
          <img :src="current.img" class="song-img" />
        </div>
        <div class="control">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
        </div>
       
      </div>
      <div class="playList">
        <h3>My PlayList</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="song.src == current.src ? 'song playing' : 'song'"
        >
          {{ song.title }} - {{ song.singer }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current: {},
      index: 0,
      songs: [
        {
          title: "Pushpa",
          singer: "DSP",
          src: require("./assets/Pushpa-Ringtone.mp3"),
          img: require("./assets/pushpa.jpeg"),
        },
         {
          title: "Ori Devuda",
          singer: "Leon James",
          src: require("./assets/Gundelonaa-Theme-BGM.mp3"),
          img: require("./assets/ori-devuda.jpg"),
        },
        {
          title: "Vikram",
          singer: "Anirudh",
          src: require("./assets/Vikram-The-Eagle-is-Coming-Ringtone.mp3"),
          img: require("./assets/Vikram.jpg.webp"),
        },
        {
          title: "Arjun Reddy",
          singer: "Harshavardhan Rameshwar",
          src: require("./assets/Arjun-Warn-Opposite-Team-BGM.mp3"),
          img: require("./assets/Arjun Reddy.webp"),
        },
        {
          title: "Harry Potter",
          singer: "Manoj",
          src: require("./assets/Harry Potter - Marimba.mp3"),
          img: require("./assets/Harry.jpg"),
        },
         {
          title: "Scam 1992",
          singer: "Achint Thakkar",
          src: require("./assets/Scam 1992.mp3"),
          img: require("./assets/Scam 1992.jpg"),
        },
         {
          title: "Vikram Vedha",
          singer: "Cam C.S",
          src: require("./assets/Vikram-Asks-Vedha-BGM.mp3"),
          img: require("./assets/Vikram_Vedha_poster.jpg"),
        },
       {
          title: "Rab Ne Bana Di Jodi",
          singer: "Jaideep Sahni",
          src: require("./assets/Tujh Mein Rab Dikhta Hai.mp3"),
          img: require("./assets/Rab_Ne_Bana_Di_Jodi.jpg"),
        },
      ],
      player: new Audio(),
      isPlaying: false,
    };
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener(
        "ended",
        function () {
          this.index++;
          if (this.index > this.songs.length - 1) {
            this.index = 0;
          }
          this.current = this.songs[this.index];
          this.play(this.current);
        }.bind(this)
      );
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
};
</script>

<style>
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  color: #fff;
  background-color: #212121;
}
body {
  font-family: sans-serif;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.bgm-title {
  font-size: 30px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
  color: #cc2e5d;
}
.bgm-title span {
  font-weight: 400;
  font-style: italic;
  color: palevioletred;
}
.control {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  background: none;
  appearance: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.9;
}
.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  color: #fff;
  background-color: #cc2e5d;
  border-radius: 8px;
}
.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  color: #fff;
  background-color: #ff5858;
  border-radius: 6px;
}
.playList {
  padding: 0px 30px;
}
.playList h3 {
  color: crimson;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playList .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playList:hover {
  color: #ff5858;
}
.playList .song.playing {
  color: #fff;
  background-image: linear-gradient(#cc2e5d, #ff5858);
}
.song-img {
  max-width: 600px;
  max-height: 150px;
  border-radius: 50%;
}
.img-section{
  text-align: center;
}
</style>

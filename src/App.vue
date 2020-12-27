<template>
  <div >
    <Header />
    <main class="container">
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist}}</span></h2>
        <div class="controls">
          <span class="music-icon prev" @click="prev"><i class="fas fa-fast-backward"></i></span>
          <span class="music-icon play" v-if="!isPlaying" @click="play"><i class="fas fa-play"></i></span>
          <span class="music-icon pause" v-else @click="pause"><i class="fas fa-pause"></i></span>
          <span class="music-icon next" @click="next"><i class="fas fa-fast-forward"></i></span>
          <span class="music-icon shuffle" @click="shuffle"><i class="fas fa-random"></i></span>
        </div>
      </section>
      <section class="playlist">
        <h3>Playlist</h3>
          <ul>
            <li v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src === current.src) ? 'song-playing' : 'song'">
              {{ song.title }} - {{ song.artist }}
            </li>
        </ul>

      </section>
    </main>
    <Footer />
  </div>
</template>


<script>
import Header from './components/Header'
import Footer from './components/Footer'

export default {
  name: 'app',
  components : {
    Header,
    Footer,
  },
  data() {
    return{
      current:{},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Homura - Demon Slayer',
          artist: 'LiSA',
          src: require('./assets/musics/homura.mp3')
        },
        {
          title: 'Unravel-Tokyou Ghoul',
          artist: 'Toru Kitajima',
          src: require('./assets/musics/tokyo-ghoul-unravel.mp3')
        },
        {
          title: 'Black Clover Opening 10 FullBlack',
          artist: ' Vickeblank',
          src: require('./assets/musics/Black Clover Opening 10 FullBlack Catcherby VickeblankaLyrics.mp3')
        },
        {
          title: 'Rent-a-Girlfriend - Opening FullCentimeter',
          artist: 'The Peggies',
          src: require('./assets/musics/Rent-a-Girlfriend - Opening FullCentimeterby the peggies.mp3')
        },
        {
          title: 'Full opening naruto Blue Bird',
          artist: 'Ikimono Gakari',
          src: require('./assets/musics/Full opening naruto Blue Bird Lyrics Full.mp3')
        },
        {
          title: 'SLAMDUNK THEME SONG LYRICS',
          artist: 'Kimi Ga Suki Da To Sakebitai',
          src: require('./assets/musics/SLAMDUNK THEME SONG LYRICS.mp3')
        },
        {
          title: '5 Centimeters Per Second Ending Soundtrack',
          artist: 'Shinta Kanou',
          src: require('./assets/musics/5 Centimeters Per Second Ending Soundtrack (2007).mp3')
        },
      ],
      player : new Audio()
    }
  },
  methods:{
    play (song){
      if(typeof song.src != "undefined"){
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    },
    prev () {
      this.index--;
      if (this.index < 0){
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },

    shuffle () {
      let random = Math.floor(Math.random()* this.songs.length)
      this.index = random;
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  mounted (){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
header{
  background: #EE6C4D;
  display:flex;
  align-content: center;
  justify-content: center;
  padding: .2rem 0;
  text-align: center;
  margin-bottom: 1rem;
}
header h1{
  color: #fff;
}
body{
  background: #293241;
  color: #E0FBFC;
  font-family: 'Poppins', sans-serif;
}
.player{
  background: #3D5A80;
  color: #E0FBFC;
  border-radius: 5px;
  padding: .5rem;
  overflow:hidden;
}
.music-icon{
  margin-left: 2rem;
  color: #EE6C4D;
  font-size: 1.8rem;
}
.music-icon:hover{
  color: #fff;
  font-size: 1.85rem;
}
.controls{
  width: 100%;
  display:flex;
  justify-content: center;
  align-items: center;
}
.song-title{
  text-align: center;
}
.playlist{
  margin-top: 70px;
}
ul{
  margin:0;
  padding: 0;
  margin-top:1rem;
}
li{
   list-style: none;
   background: #3D5A80;
   color: #fff;
   margin-bottom: .5rem;
   padding: .5rem .5rem;
   border-radius: 5px;
   cursor:pointer;
   transition: 500ms ease-out;
}
li:hover{
  background: #98C1D9;
  color: #3D5A80;
  padding-left: 1rem!important;
}
.song-playing{
  background: #EE6C4D;
   color: #fff;
}
footer{
  text-align: center;
  font-size: .9rem;
  margin-top:.5rem;
}

</style>
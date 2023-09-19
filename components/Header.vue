<template>
    <nav class="flex items-center md:justify-center lg:p-6 p-2 black-bg text-white w-screen max-w-full ">
      <div
        class="w-auto pt-3 pr-4 h-18 flex flex-none justify-left items-center text-5xl  border-t-2 border-b-2 border-solid border-white">
        <NuxtLink to="/">RTL3</NuxtLink>   
           
      </div>
      <div class="flex hidden md:flex flex-row justify-content-start h-18 flex-grow items-center border-t-2 border-b-2 border-solid border-white">
          <!-- <div><NuxtLink class="text-3xl p-2" to="/">SHOWS</NuxtLink></div>           -->
          <NuxtLink class="text-3xl p-2" to="/about">ABOUT</NuxtLink>
          <NuxtLink class="text-3xl p-2" to="/contact">CONTACT</NuxtLink>
          <NuxtLink class="text-2xl p-2" to="/getinvolved">GET INVOLVED! 👋</NuxtLink>
        </div> 
      <!-- <div class="flex flex-row justify-end h-18 flex-grow items-center border-t-2 border-b-2 border-solid border-white">              
        <div class="d-flex flex-column text-right">
          <div class="calibre pt-1 text-xs hidden md:block md:text-base "><span class="dot" style="color:red">&bull;</span>  ON AIR <br class="md:hidden"/>— CURRENT SHOW</div>
          <div class="calibre pt-1 text-xs md:hidden md:text-base "><span class="dot" style="color:red">&bull;</span>  ON AIR</div>
          <h3 class="pl-3  md:text-4xl text-md md:text-base" v-if="apiStoreData">
            {{apiStoreData.shows.current.name}} 
          </H3>
        </div>        
      </div>-->
      <div class="flex justify-content-center border-t-2 h-18 border-b-2 items-center border-solid border-white">
        <div class="border-l-2 h-10 border-solid border-1 border-white mx-3"></div>
      </div>
      <div
        class="w-1/3 md:w-3/12 h-18 flex flex-col justify-around items-end content-end pr-3 border-t-2 border-b-2 border-solid border-white">
        <!-- <progressBar class="hidden md:flex" v-if="apiStoreData" :startDate="apiStoreData.shows.current.starts"
          :endDate="apiStoreData.shows.current.ends"></progressBar> -->
        <div class="py-1 text-right">   
          <!-- mobile        -->
          <!-- <h3 class="calibre font-bold text-sm md:hidden" v-if="apiStoreData">
            {{artistName}}         
          </H3>           -->
          <!-- <h4 class="calibre text-xs pt-1 leading-3 md:hidden" >{{title}}</h4> -->
          <!-- desktop -->
          <!-- <div class="hidden md:block calibre font-bold text-right text-lg leading-tight" v-if="apiStoreData">            
            {{ artistName }}
          </div> -->
          <!-- <h4 class="hidden md:block calibre text-right text-lg md:text-base leading-tight">{{ title }}</h4> -->
        </div>
      </div>
      <!-- <div class="grid  h-full">
        <div class="onTop">
          <img class="w-18 flex-none cover sm:hidden md:flex" v-if="currentTrackId!=0"
          :src="`https://rtl3.net/admin/api/track?id=${currentTrackId}&return=artwork`" alt="wartwork" @error="imageUrlAlt"/>
        </div>
        <img class="w-18 onTop flex-none cover sm:hidden md:flex" v-if="!currentTrackId"
          :src="`/defaut.png`" alt="default-wartwork"/>
        <div class="onTop flex items-center justify-center" v-if="isPlaying"><img v-if="isPlaying" class="w-12"  src="/stopIcon.png" @click="play"/></div>
        <div class="onTop flex items-center justify-center " v-if="!isPlaying"><img v-if="!isPlaying" class="w-12  "  src="/playIcon.png" @click="play"> </div>   
      </div> -->
                   
        
    </nav>   
    
</template>

<script>
  export default {
    data: () => ({        
    streamInfos: null,
    player: null,
    currentArtwork: null,
  }),
  computed: {
    counter() {
      return this.$store.state.counter
    },
    apiStoreData() {
      return this.$store.state.apiData
    },
    currentTrackId(){
      return this.$store.state.currentTrackId
    },
    audioPlayer(){
      return this.$store.state.player
    },
    isPlaying(){
      return this.$store.state.isPlaying
    },
    artistName(){
      return this.truncate(this.apiStoreData.tracks.current.name.split("-")[0], 36)
    },
    title(){
      return this.apiStoreData?this.truncate(this.apiStoreData.tracks.current.name.split("-")[1], 36):""
    },
  },
  head() {
    if (this.apiStoreData)
      return {
        title: "RTL3 - " + this.apiStoreData.tracks.current.name
      }
  },
  mounted: function () {
      this.$store.dispatch('fetchApiData')
      this.timer2 = setInterval(() => {
        this.$store.dispatch('fetchApiData')
      }, 2000)
  },
  methods: {
    play() {
        if (!this.isPlaying) {
          this.audioPlayer.src="https://rtl3.net/live";
          this.audioPlayer.play();        
          this.$store.commit('setIsPlaying', {isPlaying: true})      
        //   this.timer = setInterval(() => {
        //   this.getStreamInfos()
        // }, 1000)
        } else {
          this.pause();        
        }
      },
    pause() {
        this.audioPlayer.pause();
        this.audioPlayer.src="";
        this.$store.commit('setIsPlaying', {isPlaying: false})      
        //this.paused = true;
      },
    imageUrlAlt(event) {
      const random = Math.floor(Math.random() * 3)+1;
      event.target.src = "/defaut"+random+".jpg"
    },
    truncate(str, n){
      if(str) return (str.length > n) ? str.slice(0, n-1) + '…' : str;
    }
  }
  }
</script>

<style lang="postcss" scoped>
.cover{
  border-top: white solid 2px;
  border-bottom: white solid 2px;
}

.onTop {
  grid-row: 1;
  grid-column: 1;
}

@keyframes blink {
  0% { opacity: 0; }
  50% { opacity: 1; }
  100% { opacity: 0; }
}
.dot {
  animation: blink 2s infinite;
}
</style>
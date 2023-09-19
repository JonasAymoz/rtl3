<script setup>
</script>

<template>
    <container class="grid black-bg">
    <div class="h-100 grid text-white ">
      <div class="image-stack mb-10">
        <div class="image-stack__item image-stack__item--top"
          v-if="paused && streamInfos && streamInfos.tracks.current">
          <img class="invert" style="max-width:250px; filter:invert(1)" src="/play.png" @click="play">
        </div>
        <div class="image-stack__item image-stack__item--top" v-bind:class="{ active: this.playing }">
          <img class="invert" style="max-width:250px; filter:invert(1)" src="/circle_logo.png" @click="play">
        </div>
        <div class="image-stack__item image-stack__item--bottom">
          <img style="max-width:250px; filter:invert(1)" src="/text_logo.png">
        </div>
      </div>
      
      <nav class="menu text-white " style="z-index:50">
        <div class="menu__item">
          <div class="marquee">
            <div class="marquee__inner">
              <span>RADIO TOUJOURS LIBRE</span>
            </div>
          </div>
        </div>
      </nav>

      <div class="content p-5 mt-20">
        <p class="pt-7 noto text-center">Let us know : contact@rtl3.net </p>
      </div>
    </div>

  </container>
</template>

<style lang="postcss">

container {
  grid-template-rows: auto 1fr auto;
  height: 100vh;
}

.black-bg {
  background-color: #1D1D1D;
  color : white;
}

.title-panel{
  padding: 12px;
}
.title{
  color: white;
  background: black;
  font-family: 'Special Elite', cursive;
}
 .image-stack__item--top:hover {
  cursor: pointer; 
 }

.image-stack {
  display: grid;
  position: relative;
  grid-template-columns: 1fr;
  justify-items: center;
  align-items: center;
}

.image-stack__item--bottom {
  grid-column: 1;
  grid-row: 1;
  z-index: 0;
  -webkit-transform:translate3d(0,0,0);
}

.image-stack__item--top {
  grid-row: 1;
  grid-column: 1;
  z-index: 1;
    &.active {    
	  animation: rotateAnimation 9s linear infinite;
  }
}
@keyframes rotateAnimation {
	from {transform: rotate3d(0,1,0, 0deg);}
	to {transform: rotate3d(0, 1, 0, 360deg);}
}
.cover{
  height: 72px;
}

hidden{
  display: none;
}
.next-show {
  padding-top: 1rem;
  color: white;    
}
.next-show-panel {
  padding: 1rem;
  font-size: 0.9rem;
  color: white;
  background: black;
  font-family:'Special Elite', cursive;
}

.mt-2 {
  margin-top: 1rem;
}

.header{
  display: flex;
}

.menu {
	-webkit-touch-callout: none;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
	padding: 0;
	--marquee-width: 99vw;
	--offset: 30vw;
	--move-initial: calc(-25% + var(--offset));
	--move-final: calc(-50% + var(--offset));
	--item-font-size: 10vw;
	counter-reset: menu;
}


.marquee {
	position: absolute;
	left: 0;
	width: var(--marquee-width);
	overflow: hidden;
	pointer-events: none;
}

<!-- .marquee__inner {
	width: fit-content;
	display: flex;
	position: relative;
	transform: translate3d(var(--move-initial), 0, 0);
	animation: marquee 10s linear infinite;
	animation-play-state: paused;
	opacity: 0;
	transition: opacity 0.1s;
} -->

.marquee .marquee__inner {
	animation-play-state: running;
	opacity: 1;
	transition-duration: 0.4s;
}

.marquee span {
  text-align: center;
	white-space: nowrap;
	font-size: var(--item-font-size);
	padding: 0 1vw;
	font-weight: 900;
	line-height: 1.15;
}

@keyframes marquee {
	0% {
		transform: translate3d(var(--move-initial), 0, 0);
	}

	100% {
		transform: translate3d(var(--move-final), 0, 0);
	}
}
</style>

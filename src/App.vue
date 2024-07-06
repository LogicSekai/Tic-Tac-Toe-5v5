<!-- <script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script> -->

<template>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView /> -->
  <div class="section">
    <div class="container lobby flex column">
      <h1>Tic Tac Toe</h1>
      <div class="users-online">Users Online: 403</div>
      <div class="flex">
        <div class="flex column p-5 item-center">
          <div class="profile">
            <img src="https://static.zerochan.net/Seele.%28Honkai.Star.Rail%29.full.3934757.jpg" alt="">
          </div>
          <h2>Guest</h2>
          <div class="login-method">
            <div class="login-button">
              <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQSTLNyHEp8ERADDJDy5wXQLoV_Lj0YTmv6eA&s"
                alt="">
            </div>
            <div class="login-button">
              <img
                src="https://cdn.icon-icons.com/icons2/2890/PNG/512/apps_social_media_facebook_logo_social_network_media_online_icon_182716.png"
                alt="">
            </div>
            <div class="login-button">
              <img src="https://img.freepik.com/premium-psd/black-brand-new-twitter-x-logo-icon_1129635-1.jpg" alt="">
            </div>
          </div>
        </div>
        <div class="play-mode p-5">
          <h2>Game Mode</h2>
          <div class="play">
            <div class="icon"><svg data-slot="icon" fill="none" stroke-width="1.5" stroke="currentColor"
                viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z">
                </path>
              </svg></div>
            <div class="mode">SOLO vs Computer</div>
          </div>
          <div class="play">
            <div class="icon"><svg data-slot="icon" fill="none" stroke-width="1.5" stroke="currentColor"
                viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M15 19.128a9.38 9.38 0 0 0 2.625.372 9.337 9.337 0 0 0 4.121-.952 4.125 4.125 0 0 0-7.533-2.493M15 19.128v-.003c0-1.113-.285-2.16-.786-3.07M15 19.128v.106A12.318 12.318 0 0 1 8.624 21c-2.331 0-4.512-.645-6.374-1.766l-.001-.109a6.375 6.375 0 0 1 11.964-3.07M12 6.375a3.375 3.375 0 1 1-6.75 0 3.375 3.375 0 0 1 6.75 0Zm8.25 2.25a2.625 2.625 0 1 1-5.25 0 2.625 2.625 0 0 1 5.25 0Z">
                </path>
              </svg></div>
            <div class="mode">Player vs Player</div>
          </div>
          <div class="play" @click="startSearchMatch_5v5">
            <div class="icon"><svg data-slot="icon" fill="none" stroke-width="1.5" stroke="currentColor"
                viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M18 18.72a9.094 9.094 0 0 0 3.741-.479 3 3 0 0 0-4.682-2.72m.94 3.198.001.031c0 .225-.012.447-.037.666A11.944 11.944 0 0 1 12 21c-2.17 0-4.207-.576-5.963-1.584A6.062 6.062 0 0 1 6 18.719m12 0a5.971 5.971 0 0 0-.941-3.197m0 0A5.995 5.995 0 0 0 12 12.75a5.995 5.995 0 0 0-5.058 2.772m0 0a3 3 0 0 0-4.681 2.72 8.986 8.986 0 0 0 3.74.477m.94-3.197a5.971 5.971 0 0 0-.94 3.197M15 6.75a3 3 0 1 1-6 0 3 3 0 0 1 6 0Zm6 3a2.25 2.25 0 1 1-4.5 0 2.25 2.25 0 0 1 4.5 0Zm-13.5 0a2.25 2.25 0 1 1-4.5 0 2.25 2.25 0 0 1 4.5 0Z">
                </path>
              </svg></div>
            <div class="mode">5v5 Tim Battle</div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div v-if="searchMatch_5v5" class="search-match">
    <div class="container">
      <div>Mencari pemain</div>
      <div class="timer">{{ formattedTime }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchMatch_5v5: false,
      searchMatch_5v5_minutes: 0,
      searchMatch_5v5_seconds: 0,
      timerInterval: null
    }
  },
  computed: {
    formattedTime() {
      const formattedMinutes = String(this.searchMatch_5v5_minutes).padStart(2, '0')
      const formattedSeconds = String(this.searchMatch_5v5_seconds).padStart(2, '0')
      return `${formattedMinutes}:${formattedSeconds}`
    }
  },
  methods: {
    startSearchMatch_5v5(){
      if (this.timerInterval) return
      this.searchMatch_5v5 = true

      this.timerInterval = setInterval(() => {
        this.searchMatch_5v5_seconds++
        if (this.searchMatch_5v5_seconds === 60) {
          this.searchMatch_5v5_minutes++
          this.searchMatch_5v5_seconds = 0
        }
      }, 1000)
    },
    stopSearchMatch_5v5() {
      clearInterval(this.timerInterval)
      this.timerInterval = null
      this.searchMatch_5v5 = false
    }
  }
}
</script>

<style scoped>
.section{
  display: flex;
  width: 100%;
  height: 100vh;
  background: #1B1B28;
}

.flex{
  display: flex;
}

.column{
  flex-direction: column;
}

.p-5{
  padding: 10px 80px;
}

.item-center{
  align-items: center;
}

.lobby.container{
  position: relative;
  margin: auto;
}

.users-online{
  margin-top: 30px;
  color:#ffffff;
  margin-left: auto;
}

.container h1{
  margin: auto;
  color: #ffffff;
  font-weight: 600;
}

.container h2{
  color: #ffffff;
}

.lobby .profile{
  width: 120px;
  height: 120px;
  border: 2px solid #957bff;
  border-radius: 12px;
  overflow: hidden;
}

.lobby .profile img{
  width: 120px;
  height: 120px;
  object-fit: cover;
}

.login-method{
  margin-top: 20px;
  display: flex;
  
}

.login-button{
  width: 60px;
  height: 60px;
  padding: 5px;
  border-radius: 30px;
  overflow: hidden;
  margin: auto 10px;
  background: #ffffff;
}

.login-button img{
  margin: auto;
  width: 50px;
  height: 50px;
  object-fit: cover;
}

.play-mode svg{
  width: 30px;
  height: 30px;
  color: #ffffff;
}

.play-mode .play{
  width: 240px;
  border: 2px solid #957bff;
  padding: 8px 8px 8px 20px;
  border-radius: 40px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: 300ms;
}

.play-mode .play:hover{
  background: #3d3362;
}

.play-mode .play .icon{
  margin-right: 10px;
}

.search-match{
  position: fixed;
  left: 50%;
  margin-left: -160px;
  bottom: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: showSearchMatch .4s;
}

@keyframes showSearchMatch {
  0%{
    bottom: -80px;
    margin-left: -150px;
  } 100% {
    bottom: 20px;
    margin-left: -160px;
  }
}

.search-match .container{
  width: 320px;
  height: 80px;
  border-radius: 12px;
  color: #ffffff;
  text-align: center;
  background: #3d3362;
  animation: containerSearchMatch .4s;
}

@keyframes containerSearchMatch{
  0% {
    width: 300px;
    height: 60px;
  } 100% {
    width: 320px;
    height: 80px;
  }
}

.search-match .container div:nth-child(1){
  padding: 6px;
}
.search-match .container .timer{
  padding: 6px;
  font-size: x-large;
  border-radius: 12px;
  background: #674fc7;
}
</style>
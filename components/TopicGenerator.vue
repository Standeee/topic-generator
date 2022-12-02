<template>
  <div style="height: 100%">
    <div class="question">
      <h1 id="congrats" class="congrats">
        Gefeliciteerd :)
      </h1>
      <div class="images">
        <div id="card-1" class="card">
          <img class="image-1" src="https://media-cdn.tripadvisor.com/media/photo-s/1a/c9/b0/87/restaurant-de-beren.jpg">
          <h2>Een leuk en lekker etentje bij de beren!</h2>
        </div>
        <div id="card-2" class="card">
          <img class="image-2" src="https://www.escaperoomsnederland.nl/wp-content/uploads/2016/12/logo-algemeen.png">
          <h2>Een uitdagende en gezellige escape room in Hoogeveen!</h2>
        </div>
      </div>
      <div id="pageLoading" class="pageloading">
        <div class="gift">
          <div class="cap" />
          <div class="ribbon" />
          <div class="ribbon" />
        </div>
        <div class="loading">
          <div id="bar" class="bar" />
        </div>
        <h3 style="text-align: center; margin-top: 32px; width: 200px;">
          Dat is correct!<br>Jouw kadootjes worden geladen...
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      percent: 0,
      interval: ''
    }
  },
  mounted () {
    this.loading()
  },
  beforeDestroy () {
    clearInterval(this.interval)
  },
  methods: {
    loading () {
      this.interval = setInterval(function () {
        this.percent = this.percent + 0.75
        document.getElementById('bar').style.width = this.percent + '%'

        if (this.percent > 100) {
          clearInterval(this.interval)
          document.getElementById('pageLoading').className += ' complete'
          document.getElementById('card-1').style.width = '100%'
          document.getElementById('congrats').style.width = '100%'
          document.getElementById('card-2').style.width = '100%'
          document.getElementById('card-1').style.opacity = '1'
          document.getElementById('congrats').style.opacity = '1'
          document.getElementById('card-2').style.opacity = '1'
        }
      }.bind(this), 30)
    }
  }
}
</script>

<style lang="css">

body, html, #__nuxt, #__layout {
  height: 100%;
  overflow: hidden;
  font-family: 'Roboto';
  margin: 0;
}

.congrats {
  font-size: 28px;
  position: absolute;
  margin: 0;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 12px;
  background-color: red;
  color: white;
  padding: 8px;
  width: 0%;
  opacity: 0;
  transition: all ease-in-out 0.25s;
}

.question {
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
}

.images {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-between;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  padding: 20px;
  box-sizing: border-box;
}

h2 {
  text-align: center;
}

.image-1 {
  width: 100%;
  height: calc(100% - 64px);
  object-fit: contain;
  box-sizing: border-box;
}

.image-2 {
  width: 100%;
  height: calc(100% - 52px);
  object-fit: contain;
  box-sizing: border-box;
}

.card {
  display: flex;
  align-items: center;
  flex-direction: column;
  height: 45%;
  width: 0%;
  opacity: 0;
  padding: 20px;
  box-shadow: 1px 1px 14px 6px rgba(0,0,0,0.32);
  box-sizing: border-box;
  transition: all ease-in-out 0.25s;
}

h1 {
  text-align: center;
}

.gift {
    width: 100px;
    height: 100px;
    position: relative;
    background-color: red;
    transform: translateY(120%);
    margin: auto;
    transition: 0.5s;
}

.cap {
  width: calc(100% + 20px);
  height: 15px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: green;
  transform: translate(-10px);
  transform: rotate(-60deg);
  transform-origin: left;
}

.ribbon {
  width: 100%;
  height: 10px;
  position: absolute;
  top: 50%;
  left: 0;
  z-index: 0;
  background-color: white;
  transform: translate(0, -50%);
}

.ribbon:nth-last-child(1) {
  z-index: 1;
  transform: rotate(90deg) translate(-5px, 0);
}

.pageLoading {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: #ccd5ae;
  transition: 0.5s;
  transition-delay: 0.5s;
}
.complete {
  opacity: 0;
}

.complete .gift {
  transform: scale(0.01) rotate(360deg);
}

  .gift {
    animation: bounce 0.8s infinite alternate;
    box-shadow: 1px 1px 14px 6px rgba(0,0,0,0.1);
    transform: translate(0);
  }

    .cap {
      transform: rotate(0) translate(-10px);
    }

  @keyframes bounce {
    50% {
      top: 0;
      box-shadow: 1px 1px 14px 6px rgba(0,0,0,0.1);
    }

    100% {
      top: -50px;
      box-shadow: 1px 1px 14px 6px rgba(0,0,0,0.1);
    }
  }

  .loading {
    width: 200px;
    height: 8px;
    margin-top: 80px;
    border-radius: 4px;
    background-color: #fff;
    overflow: hidden;
    box-shadow: 1px 1px 14px 6px rgba(0,0,0,0.1);
  }
  .bar {
      width: 0%;
      height: 100%;
      background-color: red;
    }
</style>

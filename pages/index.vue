<template>
  <div class="Container">
    <!-- last card -->
    <div class="Picture">
      <img class="Picture-img" src="https://media-cdn.tripadvisor.com/media/photo-s/27/7e/23/78/brass-boer-curacao.jpg" alt="">
      <div class="Picture-note">
        <span>Brass Boer 🤗</span>
      </div>
    </div>
    <!-- other cards -->
    <div class="Picture">
      <img class="Picture-img" src="../static/Screenshot 2023-06-09 210454.png" alt="">
      <div class="Picture-note">
        <span>Lekker eten bij 🍴</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="../static/IMG_20210728_185134.jpg" alt="">
      <div class="Picture-note">
        <span>Dan gaan we met z'n tweeën 💝</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="../static/IMG_20190815_164943.jpg" alt="">
      <div class="Picture-note">
        <span>En als we weer terug zijn in Curacao 🛬</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="../static/IMG_20210728_184938.jpg" alt="">
      <div class="Picture-note">
        <span>Met mooi weer 😎</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="../static/IMG_0148.jpg" alt="">
      <div class="Picture-note">
        <span>En zondag vieren we vieren het lekker met z'n allen</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="../static/IMG_20210715_183050.jpg" alt="">
      <div class="Picture-note">
        <span>We zullen op je proosten</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="../static/IMG_1580.jpg" alt="">
      <div class="Picture-note">
        <span>Maak er vandaag een gezellige dag van</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="https://lordicon.com/icons/wired/flat/1103-confetti.gif" alt="">
      <div class="Picture-note">
        <span>Van harte gefeliciteerd!</span>
      </div>
    </div>
    <div class="Picture">
      <img class="Picture-img" src="https://media.istockphoto.com/id/1128262881/vector/decorative-black-gift-box-with-golden-bow-isolated-on-white.jpg?s=612x612&w=0&k=20&c=Gun3eVyEhbfOTJtGvANml18ARBAqWD8UObeallkbltc=" alt="">
      <div class="Picture-note">
        <span>Sleep de kaartjes weg 😁</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  mounted () {
    const pictures = document.querySelectorAll('.Picture')
    let previousTouch

    function updateElementPosition (element, event) {
      let movementX, movementY

      if (event.type === 'touchmove') {
        const touch = event.touches[0]
        movementX = previousTouch ? touch.clientX - previousTouch.clientX : 0
        movementY = previousTouch ? touch.clientY - previousTouch.clientY : 0
        previousTouch = touch
      } else {
        movementX = event.movementX
        movementY = event.movementY
      }

      const elementY = parseInt(element.style.top || 0) + movementY
      const elementX = parseInt(element.style.left || 0) + movementX

      element.style.top = elementY + 'px'
      element.style.left = elementX + 'px'
    }

    function startDrag (element, event) {
      const updateFunction = event => updateElementPosition(element, event)
      const stopFunction = () => stopDrag({ update: updateFunction, stop: stopFunction })
      document.addEventListener('mousemove', updateFunction)
      document.addEventListener('touchmove', updateFunction)
      document.addEventListener('mouseup', stopFunction)
      document.addEventListener('touchend', stopFunction)
    }

    function stopDrag (functions) {
      previousTouch = undefined
      document.removeEventListener('mousemove', functions.update)
      document.removeEventListener('touchmove', functions.update)
      document.removeEventListener('mouseup', functions.stop)
      document.removeEventListener('touchend', functions.stop)
    }

    pictures.forEach((picture) => {
      const range = 100
      const randomX = Math.random() * (range * 2) - range + (window.innerWidth / 2)
      const randomY = Math.random() * (range * 2) - range + (window.innerHeight / 2)
      const randomRotate = Math.random() * (range / 2) - range / 4
      const startFunction = event => startDrag(picture, event)
      picture.style.top = `${randomY}px`
      picture.style.left = `${randomX}px`
      picture.style.transform = `translate(-50%, -50%) rotate(${randomRotate}deg)`
      picture.addEventListener('mousedown', startFunction)
      picture.addEventListener('touchstart', startFunction)
    })
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Caveat");

body, html, #__nuxt, #__layout {
  margin: 0;
  font-family: 'Caveat', serif;
  overflow: hidden;
}

.Container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 100dvh;
  width: 100vw;
  overflow: hidden;
}

.Picture {
  display: inline-block;
  position: absolute;
  top: 0;
  left: 0;
  border: 5px solid #fff;
  border-radius: 3px;
  background: #fff;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
  transform: translate(-50%, -50%);
  user-select: none;
  cursor: pointer;
}

.Picture-img {
  display: block;
  width: 300px;
  height: 300px;
  object-fit: contain;
  pointer-events: none;
}

.Picture-note {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 300px;
  height: 70px;
  padding: 12px 24px;
  font-size: 1.5rem;
  text-align: center;
}

.Network {
  display: inline-block;
  padding: 0 5px;
}

.Network img {
  width: 1.5rem;
  aspect-ratio: 1 / 1;
  vertical-align: middle;
}

/* --------------------- */
/* Other styles          */
/* --------------------- */

* {
  box-sizing: border-box;
}
</style>

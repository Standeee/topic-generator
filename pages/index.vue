<template>
  <div class="wallet">
    <div class="title">
      <h1>Moederdag Cadeau</h1>
      <p>J. Koster</p>
    </div>
    <div class="card">
      <div class="logo" :class="{ logoDisabled: first}">
        <img src="https://images.unsplash.com/photo-1638153534717-fb17b6d19040?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1335&q=80" alt="">
      </div>
      <div class="info">
        <div class="qty">
          <div>IPad Pro</div>
          <div>Met Apple Pencil</div>
        </div>
        <div class="btn" :class="{ btnDisabled: first}" @click="openFirst">
          Verzilveren
        </div>
      </div>
    </div>
    <div class="card">
      <div class="logo" :class="{ logoDisabled: second}">
        <img src="https://images.unsplash.com/photo-1569629743817-70d8db6c323b?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1198&q=80" alt="">
      </div>
      <div class="info">
        <div class="qty">
          <div>Verassingsbezoek</div>
          <div>Van Niek en Stan</div>
        </div>
        <div class="btn" :class="{ btnDisabled: second}" @click="openSecond">
          Verzilveren
        </div>
      </div>
    </div>
    <div class="card">
      <div class="logo" :class="{ logoDisabled: third}">
        <img src="https://images.unsplash.com/photo-1510812431401-41d2bd2722f3?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80" alt="">
      </div>
      <div class="info">
        <div class="qty">
          <div>Wijnproeverij</div>
          <div>Met Niek en Stan</div>
        </div>
        <div class="btn" :class="{ btnDisabled: third}" @click="openThird">
          Verzilveren
        </div>
      </div>
    </div>
    <div v-if="open" class="dialog">
      <h1>{{ dialogTitle }}</h1>
      <p>{{ dialogContent }}</p>
      <span v-if="closeBtn" @click="close">x</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      dialogTitle: '🎊Gefeliciteerd🎊',
      dialogContent: 'Het is moederdag en krijgt een cadeautje van Niek en Stan. Sluit het dialoog en kies jouw cadeau!',
      open: true,
      first: false,
      second: false,
      third: false,
      sure: true,
      closeBtn: true
    }
  },
  methods: {
    close () {
      this.open = false
    },
    openFirst () {
      if (!this.first) {
        this.dialogTitle = 'Prima keuze!'
        this.dialogContent = 'Een gloed nieuwe IPad pro met Apple pencil speciaal voor jou.'
        this.closeBtn = false
        window.setTimeout(this.showMsgFirst, 3000) // Time before execution
        this.open = true
        this.first = true
        this.sure = false
      }
    },
    openSecond () {
      if (!this.second) {
        this.dialogTitle = 'Kijk is achter je...'
        this.dialogContent = ''
        this.closeBtn = false
        window.setTimeout(this.showMsgSecond, 2000) // Time before execution
        this.open = true
        this.second = true
        this.sure = false
      }
    },
    openThird () {
      if (this.sure) {
        this.sure = false
        this.dialogTitle = 'Zeker weten?'
        this.dialogContent = 'Wil je niet liever één van de andere cadeautjes?'
        this.open = true
      } else if (!this.third) {
        this.dialogTitle = 'Wow goede keuze!'
        this.dialogContent = 'Wanneer je terug bent in Nederland gaan we lekker met z\'n drieën een wijnproeverij doen. De vorige keer ging het niet door, maar nu moet het lukken toch 😋🍷!'
        this.open = true
        this.third = true
      }
    },
    showMsgSecond () {
      this.dialogContent = 'Nee sorry, helaas moeten we nog werken en studeren. Was wel heel leuk geweest. Gelukkig zien we elkaar weer snel in NL 😁'
      this.closeBtn = true
    },
    showMsgFirst () {
      this.dialogTitle = 'Oh wacht.. 😅'
      this.dialogContent = ''
      window.setTimeout(this.showMsgFirstPart2, 2500) // Time before execution
    },
    showMsgFirstPart2 () {
      this.dialogTitle = 'Oh wacht.. 😅'
      this.dialogContent = 'Dit valt wel een beetje buiten ons budget. Kan je misschien één van de andere cadeautjes kiezen 😊'
      this.closeBtn = true
    }
  }
}
</script>

<style>
body, html, #__nuxt, #__layout {
  height: 100%;
  overflow: hidden;
  font-family: 'Roboto';
  margin: 0;
}

.title h1 {
  margin: 0;
  text-align: center;
  color: white;
}

.title p {
  margin: 0;
  text-align: center;
  color: white;
  font-weight: bold;
}

.dialog {
  position: absolute;
  top: 50%;
  left: calc(50% - 20px);
  transform: translate(-50%, -50%);
  background-color: white;
  width: calc(100% - 20px);
  margin: 20px;
  padding: 20px;
  border-radius: var(--radiusCard);
  box-shadow: 0px 0px 0px 500px #00000052;
}

.dialog h1 {
  margin: 0;
  margin-bottom: 12px;
  text-align: center;
  color: black;
}

.dialog p {
  margin: 0;
  text-align: center;
  color: black;
  font-weight: bold;
}

.dialog span {
  margin: 0;
  text-align: center;
  color: white;
  background-color: var(--button);
  border: 2px solid var(--button);
  border-radius: 8px;
  width: 28px;
  height: 28px;
  font-weight: bold;
  font-size: 1.25rem;
  position: absolute;
  right: 10px;
  top: 8px;
}

.hint {
  border-radius: 4px;
  padding: 4px;
  font-weight: bold;
  text-decoration: underline;
}

.error {
  color: red;
  font-weight: 500;
  font-size: 12px;
}
.form {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
  flex-direction: column;
  padding: 12px;
  box-sizing: border-box;
}

:root {
   --radiusCard : 15px   ;
   --background : #fd8974;
   --cardColor  : #343433;
   --cardInfo   : #ecf0f1;
   --money      : #7f8c8d;
   --button     : #f03f3f;
}

@media only screen and (max-width: 280px) {
  :root {
    --background  : #e74c3c;
  }
}

*{
   box-sizing: border-box;
   font-family: 'Archivo Black', sans-serif;
}

html,
body{
   margin: 0;
   width: 100%;
   height: 100%;
   background: var(--background);
}

.wallet{
   display: flex;
   justify-content: center;
   align-items: center;
   flex-direction: column;
   gap: 20px;
   width: 100%;
   height: 100%;
   padding: 1rem;
}

.card {
   display: grid;
   grid-template-columns: auto 100px auto;
   grid-template-rows: 3fr 1fr;
   grid-template-areas:
    "  .  logo   . "
    "info info info";
   background: var(--cardColor);
   border-radius: var(--radiusCard);
   max-width: 500px;
   width: 100%;
   height: 200px;
   overflow: hidden;
   box-shadow: 0px 0px 26px rgba(0,0,0,0.1);
   transition: box-shadow .5s ease;
}

.card:hover {
  box-shadow: 13px 15px 21px rgba(0,0,0,0.1);
}

.logo {
   grid-column: 1 / 4;
   grid-row: 1;
   display: flex;
   align-items: center;
   height: 100%;
   overflow: hidden;
}

.logo img {
  width: 100%;
}

.info{
   grid-area: info;
   background: var(--cardInfo);
   display: flex;
   align-items: center;
   justify-content: space-between;
   padding: .8rem 1.5rem;
}

.btn {
   padding: .8rem 1rem;
   background: var(--button);
   border-radius: 4px;
   color: white;
   cursor: pointer;
   font-weight: bold;
}

.btnDisabled {
  background-color: gray;
}

.logoDisabled {
  filter: grayscale();
}

.qty{
   line-height:1.25rem;
}

.qty div:nth-child(1){
  font-size:1.2rem;
  font-weight: bold;
  color: var(--cardColor);
}

.qty div:nth-child(2){
  color:var(--money);
  font-weight: bold;
  font-size: 0.9rem;
}
</style>

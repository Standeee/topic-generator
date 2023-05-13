<template>
  <div class="form">
    <h2>Oh oh. Er zit een wachtwoord op de kadootjes.</h2>
    <input v-model="answer">
    <p class="error">
      {{ error }}
    </p>
    <button @click="checkAnswer">
      Controleer
    </button>
    <p>Hint: er zijn twee codes. Los eerst de kaart op.</p>
    <p class="hint" @click="(hint = 'Kijk goed naar het whatsapp bericht van Stan')">
      <small>{{ hint }}</small>
    </p>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      answer: '',
      error: ' ',
      hint: 'Klik hier om een hint voor de tweede code te openen'
    }
  },
  methods: {
    checkAnswer () {
      if (this.answer.toLowerCase().replace(/\s/g, '') === 'mashapabien' || this.answer.toLowerCase().replace(/\s/g, '') === 'mashápabien') {
        this.$router.push('/old/gifts')
      } else if (this.answer.toLowerCase().replace(/\s/g, '') === 'niekstan' || this.answer.toLowerCase().replace(/\s/g, '') === 'stanniek') {
        this.$router.push('/old/gift-niek-stan')
      } else { this.error = 'Jammer, dit is niet het goede antwoord. Probeer het opnieuw :)' }
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

button {
  border: none;
  color: white;
  border-radius: 4px;
  background-color: rgb(87, 101, 228);
  padding: 4px 8px;
  width: 100%;
  height: 32px;
  max-width: 400px;
  font-size: 16px;
  font-weight: bold;
  box-sizing: border-box;
}

input {
  width: 100%;
  max-width: 400px;
  height: 32px;
  padding: 4px 8px;
  box-sizing: border-box;
}
</style>

<template>
  <div class="demo">
    <div class="form">
      <div>
        <label for="naam">Const Naam</label>
        <input v-model="naam" placeholder="naam">
      </div>
      <div>
        <label for="vraag">Vraag</label>
        <input v-model="vraag" placeholder="vraag">
      </div>
      <div>
        <label for="weetje">Weetje</label>
        <input v-model="weetje" placeholder="weetje">
      </div>
      <div>
        <label for="yesPath">Yes Image Path</label>
        <input v-model="yesPath" placeholder="yesPath">
      </div>
      <div>
        <label for="yesPointer">Yes Arrow (X Y Rotation)</label>
        <input v-model="yesPointer" onClick="this.select();" placeholder="yesPointer">
      </div>
      <div>
        <label for="noPath">No Image Path</label>
        <input v-model="noPath" placeholder="noPath">
      </div>
      <div>
        <label for="noPointer">No Arrow (X Y Rotation)</label>
        <input v-model="noPointer" onClick="this.select();" placeholder="noPointer">
      </div>
      <div>
        <label for="yesValue">Yes Value</label>
        <input v-model="yesValue" onClick="this.select();" placeholder="yesValue">
      </div>
      <div>
        <label for="noValue">No Value</label>
        <input v-model="noValue" onClick="this.select();" placeholder="noValue">
      </div>
      <div>
        <label for="yesAnswer">Yes Answer</label>
        <input v-model="yesAnswer" placeholder="yesAnswer">
      </div>
      <div>
        <label for="noAnswer">No Answer</label>
        <input v-model="noAnswer" placeholder="noAnswer">
      </div>
    </div>
    <div class="uitslag">
      <pre>
<code id="code">const {{ naam }} = {
  "question": "{{ vraag }}"",
  "info": {
    "title": "Weetje",
    "segments": [{
      "text": "{{ weetje }}"
    }],
  },
  "images": {
    "yes": "{{ yesPath }}",
    {{ getPointer(yesPointer, true) }}
    "no": "{{ noPath }}"
    {{ getPointer(noPointer, false) }}
  },
  "answerRoutes": [
    {
      "title": "Ja",
      "value": {{ yesValue }},
    },
    {
      "title": "Nee",
      "value": {{ noValue }},
    }
  ],
  "yes": "{{ yesAnswer }}",
  "no": "{{ noAnswer }}",
}</code>
      </pre>
      <div class="tooltip">
        <button class="copy" @click="copy()" @mouseout="copyOut()">
          <span id="myTooltip" class="tooltiptext">Copy to clipboard</span>
          <svg
            aria-hidden="true"
            focusable="false"
            data-prefix="fas"
            data-icon="copy"
            class="svg-inline--fa fa-copy fa-w-14"
            role="img"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 448 512"
          >
            <path fill="currentColor" d="M320 448v40c0 13.255-10.745 24-24 24H24c-13.255 0-24-10.745-24-24V120c0-13.255 10.745-24 24-24h72v296c0 30.879 25.121 56 56 56h168zm0-344V0H152c-13.255 0-24 10.745-24 24v368c0 13.255 10.745 24 24 24h272c13.255 0 24-10.745 24-24V128H344c-13.2 0-24-10.8-24-24zm120.971-31.029L375.029 7.029A24 24 0 0 0 358.059 0H352v96h96v-6.059a24 24 0 0 0-7.029-16.97z" />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      naam: '',
      vraag: '',
      weetje: '',
      yesPath: '',
      yesPointer: '0 0 0',
      noPath: '',
      noPointer: '0 0 0',
      yesValue: 1,
      noValue: 3,
      yesAnswer: '',
      noAnswer: ''
    }
  },
  methods: {
    copy () {
      const code = document.getElementById('code')
      navigator.clipboard.writeText(code.innerHTML)

      const tooltip = document.getElementById('myTooltip')
      tooltip.innerHTML = 'Copied to clipboard!'
    },
    copyOut () {
      const tooltip = document.getElementById('myTooltip')
      tooltip.innerHTML = 'Copy to clipboard'
    },
    getPointer (type, yes) {
      const points = type.split(/(\s+)/).filter(function (e) {
        return e.trim().length > 0
      })

      if (yes) {
        return ('"yesPointerX": ' + points[0] + `, 
    "yesPointerY": ` + points[1] + `,
    "yesPointerRotation": ` + points[2] + ','
        )
      }

      return ('"noPointerX": ' + points[0] + `, 
    "noPointerY": ` + points[1] + `,
    "noPointerRotation": ` + points[2] + ','
      )
    }
  }
}
</script>

<style lang="css">
.demo {
  display: flex;
  font-family: sans-serif;
  border: 1px solid #eee;
  border-radius: 2px;
  padding: 20px 30px;
  margin-top: 1em;
  margin-bottom: 40px;
  flex-direction: column;
  align-items: center;
}

.form {
  display: flex;
  flex-direction: column;
  min-width: 500px;
}

.form input {
  margin: 5px 0;
  width: 500px;
}

.form div {
  display: flex;
  flex-direction: row-reverse;
  justify-content: flex-end;
  align-items: center;
}

.form div label {
  display: inline-block;
  margin-left: 24px;
  font-size: 14px;
  font-weight: bold;
}

.uitslag {
  margin-top: 24px;
  position: relative;
  height: 100%;
  min-width: 700px;
}

pre {
  margin: 0;
  padding: 13px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  background-color: rgb(236, 236, 236);
  border-radius: 12px;
}

code {
  height: 100%;
}

.copy {
  border: unset;
  background-color: black;
  color: white;
  padding: 10px;
  border-top-left-radius: 12px;
  border-bottom-right-radius: 12px;
  cursor: pointer;
}

.copy:hover {
  background-color: rgb(41, 41, 41);
}

.copy svg {
  width: 16px;
  height: 16px;
}

.tooltip {
  position: absolute;
  bottom: 0;
  right: 0;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 110px;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip .tooltiptext::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}

</style>

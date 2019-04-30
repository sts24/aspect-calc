<template>
  <div id="app">

    <header>
      <h1>Aspect Ratio Calculator for CSS</h1>
      <p>Created by <a href="https://www.smithscott.net">Scott Smith</a></p>
    </header>
    
    <section class="input-area">
      <div class="field">
        <label for="oWidth">Original Width</label>
        <input type="number" id="oWidth" v-model="dimensions.oWidth" />
      </div>

      <div class="field">
        <label for="oHeight">Original Height</label>
        <input type="number" id="oHeight" v-model="dimensions.oHeight" />
      </div>

      <div class="field">
        <label for="width">New Width</label>
        <input type="number" id="newWidth" v-model="dimensions.newWidth" />
      </div>

      <div class="field">
        <label for="newHeight">New Height</label>
        <input type="number" id="newHeight" v-model="dimensions.newHeight" />
      </div>
    </section>

    <section class="output-area">

      <div class="code-output">
        <pre v-show="dimensions.newHeight"><code>
div {

}

div::after {
  content: '';
  display: block;
  padding-bottom: {{ dimensions.newHeight }}%;
}
        </code></pre>
      </div>

      <div class="sample-box" v-bind:style="{ 'padding-bottom': dimensions.newHeight + '%' }" v-show="dimensions.newHeight"></div>

    </section>
  </div>

  

</template>

<script>
export default {
  name: 'app',
  data: function(){
    return {
      dimensions: {
        oWidth: '',
        oHeight: '',
        newWidth: '100',
        newHeight: '',
      }
    }
  },
  methods: {
    makeCalc: function(data){ 
      let aspectCalc = (data.oHeight / data.oWidth) * data.newWidth;
      this.dimensions.newHeight = aspectCalc;
    }
  },
  watch: {
    dimensions: {
      deep: true,
      handler(data){
        this.makeCalc(data);
      }
    }
  }
}
</script>

<style lang="scss">

  :root {
    --blue: #102046;
    --orange: #e6621a;
    --lightgray: #ebebeb;
    --darkgray: #333;
  }

  * {
    box-sizing: border-box;
  }

  body {
    font-family: Helvetica, Arial, sans-serif;
    margin: 0;
    background-color: var(--lightgray);
    color: var(--darkgray);
    border: 1rem solid var(--orange);
    min-height: 100vh;
  }

  #app {
    padding: 2rem 0;
    margin: auto;
    max-width: 1000px;

    header {
      text-align: center;
      margin-bottom: 4rem;
    }
  }

  h1 {
    color: var(--blue);
  }

  a {
    color: var(--orange);
    text-decoration: none;
    font-weight: bold;

    &:hover {
      text-decoration: underline;
    }
  }

  .input-area {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-areas:
      'oWidth newWidth'
      'oHeight newHeight';
    grid-gap: 2rem;
    justify-items: center;

    margin-bottom: 10vh;
  }

  .field:nth-child(1){ grid-area: oWidth }
  .field:nth-child(2){ grid-area: oHeight }
  .field:nth-child(3){ grid-area: newWidth }
  .field:nth-child(4){ grid-area: newHeight }

  .field {
    label {
      display: block;
      font-weight: bold;
      margin-bottom: 0.5em;
    }

    input {
      display: block;
      font-size: 2em;
      width: 5ch;
    }
  }

  .output-area {
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 2rem;
    padding: 0 1rem;

    @media (min-width: 768px){
      padding: 0;
      grid-template-columns: 2fr 1fr;
    }
  }

  .sample-box {
    background-color: var(--blue);
    width: 100%;
    height: 0;
  }

  pre {
    background-color:var(--darkgray);
    color: white;
    border-radius: 0.5em;
    margin: 0;
    padding: 1em 2em;
  }

  code {
    font-size: 1.5em;
  }

</style>

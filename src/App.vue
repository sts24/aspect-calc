<template>
  <div id="app">
    
    <section class="inputArea">
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

    <div class="sample-box" v-bind:style="{ 'padding-bottom': dimensions.newHeight + '%' }"></div>

  </div>

  

</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

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
  components: {
    HelloWorld
  },
  methods: {
    makeCalc: function(data){
      
      let aspectCalc = (data.oHeight / data.oWidth) * data.newWidth;

      console.log(aspectCalc);

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

  body {
    font-family: Helvetica, Arial, sans-serif;
    margin: 0;
  }

  #app {
    padding: 2rem;
  }

  .inputArea {
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

  .sample-box {
    background-color: darkblue;
    width: 100%;
    height: 0;
  }

</style>

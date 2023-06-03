<!-- API credit https://github.com/lukePeavey/quotable-->
<template>
  <h1>Quote generator</h1>
  <!-- Create main container for the content to be displayed -->
  <div id="app">
    <!-- Render if Quote has a value -->
    <h2 :key="loadKey" v-if="Quote">
      <!-- Display quote, break line and display author -->
      {{ "\""+Quote+"\""}}
    <br>
      {{ "- "+Author }}
    </h2>
    <!-- Create button and listen for event click, when click is sent run forceRerender function -->
    <button class="btn btn__primary btn__lg" @click="forceRerender()">Generate</button>
  </div>
  <footer>Built with Vue</footer>
</template>

<script>
//Import Axios for API handling
import axios from 'axios';

export default {
  name: 'App',
  //Change page title
  created() {
    document.title = "Random quote";
  },
  //Define variables
  data() {
    return {
      Quote: null,
      Author: null,
      loadKey: 0,
    }
  },
  methods: {
    //Functionality for the "Generate button"
    forceRerender(){
      //When "Generate" button is clicked adds 1 to loadKey which makes the element re render 
      //and a new quote is displayed
      this.loadKey += 1;
      //Gets the data to be displayed from the API and assigns the value to the variables Quote and Author
      axios
      .get('https://api.quotable.io/random')
      .then(response => (this.Quote = response.data.content, this.Author = response.data.author))
    }
  },
  //Loads data when the component has finished the initial rendering
  mounted () {
    axios
      .get('https://api.quotable.io/random')
      .then(response => (this.Quote = response.data.content, this.Author = response.data.author))
  },
}

</script>

<style>
/* Styling */
  body {
    width: 100%;
    max-width: 68rem;
    margin: 0 auto;
    font: 1.6rem/1.25 "Helvetica Neue", Helvetica, Arial, sans-serif;
    background-color: #969393;
    color: #4d4d4d;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
  }

  #app {
    background: #383737;
    margin: 2rem 0 4rem 0;
    padding: 1rem;
    padding-top: 0;
    position: relative;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
  }

  #app > * {
    max-width: 50rem;
    margin-left: auto;
    margin-right: auto;
  }

  #app > form {
    max-width: 100%;
  }

  #app h1, h2 {
    display: block;
    color: rgb(214, 214, 214);
    min-width: 100%;
    width: 100%;
    text-align: center;
    margin: 0;
    margin-bottom: 1rem;
  }

  .btn {
    padding: 0.8rem 1rem 0.7rem;
    border: 0.2rem solid #4d4d4d;
    background-color: rgb(69, 87, 107);
    color: #fff;
    cursor: pointer;
    text-transform: capitalize;
  }

  .btn:hover{
    box-shadow: 0 0 10px 0 #0c0a31 inset, 0 0 10px 4px #2f2e3b;
  }

  .btn__primary {
    color: #fff;
    background-color: #000;
  }

  footer{
    text-align: center;
    font-size: 14px;
  }  

  [class*="__lg"] {
    display: inline-block;
    width: 100%;
    font-size: 1.9rem;
  }

  [class*="__lg"]:not(:last-child) {
    margin-bottom: 1rem;
  }

  [class*="stack"] > * {
    margin-top: 0;
    margin-bottom: 0;
  }

  .stack-small > * + * {
    margin-top: 1.25rem;
  }

  .stack-large > * + * {
    margin-top: 2.5rem;
  }

  *:focus {
    outline: 3px dashed #228bec;
  }

  /* Reactivity */
  @media screen and (min-width: 620px) {
    [class*="__lg"] {
      font-size: 2.4rem;
    }
  }

  @media screen and (min-width: 550px) {
    .stack-small > * + * {
      margin-top: 1.4rem;
    }
    .stack-large > * + * {
      margin-top: 2.8rem;
    }
  }

  @media screen and (min-width: 550px) {
    #app {
      padding: 4rem;
    }
  }
</style>

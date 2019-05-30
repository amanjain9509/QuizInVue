<template>
 <div id="app" v-bind:style="{ backgroundImage: 'url(https://picsum.photos/800/800/?image=90)' }">
    <Navbar/>
    <Header
    v-bind:numCorrect="numCorrect"
    v-bind:numTotal="numTotal"
     />
     
    <b-container class="bv-example-row">
      <b-row>
          <b-col sm="6" offset="3">
            <QuestionBox
            v-if="questions.length"
            v-bind:currentQuestion="questions[index]"
            v-bind:nextClick="nextClick"
            v-bind:increment="increment"
            />
          </b-col>
        </b-row>
    </b-container>
    
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import Navbar from './components/Navbar.vue'
export default {
  name: 'app',
  components: {
    Header,
    QuestionBox,
    Navbar
  },
  data: function () {
    return {
      questions: [],
      index:0,
      numCorrect:0,
      numTotal:0
    }
  },
  methods : {
    nextClick() {
      this.index++
    },
    increment(inCorrect){
      if(inCorrect){
        this.numCorrect++
      }
      this.numTotal++
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=9&difficulty=medium&type=multiple',{
    method :'get'
    })
    .then(response => {
      return response.json()
    })
    .then(jsonData => {
      this.questions = jsonData.results
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

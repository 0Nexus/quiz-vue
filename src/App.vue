<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1> oceanus quiz app</h1>
      </div>
      <div class="step-progress" :style="{'width' : progress + '%'}"></div>
      <div class="main-quiz" v-for="(element,index) in questions.slice(a,b)" :key="index" v-show="quiz">
        <div class="box-question">
          <h2>Question{{b}}/{{questions.length}}</h2>
          <p>{{element.questions}}</p>
        </div>
        <div class="box-suggestions">
          <ul>
            <li v-for="(item,index) in element.suggestions" :key="index" :class="select ? check(item):' '" @click="selectResponse(item)">
              {{item.suggestions}}
              <div class="fas fa-check" v-if="select ? item.correct: ''"></div> 
              <div class="fas fa-times" v-if="select ? !item.correct: ''"></div>
            </li>
          </ul>
        </div>
        <div class="box-score" v-if="score_show">
          <h2>Your score is</h2>
          <h2>{{score}}/{{questions.length}}</h2>
          <div class="btn-restart">
            <button @click="restartQuiz">Restart <i class="fas fa-sync-alt"></i></button>
          </div>
        </div>
      </div>
      <div class="quiz-footer">
        <div class="box-button" v-if ="progress <100">
          <button @click="skip" :style = "!next ? 'background-color:rgb(10,128,202)' : ''">skip</button>
          <button @click="nextQuestion" :style="next ? 'background-color:rgb(10,128,202)' : ''">Next</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      questions:[
        {
          question:'whats heavier ?',
          suggestions:[
            {suggestions:'1kg of steel'},
            {suggestions:'1kg of leather',correct:true},
            {suggestions:'1kg of orange'},
            {suggestions:'1kg of air'},
          ]
        },
        {
        question:'whats the role of a node in a linked-list ?',
          suggestions:[
            {suggestions:'To store the information and the link to the next item',correct:true},
            {suggestions:'To check for the end of the list'},
            {suggestions:'Not used in a linked list'},
            {suggestions:'to check for the begining of the list'},
          ]
        },
        {
        question:'whats the name of out company ?',
          suggestions:[
            {suggestions:'netulipe'},
            {suggestions:'yassir'},
            {suggestions:'oceanus',correct:true},
            {suggestions:'gitlab'},
          ]
        },
        {
        question:'The operator AND...',
          suggestions:[
            {suggestions:'Quantifies your search'},
            {suggestions:'Expands your search',correct:true},
            {suggestions:'Restricts or limits your search'},
            {suggestions:'Redirects your search'},
          ]
        },
        {
        question:'when did "the great depression" took place in the united states?',
          suggestions:[
            {suggestions:'1929',correct:true},
            {suggestions:'1880'},
            {suggestions:'1937'},
            {suggestions:'1956'},
          ]
        },
        {
        question:'how long did hundered years war last ?',
          suggestions:[
            {suggestions:'100year'},
            {suggestions:'116year',correct:true},
            {suggestions:'104year'},
            {suggestions:'112year'},
          ]
        },

      ],

      a:0,
      b:1,
      select:false,
      score:0,
      quiz : true,
      score_show:false,
      next:false,
      progress:0
    }
  },

  methods:{
    selectResponse(e){
      this.select = true;
      this.next = true;
      if(e.correct){
        this.score++;
      }
    },
    check(status){
      if(status.correct) {
        return 'correct'
      }else{
        return 'incorrect'
      }
    },
    nextQuestion(){
      if(!this.next){
        return;
      }
        this.progress = this.progress + (100/this.questions.length);
      if(this.questions.length - 1 == this.a) {
        this.score_show = true;
        this.quiz = false;
      }else{

      this.a++;
      this.b++;
      this.select= false;
      this.next = false;
      }
    },
    skip(){
      if (this.next){
        /*console.log(this.questions.length);*/
        return;
      }
      if(this.questions.length -1 == this.a){
        this.score_show  = true;
        this.quiz = false;
        console.log(this.questions.length);
        console.log(this.a);
        console.log(this.score_show);

      }else{
        this.a++;
        this.b++;
      }
    },
    restartQuiz(){
      Object.assign(this.$data, this.$options.data());

    }


  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

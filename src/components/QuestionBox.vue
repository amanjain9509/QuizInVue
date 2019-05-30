<template>
    <div>
        <b-jumbotron>
            <template slot="lead">
            {{ currentQuestion.question }}
            </template>
            <hr class="my-4"/>
            <b-list-group>
                <b-list-group-item 
                v-for ="(answer,index) in answers" v-bind:key="index" 
                @click="selectedAnswer(index)" 
                :class="answerClass(index)">{{answer}}</b-list-group-item>
            </b-list-group>

            <b-button variant="primary" @click="submitAnswer" :disabled="selectedIndex === null || answered">
                Submit
            </b-button>
            <b-button  @click="nextClick" variant="success" href="#">
                Next
            </b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from 'lodash';

export default {

data(){
    return{
        selectedIndex: null,
        shuffledAnswer:[],
        answered: false,
        correctIndex: null
    }
    
},
props: {
    currentQuestion: Object,
    nextClick:Function,
    increment: Function
},
computed:{
    answers(){
    let answers = [...this.currentQuestion.incorrect_answers]
    answers.push(this.currentQuestion.correct_answer)
    return answers
    }
},
watch:{
    currentQuestion:{
        immediate:true,
        handler(){
            this.selectedIndex = null;
            this.shuffleAnswer()
            this.answered= false;
        }     
    }
},
methods:{
    selectedAnswer(index){
        this.selectedIndex = index;
    },
    shuffleAnswer(){
        let answers = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
        this.shuffledAnswer = _.shuffle(answers)
        this.correctIndex = this.shuffledAnswer.indexOf(this.currentQuestion.correct_answer)
    },
    submitAnswer(){
        let inCorrect= false
        if(this.selectedIndex === this.correctIndex){
            inCorrect=true;
        }
        this.answered = true;
        this.increment(inCorrect);
    },
    answerClass(index){
        let answerReturn = null;
    
        if(! this.answered && this.selectedIndex === index){
            answerReturn ='selected';
        }else if(this.answered && this.correctIndex === index){
            answerReturn ='correct';
        }else if(this.answered && this.selectedIndex === index && this.correctIndex !== index){
            answerReturn ='incorrect';
        }
    
            return answerReturn;
    }
},
mounted(){
    this.shuffleAnswer()
},

}
</script>

<style scoped>
.list-group {
    margin-bottom: 15 px;
}
.list-group-item:hover {
    background: #0001;
    cursor: pointer;
}
.btn {
        margin: 20px 5px;
}

.selected{
    background: blue;
}
.correct {
    background: lightgreen;
}
.incorrect {
    background: red;
}
div {
  background-color: lightblue;
}

</style>
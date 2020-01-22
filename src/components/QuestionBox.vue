    <template>
  <div class="hello">
 <b-jumbotron >

 

    <template slot="lead">
    {{Cquestion.question}}
    </template>

    <hr class="my-4">
<b-list-group>
  <b-list-group-item
   v-for="(answer, index) in answers" 
    :key="index"
   @click.prevent="selectAnswer(index)"
   :class="answerClass(index)">
  {{answer}}
  </b-list-group-item>
  </b-list-group>

    <b-button variant="primary"
     @click='submitAnswer'
     :disabled="selectedIndex===null ||  answered"
      >submit</b-button>
    <b-button variant="success" @click='next' href="#">next</b-button>
  </b-jumbotron>


  </div>
</template>

<script>
import _ from 'lodash'
export default {
  name: 'QuestionBox', 
  props: {
   Cquestion:Object,
   next:Function,
   increment:Function
  },
  data(){
    return{
      selectedIndex:null,
      shuffledAnswers:[],
      correctIndex:null,
      answered:false

    }
  },
  computed:{
    answers(){
     let answers=[...this.Cquestion.incorrect_answers]
      answers.push(this.Cquestion.correct_answer)
   return answers     

  }},
  watch:{
Cquestion:{
 immediate:true,
 handler(){
    this.selectedIndex=null
  this.shuffleAnswers()
  this.answered=false
 }

}
  },
  
  methods:{
    selectAnswer(index){ 
      this.selectedIndex=index
    },
    submitAnswer(){
  let isCorrect= false 
  if(this.selectedIndex ===this.correctIndex){
       isCorrect=true
  }
  this.answered=true
  this.increment(isCorrect)

    },
    shuffleAnswers(){
    let answers=[...this.Cquestion.incorrect_answers,this.Cquestion.correct_answer]
     this.shuffledAnswers=_.shuffle(answers)
     this.correctIndex = this.shuffledAnswers.indexOf(this.Cquestion.correct_answer)
  },
   answerClass(index){
  let answerClass=''
  if( !this.answered && this.selectedIndex === index){
  answerClass='selected'
  }else if(this.answered && this.correctIndex === index){
  answerClass='correct'
  }else if( this.answered &&this. selectedIndex === index && this.correctIndex !== index ){
answerClass='incorrect'
  }
  return answerClass
    }

  }
   
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list-group{
  margin-bottom: 15px
}
.list-group-item:hover{
  background: #eee;
  cursor:pointer
}
.btn{
  margin:0 5px
}
.selected{
  background-color: lightblue
}
.correct{
  background-color: lightgreen
}
.incorrect{
  background-color: red
}

</style>

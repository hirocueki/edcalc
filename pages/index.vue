<template>
  <section class="container">
    <div>
      <div class="center">
        <div id='result-box'>{{result}}</div>
        <div class='quest'>{{quest}}</div>
        <input class='answer' type="number" readonly v-model.number='ur_answer'>
        
        
      </div>
      <div class="numpad">
        <br>
        <button class='button--green' @click='contains(7)'>7</button>
        <button class='button--green' @click='contains(8)'>8</button>
        <button class='button--green' @click='contains(9)'>9</button>
        <br>
        <button class='button--green' @click='contains(4)'>4</button>
        <button class='button--green' @click='contains(5)'>5</button>
        <button class='button--green' @click='contains(6)'>6</button>
        <br>
        <button class='button--green' @click='contains(1)'>1</button>
        <button class='button--green' @click='contains(2)'>2</button>
        <button class='button--green' @click='contains(3)'>3</button>
        <br>
        <button class='button--green' @click='contains(0)'>0</button>
        <button class='button--green' @click='clear'>AC</button>
        <button class='button--green' @click='revert'>-/+</button>
        
      </div>
      <div>
        <button class='button-answer button--green' @click='calc'>こたえる！</button>
      </div>
      <br>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      quest: '',
      answer: 0,
      ur_answer: 0,
      result: '',
      difficult: 0
    }
  },
  computed: {
    
  },
  created: function () {
    this.build_quest()
  },
  methods: {
    revert: function () {
      this.ur_answer = this.ur_answer*-1+'' 
    },
    clear: function () {
      this.ur_answer = ''
    },
    contains: function (s) {
      this.ur_answer += s 
    },
    build_quest: function () {
      var l = Math.floor( Math.random() * 100 );
      var r = Math.floor( Math.random() * 100 );
      var is_plus = Math.floor( Math.random() * 9 ) %2 ==0;

      if(is_plus){
        this.quest = l+'+'+r
        this.answer = l+r
      }
      else{
        this.quest = l+'-'+r
        this.answer = l-r
      }
      this.ur_answer = ''
    },
    focues_in: function (selector) {
      var el = document.querySelector(selector)
      el.focus()
    },
    is_collect: function () {
      return this.ur_answer == this.answer
    },
    calc () {
      if (this.is_collect()){
        this.result = '正解！'
        this.build_quest()
        this.focues_in('#answer')
        return
      } 
      this.result = 'ちがうよ！'
      this.focues_in('#answer')
    }
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.button-answer{
  width:15rem;
  height: 3rem;
}
.numpad > button{
  width:5rem;
  height: 4rem;
}
.quest {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.answer {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
  text-align: center;
}

.links {
  padding-top: 15px;
}
</style>

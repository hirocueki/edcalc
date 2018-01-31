<template>
  <section class="container">
    <div>
      <div class="center">
        <h1 id='result-box'>{{result}}</h1>
        <h1 class='quest'>{{quest}}</h1>
        <input class='answer' type="number" v-model='ur_answer' id="answer">
      </div>
      <div>
        <button class='button--green' @click='calc'>こたえる！</button>
      </div>
      <br>
      <div>
        <button class='button--green' @click='build_quest'>つぎの問題</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      quest: '',
      answer: 0,
      ur_answer: '',
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

    build_quest: function () {
      var l = Math.floor( Math.random() * 100 );
      var r = Math.floor( Math.random() * 100 );
      this.quest = l+'+'+r
      this.answer = l+r
    },
    focues_in: function (selector) {
      document.querySelector(selector).focus()
    },
    is_collect: function () {
      console.log(this.ur_answer )
      console.log( this.answer)
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

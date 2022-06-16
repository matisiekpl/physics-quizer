<template>
  <div class="hello">
    <h2>{{ question['question'] }}</h2>
    <p style="font-size: 26px">
      <input type="checkbox" id="answer_a" name="answer_a" v-model="answer_a_selected">
      <label for="answer_a">{{ question['answer_a'] }}
        <span class="green" v-if="checking&&answer_a_correct">Dobrze</span>
        <span class="red"
              v-if="checking&&!answer_a_correct">Źle</span>
      </label><br>

      <input type="checkbox" id="answer_b" name="answer_b" v-model="answer_b_selected">
      <label for="answer_b">{{ question['answer_b'] }}
        <span class="green" v-if="checking&&answer_b_correct">Dobrze</span>
        <span class="red"
              v-if="checking&&!answer_b_correct">Źle</span></label><br>

      <input type="checkbox" id="answer_c" name="answer_c" v-model="answer_c_selected">
      <label for="answer_c">{{ question['answer_c'] }} <span class="green"
                                                             v-if="checking&&answer_c_correct">Dobrze</span>
        <span class="red"
              v-if="checking&&!answer_c_correct">Źle</span></label><br>

      <input type="checkbox" id="answer_d" name="answer_d" v-model="answer_d_selected">
      <label for="answer_d">{{ question['answer_d'] }}
        <span class="green" v-if="checking&&answer_d_correct">Dobrze</span>
        <span class="red"
              v-if="checking&&!answer_d_correct">Źle</span></label><br>

    </p>

    <h1 style="color: green" v-if="answer_a_correct&&answer_b_correct&&answer_c_correct&&answer_d_correct">
      Gratulacje</h1>

    <button @click="check" style="font-size: 26px; margin-right: 12px;">Sprawdź</button>
    <button @click="next" style="font-size: 26px;">Losuj</button>
  </div>
</template>

<script>
const questions = require('../assets/questions.json');

export default {
  name: 'HelloWorld',
  data() {
    return {
      question: {},
      answer_a_selected: false,
      answer_b_selected: false,
      answer_c_selected: false,
      answer_d_selected: false,
      answer_a_correct: false,
      answer_b_correct: false,
      answer_c_correct: false,
      answer_d_correct: false,
      checking: false,
    };
  },
  mounted() {
    this.question = questions[Math.floor(Math.random() * questions.length)];
  },
  methods: {
    check() {
      this.answer_a_correct = this.answer_a_selected === this.question['answer_a_correct'];
      this.answer_b_correct = this.answer_b_selected === this.question['answer_b_correct'];
      this.answer_c_correct = this.answer_c_selected === this.question['answer_c_correct'];
      this.answer_d_correct = this.answer_d_selected === this.question['answer_d_correct'];
      this.checking = true;
    }, next() {
      this.answer_a_correct = false;
      this.answer_b_correct = false;
      this.answer_c_correct = false;
      this.answer_d_correct = false;
      this.answer_a_selected = false;
      this.answer_b_selected = false;
      this.answer_c_selected = false;
      this.answer_d_selected = false;
      this.checking = false;
      this.question = questions[Math.floor(Math.random() * questions.length)];
    }
  }
}
</script>

<style>
input[type=checkbox] {
  transform: scale(1.5);
  margin-right: 12px;
}

.green {
  color: green;
}

.red {
  color: red;
}
</style>

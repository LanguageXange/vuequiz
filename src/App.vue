<template>
  <div class="ctr">
    <question
      v-if="questionAnswered < questions.length"
      :questions="questions"
      :currentQ="questionAnswered"
      @question-answer="questionAnswer"
    ></question>
    <result v-else :totalCorrect="totalCorrect" :results="results"></result>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionAnswered == questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Question from './components/Question.vue'
import Result from './components/Result.vue'

export default {
  name: 'App',
  components: {
    Question,
    Result
  },
  methods: {
    questionAnswer(isCorrect) {
      if (isCorrect) this.totalCorrect++
      this.questionAnswered++ // proceed to next question
    },
    reset() {
      this.questionAnswered = 0
      this.totalCorrect = 0
    }
  },
  data() {
    return {
      questionAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: 'What is 2 + 2?',
          answers: [
            {
              text: '4',
              is_correct: true
            },
            {
              text: '3',
              is_correct: false
            },
            {
              text: 'Fish',
              is_correct: false
            },
            {
              text: '5',
              is_correct: false
            }
          ]
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: '5',
              is_correct: false
            },
            {
              text: '7',
              is_correct: false
            },
            {
              text: '6',
              is_correct: true
            },
            {
              text: '12',
              is_correct: false
            }
          ]
        },
        {
          q: 'Find the missing letter: C_ke',
          answers: [
            {
              text: 'e',
              is_correct: false
            },
            {
              text: 'a',
              is_correct: true
            },
            {
              text: 'i',
              is_correct: false
            }
          ]
        }
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: 'Try again!',
          desc: 'Come back later and give it another try!'
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: 'Studying has definitely paid off for you!'
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped></style>

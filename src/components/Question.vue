<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${(currentQ / questions.length) * 100}%` }"></div>
      <div class="status">{{ currentQ }} out of {{ questions.length }} questions answered</div>
    </div>

    <transition-group name="fade" mode="out-in">
      <div
        v-for="(question, index) in questions"
        class="single-question"
        :key="question.q"
        v-show="index == currentQ"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers" v-for="answer in question.answers" :key="answer.text">
          <div class="answer" @click.prevent="selectAnswer(answer.is_correct)">
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ['questions', 'currentQ'],
  emits: ['question-answer'],
  methods: {
    selectAnswer(isCorrect) {
      this.$emit('question-answer', isCorrect)
    }
  }
}
</script>

<style lang="scss" scoped></style>

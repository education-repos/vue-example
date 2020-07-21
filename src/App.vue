<template>
  <div id="app">
    <Header />
    <QuestionBox
      v-if="questions.length"
      :currentQuestion="questions[index]"
      :next="next"
    />
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import QuestionBox from "@/components/QuestionBox";

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0
    }
  },
  methods: {
    next: function() {
      this.index++
    }
  },
  mounted() {
    fetch('https://opentdb.com/api.php?amount=10&category=9&difficulty=hard&type=multiple', {
      method: 'get'
    })
      .then((response) => {
        return response.json()
      })
      .then((jsonData) => {
        this.questions = jsonData.results
      })
  }
}
</script>

<style>

</style>

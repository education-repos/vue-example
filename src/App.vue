<template>
  <div id="app">
    <Header />
    <QuestionBox
      :currentQuestion="questions[index]"
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

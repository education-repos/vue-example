<template>
  <div id="app">
    <Header />
    <QuestionBox />
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
  }
}
</script>

<style>

</style>

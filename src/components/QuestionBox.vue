<template>
    <b-container class="question-box-container">
        <b-row>
            <b-col offset="3" sm="6">
                <b-jumbotron>
                    <template v-slot:lead>
                        {{ currentQuestion.question }}
                    </template>

                    <hr class="my-4">

                    <b-list-group>
                        <b-list-group-item
                                :class="answerClass(index)"
                                :key="index"
                                @click="selectAnswer(index)"
                                v-for="(answer, index) in answers"
                        >
                            {{ answer }}
                        </b-list-group-item>
                    </b-list-group>

                    <hr class="my-4">

                    <b-button
                            :disabled="selectedIndex === null || isAnswered"
                            @click="submitAnswer"
                            variant="primary"
                    >
                        Submit
                    </b-button>
                    <b-button
                            :disabled="!isAnswered"
                            @click="next"
                            variant="success"
                    >
                        Next
                    </b-button>
                </b-jumbotron>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
    import _ from 'lodash'

    export default {
        name: "QuestionBox",
        props: {
            currentQuestion: Object,
            next: Function,
            increment: Function
        },
        data() {
            return {
                selectedIndex: null,
                correctIndex: null,
                shuffledAnswers: [],
                isAnswered: false
            }
        },
        computed: {
            answers() {
                let answers = [...this.currentQuestion.incorrect_answers]
                answers.push(this.currentQuestion.correct_answer)
                return answers
            }
        },
        watch: {
            currentQuestion: {
                immediate: true,
                handler() {
                    this.selectedIndex = null
                    this.isAnswered = false
                    this.shuffleAnswers()
                }
            }
        },
        methods: {
            selectAnswer(index) {
                this.selectedIndex = index
            },
            shuffleAnswers() {
                let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
                this.shuffledAnswers = _.shuffle(answers)
                this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
            },
            submitAnswer() {
                let isCorrect = false
                if (this.selectedIndex === this.correctIndex) {
                    isCorrect = true
                }
                this.increment(isCorrect)
                this.isAnswered = true
            },
            answerClass(index) {
                let answerClass = ''
                if (!this.isAnswered && this.selectedIndex === index) {
                    answerClass = 'selected'
                } else if (this.isAnswered && this.correctIndex === index) {
                    answerClass = 'correct'
                } else if (this.isAnswered && this.selectedIndex === index && this.correctIndex !== index) {
                    answerClass = 'incorrect'
                }
                return answerClass
            }
        }
    }
</script>

<style scoped>
    .jumbotron {
        padding: 2rem;
    }

    .btn {
        margin-right: 1rem;
    }

    .list-group-item {
        transition: .1s all;
    }

    .list-group-item:hover {
        cursor: pointer;
        background: lightslategray;
        color: white;
    }

    .selected {
        background: lightblue;
    }

    .correct {
        background: lightgreen;
        color: white;
    }

    .incorrect {
        background: lightcoral;
        color: white;
    }
</style>

<template>
    <b-container class="question-box-container">
        <b-row>
            <b-col sm="6" offset="3">
                <b-jumbotron>
                    <template v-slot:lead>
                        {{ currentQuestion.question }}
                    </template>

                    <hr class="my-4">

                    <b-list-group>
                        <b-list-group-item
                            v-for="(answer, index) in answers"
                            :key="index"
                            @click="selectAnswer(index)"
                            :class="[selectedIndex === index ? 'selected' : '']"
                        >
                            {{ answer }}
                        </b-list-group-item>
                    </b-list-group>

                    <hr class="my-4">

                    <b-button variant="primary">Submit</b-button>
                    <b-button @click="next" variant="success">Next</b-button>
                </b-jumbotron>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
    export default {
        name: "QuestionBox",
        props: {
            currentQuestion: Object,
            next: Function
        },
        data() {
            return {
                selectedIndex: null
            }
        },
        methods: {
            selectAnswer(index) {
                this.selectedIndex = index
            }
        },
        computed: {
            answers() {
                let answers = [...this.currentQuestion.incorrect_answers]
                answers.push(this.currentQuestion.correct_answer)
                return answers
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

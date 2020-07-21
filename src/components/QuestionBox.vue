<template>
    <b-container class="question-box-container">
        <b-row>
            <b-col sm="6" offset="3">
                <b-jumbotron>
                    <template v-slot:lead>
                        Question text here?
                    </template>

                    <hr class="my-4">

                    <p>
                        List of answers
                    </p>

                    <b-button variant="primary">Submit</b-button>
                    <b-button variant="success">Next</b-button>
                </b-jumbotron>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
    export default {
        name: "QuestionBox"
    }
</script>

<style scoped>

</style>

<script setup>
    import Question from '../components/Question.vue';
    import QuizHeader from '../components/QuizHeader.vue';
    import Result from '../components/Result.vue';
    import {useRoute} from 'vue-router';
    import {ref, watch, computed} from 'vue';   
    import quizes from '../data/quizes.json';

    const route                     = useRoute();
    const quizId                    = parseInt(route.params.id);
    const quiz                      = quizes.find(q => q.id === quizId);
    const currentQusetionIndex      = ref(0);
    const numberOfCorrectAnswers    = ref(0);
    const showResults               = ref(false);
    const questionStatus            = computed( () =>  `${currentQusetionIndex.value}/${quiz.questions.length}`);
    const barPercentage             = computed( () => `${currentQusetionIndex.value/quiz.questions.length * 100}%`);

    const onOptionSelected          = (isCorrect) => {
        if(isCorrect){
            numberOfCorrectAnswers.value++;
        }

        if(quiz.questions.length -1 === currentQusetionIndex.value){
            showResults.value = true;
        }

        currentQusetionIndex.value++;
    }
    
</script> 

<template>
    <div>
        <QuizHeader 
            :questionStatus = "questionStatus" 
            :barPercentage  = "barPercentage" />
        <div>
            <Question 
                v-if="!showResults"
                :question = "quiz.questions[currentQusetionIndex]"  
                @selectOption = "onOptionSelected" />
            <Result 
                v-else 
                :quizQuestionLength = "quiz.questions.length" 
                :numberOfCorrectAnswers = "numberOfCorrectAnswers" />
        </div>
    </div>
</template>

<style scoped>
  
</style>
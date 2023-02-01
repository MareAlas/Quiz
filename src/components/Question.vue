<script setup>
    import {defineProps, defineEmits} from 'vue';

    const emit                  = defineEmits('selectOption');
    const { question }          = defineProps(['question']);
    const emitSelectedOption    = (isCorrect) => {
        emit('selectOption', isCorrect)
    }
</script>

<template>
  <div class="question-countainer">
                <h1 class="question">
                    {{ question.text }}
                </h1>
            </div>
            <div class="options-countainer">
               <div v-for="option in question.options" 
                        :key="option.id" 
                        class="option"
                        @click="emitSelectedOption(option.isCorrect)">
                   <p class="option-label">{{ option.label }}</p>
                   <div class="option-value">{{ option.text }}</div>
               </div>
            </div>
</template>

<style scoped>
       .question-countainer{
        margin-top: 20px;
    }
    .question{
        font-weight: 40px;
        margin-bottom: 20px;
    }
    .options-countainer{

    }
    .option{
        display: flex;
        margin-bottom: 20px;
        cursor: pointer;
    }
    .option-label{
        background-color: bisque;
        width: 50px;
        height: 50px;
        font-size: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .option-value{
        background-color: rgb(244,239,239);
        width: 100%;
        font-size: 30px;
        padding: 0 20px;
    }
</style>
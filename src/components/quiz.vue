<template>
  
  <div class="container mt-5">
    <div v-if="quiz">
      <h1 class="text-center mb-4">{{ quiz.title }}</h1>

      <div v-if="quiz.questions" class="mb-4">
        <Progress :max="quiz.questions.length" :current="current + 1" />
      </div>

      <Transition name="fade" mode="out-in">
        <div class="ombre" v-if="etape === 'question' && task" :key="current">
          <Question :task="task" @answer="addAnswer" />
        </div>
      </Transition>
    </div>

    <div v-if="etape === 'result'" class="results-container">
      <h2>🎯 Résultats</h2>
      <div class="score-display">
        <span class="score-value">{{ note }}</span>
        <span class="score-total">/ {{ quiz.questions.length }}</span>
      </div>
      <div class="score-percentage">
        {{ Math.round((note / quiz.questions.length) * 100) }}% de réussite
      </div>

      <div v-if="note >= quiz.minimum_score" class="alert alert-success">
        🎉 {{ quiz.success_message }}
      </div>
      <div v-else class="alert alert-danger">
        😔 {{ quiz.failure_message }}
      </div>

      <div class="detailed-results">
        <h3>Détails des réponses</h3>
        <div 
          v-for="(question, index) in quiz.questions" 
          :key="index"
          class="result-item"
        >
          <div class="result-header">
            <span class="result-icon">
              {{ answers[index] === question.correct_answer ? '✅' : '❌' }}
            </span>
            <span class="result-question">{{ question.question }}</span>
          </div>
          <div class="result-details">
            <div v-if="answers[index] !== question.correct_answer && answers[index] !== null" class="your-answer">
              Votre réponse : <strong>{{ answers[index] }}</strong>
            </div>
            <div class="correct-answer">
              Bonne réponse : <strong>{{ question.correct_answer }}</strong>
            </div>
          </div>
        </div>
      </div>

      <button class="btn restart-btn" @click="restartQuiz">
        🔄 Recommencer le quiz
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Progress from './progress.vue';
import Question from './question.vue';

const props = defineProps({
  quiz: Object
});

const etape = ref('question');
const answers = ref([]);

if (props.quiz && props.quiz.questions) {
  answers.value = props.quiz.questions.map(() => null);
}

const current = ref(0);

const task = computed(() =>
  props.quiz && props.quiz.questions
    ? props.quiz.questions[current.value]
    : null
);

const note = computed(() => {
  let total = 0;
  for (let i = 0; i < answers.value.length; i++) {
    if (
      answers.value[i] === props.quiz.questions[i].correct_answer
    ) {
      total++;
    }
  }
  return total;
});

const addAnswer = (answer) => {
  answers.value[current.value] = answer;
  if (current.value === props.quiz.questions.length - 1) {
    etape.value = 'result';
  } else {
    current.value++;
  }
};

const restartQuiz = () => {
  current.value = 0;
  answers.value = props.quiz.questions.map(() => null);
  etape.value = 'question';
};
</script>
<style scoped>
* {
  font-family: 'Montserrat', sans-serif;
  box-sizing: border-box;
}



.container {
  max-width: 700px;
  margin: 3rem auto;
  padding: 2rem;
  border-radius: 16px;
  background: #ffffff;
  border: solid 1px #000000;
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.434), 0 8px 24px rgba(0, 0, 0, 0.12);
  transition: all 0.3s ease-in-out;
}

h1 {
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 1.5rem;
  color: #111;
}

h2 {
  font-size: 1.4rem;
  font-weight: 600;
  text-align: center;
  margin-bottom: 1rem;
  color: #333;
}

p {
  font-size: 1rem;
  text-align: center;
  color: #444;
}

.card {
  background: #fdfdfd;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.05), 0 6px 16px rgba(0, 0, 0, 0.06);
  transition: box-shadow 0.2s ease;
}

.card:hover {
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.08), 0 8px 20px rgba(0, 0, 0, 0.08);
}

.question-title {
  font-weight: 600;
  font-size: 1.1rem;
  margin-bottom: 1rem;
  color: #222;
}

.choices {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.choice {
  display: flex;
  align-items: center;
  padding: 0.75rem 1rem;
  border: 1px solid #dcdcdc;
  border-radius: 10px;
  background: #fff;
  cursor: pointer;
  transition: background 0.2s ease, border 0.2s ease;
}

.choice:hover {
  background: #f1eefc;
  border-color: #b9aef9;
}

input[type="radio"] {
  margin-right: 0.75rem;
  accent-color: #8e80ff; /* Mauve clair */
}

.btn {
  display: inline-block;
  background: #8e80ff; /* Mauve */
  color: #ffffff;
  padding: 0.6rem 1.4rem;
  border: none;
  border-radius: 10px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s ease;
}

.btn:hover {
  background: #7b6ee0;
}

.progress-container {
  width: 100%;
  background: #e3e3e3;
  border-radius: 8px;
  overflow: hidden;
  height: 10px;
  margin-bottom: 1.5rem;
}

.progress-bar {
  height: 10px;
  background: #8e80ff;
  transition: width 0.3s ease;
}

.alert-success {
  background: #f0fdf9;
  color: #14866d;
  padding: 1rem;
  border-radius: 10px;
  border: 1px solid #b6e8d8;
  margin-top: 1rem;
}

.alert-danger {
  background: #fff2f2;
  color: #c0392b;
  padding: 1rem;
  border-radius: 10px;
  border: 1px solid #f5bcbc;
  margin-top: 1rem;
}

.results-container {
  text-align: center;
  margin-top: 2rem;
}

.score-display {
  margin: 1.5rem 0;
}

.score-value {
  font-size: 4rem;
  font-weight: 700;
  color: #8e80ff;
}

.score-total {
  font-size: 2rem;
  color: #666;
  margin-left: 0.5rem;
}

.score-percentage {
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 1.5rem;
}

.detailed-results {
  margin: 2rem 0;
  text-align: left;
}

.detailed-results h3 {
  font-size: 1.3rem;
  color: #333;
  margin-bottom: 1rem;
  text-align: center;
}

.result-item {
  background: #f9f9f9;
  border: 1px solid #e0e0e0;
  border-radius: 10px;
  padding: 1rem;
  margin-bottom: 1rem;
  transition: all 0.2s ease;
}

.result-item:hover {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.result-header {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  margin-bottom: 0.5rem;
}

.result-icon {
  font-size: 1.5rem;
  flex-shrink: 0;
}

.result-question {
  font-weight: 600;
  color: #333;
  flex: 1;
}

.result-details {
  margin-left: 2.25rem;
  font-size: 0.95rem;
}

.your-answer {
  color: #c0392b;
  margin-bottom: 0.25rem;
}

.correct-answer {
  color: #14866d;
}

.restart-btn {
  margin-top: 1.5rem;
  font-size: 1.1rem;
  padding: 0.8rem 2rem;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateX(30px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

</style>

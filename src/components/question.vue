<template>
  <div class="quiz-card">
    <div class="quiz-question-title">
      {{ task.question }}
    </div>

    <ul class="quiz-choices">
      <li
        v-for="(choice, index) in task.choices"
        :key="choice"
        class="quiz-choice-item"
        :style="{ animationDelay: `${index * 0.1}s` }"
      >
        <label 
          class="quiz-choice"
          :class="{ 'selected': selected === choice }"
        >
          <input
            type="radio"
            name="answer"
            :value="choice"
            v-model="selected"
            :aria-label="choice"
          />
          <span class="choice-text">{{ choice }}</span>
        </label>
      </li>
    </ul>

    <button
      class="quiz-btn"
      @click="validate"
      :disabled="!selected"
      :aria-label="selected ? 'Valider la réponse' : 'Sélectionnez une réponse'"
    >
      {{ selected ? '✓ Valider' : 'Sélectionnez une réponse' }}
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  task: Object,
});
const emit = defineEmits(['answer']);
const selected = ref('');

const validate = () => {
  emit('answer', selected.value);
};

</script>

<style scoped>
.quiz-card {
  border: 1px solid #868585;
  background-color: #f1e6e6;
  color: #000000;
  padding: 2rem;
  border-radius: 1rem;
  max-width: 600px;
  margin: 2rem auto;
  animation: slideIn 0.4s ease-out;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.quiz-question-title {
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  font-weight: bold;
  animation: fadeIn 0.6s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.quiz-choices {
  list-style: none;
  padding: 0;
  margin-bottom: 2rem;
}

.quiz-choice-item {
  margin-bottom: 0.75rem;
  animation: slideInChoice 0.4s ease-out both;
}

@keyframes slideInChoice {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.quiz-choice {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 1.1rem;
  cursor: pointer;
  padding: 0.75rem;
  border-radius: 8px;
  transition: all 0.2s ease;
  background: rgba(255, 255, 255, 0.3);
}

.quiz-choice:hover {
  background: rgba(255, 255, 255, 0.6);
  transform: translateX(5px);
}

.quiz-choice.selected {
  background: rgba(142, 128, 255, 0.2);
  border: 2px solid #8e80ff;
  padding: calc(0.75rem - 2px);
}

.choice-text {
  flex: 1;
}

input[type="radio"] {
  cursor: pointer;
  width: 20px;
  height: 20px;
  accent-color: #8e80ff;
}

.quiz-btn {
  background-color: #7f7191;
  color: white;
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1.05rem;
  font-weight: 600;
  transition: all 0.3s ease;
  width: 100%;
  max-width: 300px;
  margin: 0 auto;
  display: block;
}

.quiz-btn:hover:enabled {
  background-color: #000000;
  transform: scale(1.05);
  color: #ffffff;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.quiz-btn:disabled {
  background-color: #a09999;
  cursor: not-allowed;
  opacity: 0.6;
}

.quiz-btn:active:enabled {
  transform: scale(0.98);
}
</style>

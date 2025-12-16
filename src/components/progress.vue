<template>
    <div class="progress-wrapper">
        <div class="progress-text">
            Question <strong>{{ current }}</strong> sur <strong>{{ max }}</strong>
        </div>
        <div class="progress-container">
            <div 
                class="progress-bar" 
                :style="{ width: progressPercentage + '%' }"
                role="progressbar"
                :aria-valuenow="current"
                :aria-valuemin="0"
                :aria-valuemax="max"
            >
            </div>
        </div>
    </div>
</template>
<script setup>
import { computed } from 'vue';

const props = defineProps({
    max: Number,
    current: Number
});

const progressPercentage = computed(() => {
    return props.max > 0 ? (props.current / props.max) * 100 : 0;
});

</script>
<style scoped>
.progress-wrapper {
    margin-bottom: 2rem;
}

.progress-text {
    text-align: center;
    font-size: 1rem;
    color: #555;
    margin-bottom: 0.75rem;
}

.progress-container {
    width: 100%;
    height: 12px;
    background: #e3e3e3;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
}

.progress-bar {
    height: 100%;
    background: linear-gradient(90deg, #8e80ff 0%, #b9aef9 100%);
    transition: width 0.4s ease;
    border-radius: 10px;
}
</style>
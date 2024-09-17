<template>
    <h1 :class="{ 'fade-out': isFadingOut }">{{ curlyHello }} 🙂</h1>
</template>

<script>
import { ref, computed, onMounted } from 'vue';

export default {
  setup() {
    const helloTranslations = ref([
      'Hello', // English
      'Dumela' // Setswana
    ]);

    const currentTranslationIndex = ref(0);
    const isFadingOut = ref(false);

    const curlyHello = computed(() => {
      return '{' + helloTranslations.value[currentTranslationIndex.value] + '}';
    });

    function updateTranslation() {
      isFadingOut.value = true;
      setTimeout(() => {
        currentTranslationIndex.value = (currentTranslationIndex.value + 1) % helloTranslations.value.length;
        isFadingOut.value = false;
      }, 500);
      setTimeout(() => {
        updateTranslation();
      }, 7000);
    }

    onMounted(() => {
      updateTranslation();
    });

    return {
      curlyHello,
      isFadingOut,
    };
  }
}
</script>

<style>
h1 {
  transition: opacity 0.5s;
}

.fade-out {
  opacity: 0;
}
</style>
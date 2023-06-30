<template>
  <div class="app">
    <h1>Записи о занятиях</h1>
    <lesson-form @create="addLesson" :lessons="lessons" />
    <lesson-list :lessons="lessons" @remove="removeLesson" />
  </div>
</template>

<script>
import LessonForm from "@/components/LessonForm.vue";
import LessonList from "@/components/LessonList.vue";

export default {
  components: { LessonForm, LessonList },
  data() {
    return {
      lessons: [],
    };
  },
  methods: {
    addLesson(newLesson) {
      this.lessons.push(newLesson);
    },
    removeLesson(lesson) {
      this.lessons = this.lessons.filter((l) => l.id !== lesson.id);
    },
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}
</style>

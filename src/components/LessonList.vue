<template>
  <div v-if="lessons.length > 0">
    <h3>Список занятий</h3>
    <transition-group name="lesson-list">
      <lesson-item
        v-for="lesson in lessons"
        :lesson="lesson"
        :key="lesson.id"
        @remove="$emit('remove', lesson)"
      />
    </transition-group>
  </div>
  <h2 v-else style="color: red">Список занятий пуст</h2>
</template>

<script>
import LessonItem from "@/components/LessonItem";

export default {
  components: {
    LessonItem,
  },

  props: {
    lessons: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.lesson-list-item {
  display: inline-block;
  margin-right: 10px;
}

.lesson-list-enter-active,
.lesson-list-leave-active {
  transition: all 0.4s ease;
}

.lesson-list-enter-from,
.lesson-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

.lesson-list-move {
  transition: transform 0.4s ease;
}
</style>

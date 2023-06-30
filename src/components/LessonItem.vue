<template>
  <div class="lesson">
    <div>
      <strong>Название:</strong>
      {{ lesson.name }}
    </div>

    <div>
      <strong>Даты проведения:</strong>
      с {{ lesson.startDate }} по {{ lesson.endDate }}
    </div>
    <div class="lesson__btns">
      <my-button @click="$emit('remove', lesson)">Удалить</my-button>
    </div>
  </div>
</template>

<script>
import myButton from "@/components/UI/MyButton.vue";

export default {
  components: { myButton },
  props: {
    lesson: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.lesson {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.lesson__btns {
  display: flex;
}
</style>

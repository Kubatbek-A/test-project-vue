<template>
  <form @submit.prevent="createLesson">
    <div class="form-group">
      <label for="lesson">Занятие:</label>
      <my-input
        v-model="newLesson"
        v-focus
        id="lesson"
        placeholder="Название"
      />
    </div>

    <div class="form-group">
      <label for="startDate">Дата начала:</label>
      <my-input v-model="newStartDate" id="startDate" type="date" />
    </div>

    <div class="form-group">
      <label for="endDate">Дата окончания:</label>
      <my-input v-model="newEndDate" id="endDate" type="date" />
    </div>

    <my-button type="submit">Добавить запись</my-button>

    <p v-if="error" class="error-message">{{ error }}</p>
  </form>
</template>

<script>
import myButton from "@/components/UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";

export default {
  components: { myButton, MyInput },

  props: {
    lessons: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      newLesson: "",
      newStartDate: "",
      newEndDate: "",
      error: "",
    };
  },
  methods: {
    createLesson() {
      if (this.isValidInput() && this.isValidDate()) {
        const newLesson = {
          id: Date.now(),
          name: this.newLesson,
          startDate: this.newStartDate,
          endDate: this.newEndDate,
        };
        if (!this.isLessonOverlap(newLesson)) {
          this.$emit("create", newLesson);

          this.clearForm();
          this.error = "";
        } else {
          this.error = "Диапазоны дат пересекаются.";
        }
      }
    },
    isValidInput() {
      if (
        this.newLesson.trim() !== "" &&
        this.newStartDate !== "" &&
        this.newEndDate !== ""
      ) {
        return true;
      } else {
        this.error = "Заполните все поля.";
        return false;
      }
    },
    isValidDate() {
      if (this.newStartDate > this.newEndDate) {
        this.error = "Некорректные даты";
        return false;
      } else {
        return true;
      }
    },
    isLessonOverlap(newLesson) {
      for (const lesson of this.lessons) {
        if (
          (lesson.startDate <= newLesson.startDate &&
            lesson.endDate >= newLesson.startDate) ||
          (lesson.startDate <= newLesson.endDate &&
            lesson.endDate >= newLesson.endDate)
        ) {
          return true;
        }
      }
      return false;
    },
    clearForm() {
      this.newLesson = "";
      this.newStartDate = "";
      this.newEndDate = "";
    },
  },
};
</script>

<style scoped>
.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  font-weight: bold;
}

.form-group input {
  width: 100%;
  padding: 8px;
  font-size: 16px;
}

.error-message {
  color: red;
  font-size: 14px;
  margin-top: 5px;
}
</style>

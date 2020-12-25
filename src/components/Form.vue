<template>
  <div>
    <form-fields
      v-for="field in data"
      :key="field.label"
      :field="field"
      @triggerErr="q"
    />
    <div class="form-submit">
      <button @click="saveData" :disabled="isError">Сохранить</button>
    </div>
  </div>
</template>

<script>
import FormFields from "@/components/FormFields.vue";
export default {
  name: "Form",
  data() {
    return {
      isError: false,
    };
  },
  props: ["data"],
  components: { FormFields },
  methods: {
    saveData() {
      alert("Данные сохранены"); // имитация запроса
    },
    q(data) {
      this.isError = data;
    },
  },
};
</script>
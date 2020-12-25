<template>
  <div>
    <div class="form-line" v-if="field.type === 'string'">
      <input
        type="text"
        placeholder="Имя пользователя"
        v-model="field.value"
        :class="{ 'error-input': errName }"
        @keyup="nameValidator(field.value)"
      />
      <div class="err-msg" v-if="errName">Поле не может быть пустым</div>
    </div>
    <div class="form-line" v-else-if="field.type === 'select'">
      <select
        v-model="field.value"
        :class="{ 'error-input': errSelect }"
        @change="selectValidator(field.value)"
      >
        <option disabled>Выберите пол</option>
        <option v-for="option in field.meta.values" :key="option.value">
          {{ option.value }}
        </option>
      </select>
      <div class="err-msg" v-if="errSelect">Обязательное поле</div>
    </div>
    <div class="form-line" v-else-if="field.type === 'date'">
      <input
        type="date"
        v-model="field.value"
        :class="{ 'error-input': errDate }"
        @change="dateValidator(field.value)"
      />
      <div class="err-msg" v-if="errDate">{{ errDateString }}</div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "FormFields",
  props: ["field"],
  components: {},
  data() {
    return {
      errName: false,
      errSelect: false,
      errDateString: "",
      errDate: false,
      finalErr: false,
    };
  },
  methods: {
    isValid() {
      this.finalErr = this.errName || this.errSelect || this.errDate; // cкладываем ошибки и отправляем в родительский компонент для отключения disable кнопки отправить

      this.$emit("triggerErr", this.finalErr); // проброс данных в родительский компонент через пользовательское событие
    },
    nameValidator(val) {
      if (val) this.errName = false;
      else this.errName = true;
      this.isValid();
    },
    selectValidator(val) {
      if (val !== "male" && val !== "female") this.errSelect = true;
      else this.errSelect = false;
      this.isValid();
    },
    dateValidator(val) {
      const today = moment().year();
      const valYear = val.split("-")[0];
      if (val) {
        if (today < valYear) {
          this.errDateString = "Укажите дату текущего года";
          this.errDate = true;
        } else {
          this.errDateString = "";
          this.errDate = false;
        }
      } else {
        this.errDateString = "Поле не может быть пустым";
        this.errDate = true;
      }
      this.isValid();
    },
  },
};
</script>
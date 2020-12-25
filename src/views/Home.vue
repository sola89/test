<template>
  <div class="container mini-container">
    <div class="text-center"><h1>Данные пользователя</h1></div>
    <div class="home">
      <Form :data="userFields"></Form>
    </div>
  </div>
</template>

<script>
import Form from "@/components/Form.vue";
import moment from "moment";
export default {
  name: "Home",
  components: { Form },
  data() {
    return {
      errors: [],
      userFields: [
        {
          label: "Name",
          field: "name",
          type: "string",
          value: "",
        },
        {
          label: "Gender",
          field: "gender",
          type: "select",
          value: "",
          meta: {
            values: [
              {
                label: "Male",
                value: "male",
              },
              {
                label: "Female",
                value: "female",
              },
            ],
          },
        },
        {
          label: "Subscription",
          field: "sub",
          type: "date",
          value: "",
        },
      ],
      testData: {
        name: "UserName",
        gender: "male",
        sub: "2020-03-04T13:40Z",
      },
    };
  },

  mounted() {
    // Имитация запроса данных с сервера
    this.userFields[0].value = this.testData.name;
    this.userFields[1].value = this.testData.gender;
    this.userFields[2].value = moment(this.testData.sub).format("YYYY-MM-DD");
  },
};
</script>

<template>
  <div class="form-builder">
    <h2>{{ user.name }}</h2>
    <form @submit.prevent="onSubmit">
      <template v-for="(item) in user.items" :key="item.name">
        <form-input
          v-if="item.type === 'input'"
          :label="item.label"
          :type="item.type"
          v-model="inputValues[item.name]"
        />
        <form-select
          v-else-if="item.type === 'select'"
          :label="item.label"
          :options="item.additional.options"
          v-model="selectValues[item.name]"
        />
        <form-radio
          v-else-if="item.type === 'radio'"
          :label="item.label"
          :options="item.additional.options"
          v-model="radioValues[item.name]"
        />
        <form-password
          v-else-if="item.type === 'password'"
          :label="item.label"
          :type="item.type"
          v-model="passwordValues[item.name]"
        />
        <span v-if="item.type === 'password' && item.additional && passwordMismatch" class="error">Пароли не совпадают</span>
      </template>
      <div class="form-builder__buttons">
        <button type="reset" class="button button_reset">Стереть</button>
        <button type="submit" class="button button_submit">Отправить</button>
      </div>
    </form>
    </div>
</template>

<script>
import axios from 'axios';
import FormInput from "@/components/form-items/FormInput.vue";
import FormSelect from "@/components/form-items/FormSelect.vue";
import FormRadio from "@/components/form-items/FormRadio.vue";
import FormPassword from "@/components/form-items/FormPassword.vue";

export default {
  name: "FormBuilder",
  props: {
    user: Object,
  },
  data() {
    return {
      inputValues: {},
      selectValues: {},
      radioValues: {},
      passwordValues: {},
      passwordMismatch: false
    };
  },
  methods: {
    onSubmit() {    
      if (this.passwordValues.pass === this.passwordValues['repeat-pass']) { 
        this.passwordMismatch = false;      
        const formData = {};

        Object.assign(formData, this.inputValues);
        Object.assign(formData, this.selectValues);
        Object.assign(formData, this.radioValues);
        Object.assign(formData, {pass: parseInt(this.passwordValues.pass)});

        console.log(formData)

        axios.post('https://google.com/endpoint', formData)
          .then(response => {
            console.log('Response from server:', response.data);
            alert('Запрос успешно отправлен');
          })
          .catch(error => {
            console.error('Error:', error);
          });
      } else {
        this.passwordMismatch = true;  
      }
    }
  },
  components: {FormPassword, FormRadio, FormSelect, FormInput}
}
</script>

<style scoped lang="scss">
.form-builder {
  max-width: 400px;
  width: 100%;
  padding: 10px 10px 15px;
  border-radius: 10px;
  border: 1px solid #bb8bc3;
  h2 {
    margin: 0 0 10px;
    text-align: center;
  }
  form {
    display: flex;
    flex-direction: column;
    gap: 10px;
    .form-builder__buttons {
      display: flex;
      justify-content: space-between;
      gap: 20px;
      margin: 15px 0 0;
    }
    .button {
      display: inline-block;
      margin: 0 auto;
      width: 200px;
      border-radius: 10px;
      font-weight: 400;
      line-height: 24px;
      text-align: center;
      color: #fcfcfc;
      font-size: 14px;
      border: none;
      padding: 8px 0;
      &.button_submit {
        flex: 1;
        background-image: linear-gradient(87deg, rgb(155, 63, 212) 0%, rgb(118, 54, 223) 98%);
        box-shadow: 0 0 10px 2px #a346f44d;
      }
      &.button_reset {
        background: linear-gradient(to right, #9b3fd4, #aa73b3);
        box-shadow: 0px 0px 10px 2px rgba(163, 70, 244, 0.3);
        max-width: 100px;
      }
    }
    .error {
      color: red;
    }
  }
}
</style>

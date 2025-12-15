<script setup lang="ts">
import { Field, Form, ErrorMessage } from 'vee-validate'
import { ref } from 'vue'
import * as yup from 'yup'

const formSendSuccessfull = ref<boolean>(false)

const PasswordVisibility = ref<boolean>(false)
const ConfirmPasswordVisibility = ref<boolean>(false)

const nameRules = yup.string().required('Поле обязательно для заполнения')
const phoneRegExp =
  /^(([ \\+]\\+[1-9]{1,4}[ \\-]*)|(\\([0-9]{2,3}\\)[ \\-]*)|([0-9]{2,4})[ \\-]*)*?[0-9]{3,4}?[ \\-]*[0-9]{3,4}?$/

const schema = yup.object({
  firstname: nameRules,
  lastname: nameRules,
  country: nameRules,
  // city: yup.string().required('Выберите город'),
  phone: yup
    .string()
    .required('Поле обязательно для заполнения')
    .matches(phoneRegExp, 'Введитие корректный номер телефона'),
  email: nameRules.email('Введите корректный email'),
  password: nameRules,
  'confirm-password': nameRules,
})

const togglePasswordVisibility = () => {
  PasswordVisibility.value = !PasswordVisibility.value
}
const toggleConfirmPasswordVisibility = () => {
  ConfirmPasswordVisibility.value = !ConfirmPasswordVisibility.value
}
const register = () => {
  formSendSuccessfull.value = true
}
</script>

<template>
  <body>
    <div class="container">
      <h1 class="title">Регистрация</h1>
      <Form
        v-if="!formSendSuccessfull"
        :validation-schema="schema"
        @submit="register"
        class="registration-form"
      >
        <div class="form-group">
          <label class="form-label" for="firstname">Имя *</label>
          <Field class="form-control" name="firstname" type="text" id="firstname" />
          <ErrorMessage class="!!!!!!!!" name="firstname" />
        </div>
        <div class="form-group">
          <label class="form-label" for="lastname">Фамилия *</label>
          <Field class="form-control" name="lastname" type="text" id="lastname" />
          <ErrorMessage name="lastname" />
        </div>
        <div class="form-group">
          <label class="form-label" for="country">Страна/Регион *</label>
          <Field class="form-control" name="country" type="text" id="country" />
          <ErrorMessage name="country" />
        </div>
        <div class="form-group">
          <label class="form-label" for="city">Город *</label>
          <div class="custom-select">
            <select class="form-control" id="city" name="city">
              <option value="" disabled selected>Выберите город</option>
              <option value="msc">Москва</option>
              <option value="spb">Санкт-Петербург</option>
              <option value="ovb">Новосибирск</option>
              <option value="svx">Екатеринбург</option>
              <option value="other">Другой</option>
            </select>
          </div>
          <ErrorMessage name="city" />
        </div>
        <div class="form-group">
          <label class="form-label" for="phone">Телефон *</label>
          <Field class="form-control" type="tel" name="phone" id="phone" />
          <ErrorMessage name="phone" />
        </div>
        <div class="form-group">
          <label class="form-label" for="email">Email *</label>
          <Field class="form-control" type="email" name="email" id="email" />
          <ErrorMessage name="email" />
        </div>
        <div class="form-group form-group--password">
          <label class="form-label" for="password">Пароль *</label>
          <Field
            class="form-control"
            :type="PasswordVisibility ? 'text' : 'password'"
            name="password"
            id="password"
          />
          <button
            class="btn-icon btn-icon--password"
            @click.prevent="togglePasswordVisibility()"
            type="button"
          >
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
              <path
                d="M12 4.5C6.5 4.5 2 9 2 12s4.5 7.5 10 7.5S22 14.5 22 12s-4.5-7.5-10-7.5zm0 13c-3.1 0-5.5-2.4-5.5-5.5S8.9 7.5 12 7.5s5.5 2.4 5.5 5.5S15.1 17.5 12 17.5z"
              />
              <path d="M12 10c-1.1 0-2 .9-2 2s.9 2 2 2c1.1 0 2-.9 2-2s-.9-2-2-2z" />
            </svg>
          </button>
          <ErrorMessage name="password" />
        </div>
        <div class="form-group form-group--password">
          <label class="form-label" for="confirm-password">Подтвердите пароль *</label>
          <Field
            class="form-control"
            :type="ConfirmPasswordVisibility ? 'text' : 'password'"
            name="confirm-password"
            id="confirm-password"
          />
          <button
            class="btn-icon btn-icon--password"
            type="button"
            @click="toggleConfirmPasswordVisibility"
          >
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
              <path
                d="M12 4.5C6.5 4.5 2 9 2 12s4.5 7.5 10 7.5S22 14.5 22 12s-4.5-7.5-10-7.5zm0 13c-3.1 0-5.5-2.4-5.5-5.5S8.9 7.5 12 7.5s5.5 2.4 5.5 5.5S15.1 17.5 12 17.5z"
              />
              <path d="M12 10c-1.1 0-2 .9-2 2s.9 2 2 2c1.1 0 2-.9 2-2s-.9-2-2-2z" />
            </svg>
          </button>
          <ErrorMessage name="confirm-password" />
        </div>
        <div class="form-group form-group--full-width">
          <label class="form-label" for="comments">Дополнительная информация</label>
          <textarea class="form-control" id="comments" name="comments"></textarea>
        </div>
        <div class="form-group form-group--full-width">
          <label class="form-label form-label--checkbox" for="terms">
            <Field type="checkbox" id="terms" name="terms" />
            Я согласен c условиями пользования и политикой конфиденциальности
          </label>
        </div>
        <button class="btn" type="submit">Зарегистрироваться</button>
        <button class="btn" type="reset">Очистить форму</button>
      </Form>
      <div v-if="formSendSuccessfull" class="message message--success">
        Регистрация прошла успешно!
      </div>
    </div>
  </body>
</template>

<style scoped></style>

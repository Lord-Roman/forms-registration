<script setup lang="ts">
import { Field, Form, ErrorMessage } from 'vee-validate'
import * as yup from 'yup'

const nameRules = yup.string().required()
</script>

<template>
  <body>
    <div class="container">
      <h1 class="title">Регистрация</h1>
      <Form @submit="submit" class="registration-form">
        <div class="form-group">
          <label class="form-label" for="firstname">Имя *</label>
          <Field
            class="form-control"
            name="firstname"
            type="text"
            id="firstname"
            :rules="nameRules"
          />
          <ErrorMessage name="firstname" />
        </div>
        <div class="form-group">
          <label class="form-label" for="lastname">Фамилия *</label>
          <Field
            class="form-control"
            name="lastname"
            type="text"
            id="lastname"
            :rules="nameRules"
          />
          <ErrorMessage name="lastname" />
        </div>
        <div class="form-group">
          <label class="form-label" for="country">Страна/Регион *</label>
          <Field class="form-control" name="country" type="text" id="country" :rules="isRequired" />
          <ErrorMessage name="country" />
        </div>
        <div class="form-group">
          <label class="form-label" for="city">Город *</label>
          <div class="custom-select">
            <select class="form-control" id="city" name="city" :rules="isRequired">
              <option value="" disabled selected>Выберите город</option>
              <option value="msc">Москва</option>
              <option value="spb">Санкт-Петербург</option>
              <option value="ovb">Новосибирск</option>
              <option value="svx">Екатеринбург</option>
              <option value="other">Другой</option>
            </select>
          </div>
        </div>
        <div class="form-group">
          <label class="form-label" for="phone">Телефон *</label>
          <Field class="form-control" type="tel" name="phone" id="phone" :rules="isRequired" />
        </div>
        <div class="form-group">
          <label class="form-label" for="email">Email *</label>
          <Field class="form-control" type="email" name="email" id="email" :rules="isRequired" />
        </div>
        <div class="form-group form-group--password">
          <label class="form-label" for="password">Пароль *</label>
          <Field
            class="form-control"
            type="password"
            name="password"
            id="password"
            :rules="isRequired"
          />
          <button class="btn-icon btn-icon--password" type="button">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
              <path
                d="M12 4.5C6.5 4.5 2 9 2 12s4.5 7.5 10 7.5S22 14.5 22 12s-4.5-7.5-10-7.5zm0 13c-3.1 0-5.5-2.4-5.5-5.5S8.9 7.5 12 7.5s5.5 2.4 5.5 5.5S15.1 17.5 12 17.5z"
              />
              <path d="M12 10c-1.1 0-2 .9-2 2s.9 2 2 2c1.1 0 2-.9 2-2s-.9-2-2-2z" />
            </svg>
          </button>
        </div>
        <div class="form-group form-group--password">
          <label class="form-label" for="confirm-password">Подтвердите пароль *</label>
          <Field
            class="form-control"
            type="password"
            name="confirm-password"
            id="confirm-password"
            :rules="isRequired"
          />
          <button class="btn-icon btn-icon--password" type="button">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
              <path
                d="M12 4.5C6.5 4.5 2 9 2 12s4.5 7.5 10 7.5S22 14.5 22 12s-4.5-7.5-10-7.5zm0 13c-3.1 0-5.5-2.4-5.5-5.5S8.9 7.5 12 7.5s5.5 2.4 5.5 5.5S15.1 17.5 12 17.5z"
              />
              <path d="M12 10c-1.1 0-2 .9-2 2s.9 2 2 2c1.1 0 2-.9 2-2s-.9-2-2-2z" />
            </svg>
          </button>
        </div>
        <div class="form-group form-group--full-width">
          <label class="form-label" for="comments">Дополнительная информация</label>
          <textarea class="form-control" id="comments" name="comments"></textarea>
        </div>
        <div class="form-group form-group--full-width">
          <label class="form-label form-label--checkbox" for="terms">
            <Field type="checkbox" id="terms" name="terms" :rules="isRequired" />
            Я согласен c условиями пользования и политикой конфиденциальности
          </label>
        </div>
        <button class="btn" type="submit">Зарегистрироваться</button>
        <button class="btn" type="reset">Очистить форму</button>
      </Form>
      <div class="message message--success">Регистрация прошла успешно!</div>
    </div>
  </body>
</template>

<style scoped></style>

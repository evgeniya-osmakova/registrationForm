<template>
  <form v-on:change="$emit('changeAddressValidity', $v.$invalid)">
    <h1><label for="user-data-address">Адрес</label></h1>
    <div id="user-data-address">
      <div class="error" v-if="$v.index.$error">
        {{ errs.onlyNumbers }}
      </div>
      <div class="form-group">
        <label for="user-data-index">Индекс</label>
        <input id="user-data-index" type="text" name="index"
               v-model="index" @blur="$v.index.$touch()">
      </div>

      <div class="error" v-if="$v.country.$error">
        {{ errs.onlyAlpha }}
      </div>
      <div class="form-group">
        <label for="user-data-country">Страна</label>
        <input id="user-data-country" type="text" name="country"
               v-model="country" @blur="$v.country.$touch()">
      </div>

      <div class="error" v-if="$v.region.$error">
        {{ errs.onlyAlpha }}
      </div>
      <div class="form-group">
        <label for="user-data-region">Область</label>
        <input id="user-data-region" type="text" name="region"
               v-model="region" @blur="$v.region.$touch()">
      </div>

      <div class="error" v-if="$v.town.$error">
        <template v-if="!$v.town.alpha">
          {{ errs.onlyAlpha }}
        </template>
        <template v-else>
          {{ errs.empty }}
        </template>
      </div>

      <div class="form-group">
        <label for="user-data-town">Город<sup>*</sup></label>
        <input id="user-data-town" type="text" name="town"
               v-model="town" @blur="$v.town.$touch()">
      </div>

      <div class="form-group">
        <label for="user-data-street">Улица</label>
        <input id="user-data-street" type="text" name="street">
      </div>

      <div class="form-group">
        <label for="user-data-house">Дом</label>
        <input id="user-data-house" type="text" name="house">
      </div>
    </div>
  </form>
</template>

<script>
import { required } from 'vuelidate/lib/validators';

export default {
  name: 'Address',
  props: ['errs'],
  data() {
    return {
      index: '',
      country: '',
      region: '',
      town: '',
      street: '',
      house: '',
    };
  },
  validations: {
    index: {
      numeric: (val) => /^[0-9]*$/i.test(val),
    },
    country: {
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    region: {
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    town: {
      required,
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
  },
};
</script>

<style scoped>
  .form-group {
    border-radius: 5px;
    background-color: white;
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-end;
    padding: .5em;
    margin-bottom: 24px;
  }

  .error {
    color: red;
  }
</style>

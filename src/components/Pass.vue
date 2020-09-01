<template>
    <form v-on:change="$emit('changePassValidity', $v.$invalid)">
        <h1><label for="user-data-passport">Паспорт</label></h1>
        <div id="user-data-passport">
            <div class="form-group">
                <div class="error" v-if="$v.docType.$error">
                    {{ errs.empty }}
                </div>
                    <label for="user-data-docType">Тип документа<sup>*</sup></label>
                    <select id="user-data-docType" name="docType" size="3" v-model="docType" >
                        <option value="passport">Паспорт</option>
                        <option value="certificate">Свидетельство о рождении</option>
                        <option value="license">Вод. удостоверение</option>
                    </select>
            </div>

            <div class="error" v-if="$v.series.$error">
                {{ errs.onlyNumbers }}
            </div>
            <div class="form-group">
                <label for="user-data-series">Серия</label>
                <input id="user-data-series" type="text" name="series"
                       v-model="series" @blur="$v.series.$touch()">
            </div>

            <div class="error" v-if="$v.number.$error">
                {{ errs.onlyNumbers }}
            </div>
            <div class="form-group">
                <label for="user-data-number">Номер</label>
                <input id="user-data-number" type="text" name="number"
                       v-model="number" @blur="$v.number.$touch()">
            </div>

            <div class="form-group">
                <label for="user-data-issued">Кем выдан</label>
                <input id="user-data-issued" type="text" name="issued">
            </div>

            <div class="error" v-if="$v.date.$error">
                {{ errs.empty }}
            </div>
            <div class="form-group">
                <label for="user-data-date">Дата выдачи<sup>*</sup></label>
                <input id="user-data-date" type="date" name="date"
                       v-model="date" @blur="$v.date.$touch()">
            </div>
        </div>
    </form>
</template>

<script>
import { required } from 'vuelidate/lib/validators';

export default {
  name: 'Pass',
  props: ['errs'],

  data() {
    return {
      docType: '',
      series: '',
      number: '',
      date: '',
    };
  },
  validations: {
    docType: {
      required,
    },
    series: {
      numeric: (val) => /^[0-9]*$/i.test(val),
    },
    number: {
      numeric: (val) => /^[0-9]*$/i.test(val),
    },
    date: {
      required,
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

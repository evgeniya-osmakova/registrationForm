<template>
    <form v-on:change="$emit('changeBioValidity', $v.$invalid)">
        <h1><label for="user-data-main">Основные данные</label></h1>
        <div id="user-data-main">

            <div class="error" v-if="$v.surname.$error">
                <template v-if="!$v.surname.alpha">
                    {{ errs.onlyAlpha }}
                </template>
                <template v-else>
                    {{ errs.empty }}
                </template>
            </div>
            <div class="form-group">
                <label for="user-data-surname">Фамилия<sup>*</sup></label>
                <input id="user-data-surname" type="text" name="surname"
                       v-model="surname" @blur="$v.surname.$touch()">
            </div>

            <div class="error" v-if="$v.name.$error">
                <template v-if="!$v.name.alpha">
                    {{ errs.onlyAlpha }}
                </template>
                <template v-else>
                    {{ errs.empty }}
                </template>
            </div>
            <div class="form-group">
                <label for="user-data-name">Имя<sup>*</sup></label>
                <input id="user-data-name" type="text" name="name"
                       v-model="name" @blur="$v.name.$touch()">
            </div>

            <div class="error" v-if="$v.patronymic.$error">
                {{ errs.onlyAlpha }}
            </div>
            <div class="form-group">
                <label for="user-data-patronymic">Отчество</label>
                <input id="user-data-patronymic" type="text" name="patronymic"
                   v-model="patronymic" @blur="$v.patronymic.$touch()">
            </div>

            <div class="error" v-if="$v.birth.$error">
                {{ errs.empty }}
            </div>
            <div class="form-group">
                <label for="user-data-birth">Дата рождения<sup>*</sup></label>
                <input id="user-data-birth" type="date" name="birth"
                       v-model="birth" @blur="$v.birth.$touch()">
            </div>

            <div class="error" v-if="$v.phone.$error">
                <div v-if="!$v.phone.numeric">
                    {{ errs.onlyNumbers }}
                </div>
                <div v-if="!$v.phone.validFormat">
                    {{ errs.phone }}
                </div>
                <div v-if="!$v.phone.maxLength || !$v.phone.minLength">
                    Номер телефона должен содержать {{$v.phone.$params.minLength.min}} цифр
                </div>
                <div v-if="!$v.phone.required">
                    {{ errs.empty }}
                </div>
            </div>
            <div class="form-group">
                <label for="user-data-phone">Номер телефона<sup>*</sup></label>
                <input id="user-data-phone" type="tel" placeholder="7XXXXXXXXXX" name="phone"
                       v-model="phone" @blur="$v.phone.$touch()">
            </div>

            <div class="error" v-if="$v.sex.$error">
                {{ errs.onlyAlpha }}
            </div>
            <div class="form-group">
                <label for="user-data-sex">Пол</label>
                <input id="user-data-sex" type="text" name="sex"
                       v-model="sex" @blur="$v.sex.$touch()">
            </div>

            <div class="error" v-if="$v.clientgroup.$error">
                {{ errs.empty }}
            </div>
            <div class="form-group">
                <label for="user-data-clientgroup">Группа клиентов<sup>*</sup></label>
                <select id="user-data-clientgroup"
                        name="clientgroup" size="3" multiple v-model="clientgroup" >
                    <option value="vip">VIP</option>
                    <option value="problem">Проблемные</option>
                    <option value="oms">ОМС</option>
                </select>
            </div>

            <div class="form-group">
                <label for="user-data-doctor">Лечащий врач</label>
                <select id="user-data-doctor" name="doctor" size="3">
                    <option value="ivanov">Иванов</option>
                    <option value="zakharov">Захаров</option>
                    <option value="chernysheva">Чернышева</option>
                </select>
            </div>

            <div class="form-group">
                <label for="user-data-sms">Не отправлять смс</label>
                <input id="user-data-sms" type="checkbox" name="sms">
            </div>
        </div>
    </form>
</template>

<script>
import { required, minLength, maxLength } from 'vuelidate/lib/validators';

export default {
  name: 'Bio',
  props: ['errs'],

  data() {
    return {
      surname: '',
      name: '',
      patronymic: '',
      birth: null,
      phone: null,
      sex: '',
      clientgroup: '',
    };
  },

  validations: {
    surname: {
      required,
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    name: {
      required,
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    patronymic: {
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    birth: {
      required,
    },
    phone: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
      validFormat: (val) => /^7/.test(val),
      numeric: (val) => /^[0-9]*$/i.test(val),
    },
    sex: {
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    clientgroup: {
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

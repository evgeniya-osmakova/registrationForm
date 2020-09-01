<template>
  <div class="container">
    <form @submit.prevent="showMessage" data-form="user-data">
      <Bio :errs=errsMsgs v-on:changeBioValidity="onChangeBioValidity" />
      <Address :errs=errsMsgs v-on:changeAddressValidity="onChangeAddressValidity" />
      <Pass :errs=errsMsgs v-on:changePassValidity="onChangePassValidity" />
      <button :errs=errsMsgs type="submit"
              :disabled="invalidAllForm" class="btn btn-primary">Отправить</button>
    </form>
  </div>
</template>

<script>
import Bio from './components/Bio.vue';
import Address from './components/Address.vue';
import Pass from './components/Pass.vue';

export default {
  components: { Pass, Address, Bio },

  data() {
    return {
      errsMsgs: {
        empty: 'Поле обязательно для заполнения',
        onlyNumbers: 'Поле должно содержать только цифры',
        onlyAlpha: 'Поле должно содержать только русские буквы',
        phone: 'Номер телефона должен начинаться с цифры 7',
      },
      invalidBio: true,
      invalidAddress: true,
      invalidPass: true,
      invalidAllForm: true,
    };
  },

  methods: {
    showMessage() {
      // eslint-disable-next-line no-alert
      alert('Клиент создан');
    },
    onChangeBioValidity(value) {
      this.invalidBio = value;
      this.invalidAllForm = this.invalidBio || this.invalidAddress || this.invalidPass;
    },
    onChangeAddressValidity(value) {
      this.invalidAddress = value;
      this.invalidAllForm = this.invalidBio || this.invalidAddress || this.invalidPass;
    },
    onChangePassValidity(value) {
      this.invalidPass = value;
      this.invalidAllForm = this.invalidBio || this.invalidAddress || this.invalidPass;
    },
  },
};
</script>

<style>
  .container {
    border-radius: 5px;
    background-color: whitesmoke;
    padding: 20px;
  }

  .form-group label {
    padding: .5em 1em .5em 0;
    flex: 1;
  }

  .form-group input {
    flex: 2;
  }

  footer {
    position: absolute;
    width: 100%;
    text-align: center;
  }
</style>

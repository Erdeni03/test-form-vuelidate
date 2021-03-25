<template>
  <div id="app" class="container">
    <form class="card" @submit.prevent="submitHandler">
      <h1>VueJs Vuelidate</h1>

      <div class="form-control">
        <label for="name">Фамилия*</label>
        <input
          type="text"
          id="name"
          placeholder="Введите фамилию"
          :class="{invalid: $v.surname.$dirty && !$v.surname.required}"
          v-model.trim="surname"
        />
        <small class="invalid" v-if="$v.surname.$dirty && !$v.surname.required"
          >Поле не должно быть пустым</small
        >
      </div>
      <div class="form-control">
        <label for="name">Имя*</label>
        <input
          type="text"
          id="name"
          placeholder="Введите имя"
          :class="{invalid: $v.name.$dirty && !$v.name.required}"
          v-model.trim="name"
        />
        <small class="invalid" v-if="$v.name.$dirty && !$v.name.required"
          >Поле не должно быть пустым</small
        >
      </div>
      <div class="form-control">
        <label for="name">Отчество</label>
        <input
          type="text"
          id="name"
          placeholder="Введите отчество"
          v-model.trim="patronymic"
        />
      </div>

      <div class="form-control">
        <label for="dateBirthday">Дата рождения*</label>
        <input
          type="date"
          id="dateBirthday"
          v-model="dateBirthday"
          :class="{
            invalid: $v.dateBirthday.$dirty && !$v.dateBirthday.required
          }"
        />
        <small
          class="invalid"
          v-if="$v.dateBirthday.$dirty && !$v.dateBirthday.required"
          >Обязательное поле</small
        >
      </div>
      <div class="form-control">
        <label for="tel">Номер телефона*</label>
        <input
          type="tel"
          name="tel"
          placeholder="791-4567-8901"
          v-model.number="tel"
          :class="{
            invalid:
              ($v.tel.$dirty && !$v.tel.required) ||
              ($v.tel.$dirty && !$v.tel.telRegex)
          }"
        />
        <small class="invalid" v-if="$v.tel.$dirty && !$v.tel.required"
          >Поле не должно быть пустым</small
        >

        <small class="invalid" v-else-if="$v.tel.$dirty && !$v.tel.telRegex"
          >Поле Номер телефона должен начинаться с 7 и содержать 11 цифр</small
        >
      </div>
      <div class="form-control">
        <label for="gender">Пол</label>
        <input type="text" name="gender" v-model="gender" />
      </div>
      <div class="form-control">
        <label for="client">Группа клиентов*</label>
        <select
          id="client"
          multiple
          size="3"
          v-model.trim="clientGroup"
          :class="{
            invalid: $v.clientGroup.$dirty && !$v.clientGroup.required
          }"
        >
          <option value="VIP">VIP</option>
          <option value="Проблемные">Проблемные</option>
          <option value="ОМС">ОМС</option>
        </select>
        <small
          class="invalid"
          v-if="$v.clientGroup.$dirty && !$v.clientGroup.required"
          >Поле не должно быть пустым</small
        >
      </div>
      <div class="form-control">
        <label for="doctor">Лечащий врач</label>
        <select name="doctor" v-model="doctor">
          <option value="Иванов">Иванов</option>
          <option value="Захаров">Захаров</option>
          <option value="Чернышева">Чернышева</option>
        </select>
      </div>
      <div class="form-checkbox">
        <label for="check">Не отправлять СМС</label>
        <input type="checkbox" name="check" v-model="sendCheck" />
      </div>

      <h3>Адрес:</h3>

      <div class="form-control">
        <label for="postcode">Индекс</label>
        <input type="text" id="postcode" name="postcode" v-model="postcode" />
      </div>

      <div class="form-control">
        <label for="country">Страна</label>
        <input type="text" id="country" name="country" v-model="country" />
      </div>

      <div class="form-control">
        <label for="region">Область</label>
        <input type="text" id="region" name="region" v-model="region" />
      </div>

      <div class="form-control">
        <label for="city">Город*</label>
        <input
          type="text"
          id="city"
          name="city"
          v-model.trim="city"
          :class="{
            invalid: $v.city.$dirty && !$v.city.required
          }"
        />
        <small class="invalid" v-if="$v.city.$dirty && !$v.city.required"
          >Поле не должно быть пустым</small
        >
      </div>

      <div class="form-control">
        <label for="street">Улица</label>
        <input type="text" id="street" name="street" v-model="street" />
      </div>
      <div class="form-control">
        <label for="house">Дом</label>
        <input type="text" id="house" name="house" v-model="house" />
      </div>

      <h3>Паспорт:</h3>
      <div class="form-control">
        <label for="document">Тип документа*</label>
        <select
          name="document"
          v-model.trim="documentType"
          :class="{
            invalid: $v.documentType.$dirty && !$v.documentType.required
          }"
        >
          <option value="Паспорт">Паспорт</option>
          <option value="Свидетельство о рождении"
            >Свидетельство о рождении</option
          >
          <option value="Вод. удостоверение">Вод. удостоверение</option>
        </select>
        <small
          class="invalid"
          v-if="$v.documentType.$dirty && !$v.documentType.required"
          >Обязательное поле</small
        >
      </div>

      <div class="form-control">
        <label for="passport_series">Серия</label>
        <input
          type="text"
          id="passport_series"
          name="passport_series"
          v-model="passportSeries"
        />
      </div>

      <div class="form-control">
        <label for="passport_region">Область</label>
        <input
          type="text"
          id="passport_region"
          name="passport_region"
          v-model="passportRegion"
        />
      </div>

      <div class="form-control">
        <label for="passport_ID">Номер</label>
        <input
          type="number"
          id="passport_ID"
          name="passport_ID"
          v-model="passportID"
        />
      </div>

      <div class="form-control">
        <label for="issued_by">Кем выдан</label>
        <input type="text" id="issued_by" name="issued_by" v-model="issuedBy" />
      </div>

      <div class="form-control">
        <label for="date_of_issue">Дата выдачи*</label>
        <input
          type="text"
          id="date_of_issue"
          name="date_of_issue"
          v-model.trim="dateOfIssue"
          :class="{
            invalid: $v.dateOfIssue.$dirty && !$v.dateOfIssue.required
          }"
        />
        <small
          class="invalid"
          v-if="$v.dateOfIssue.$dirty && !$v.dateOfIssue.required"
          >Поле не должно быть пустым</small
        >
      </div>

      <button type="submit" class="btn primary">Отправить</button>
      <div class="card marked center" v-if="validateForm">
        <small class="primary">Клиент успешно создан!</small>
      </div>
    </form>
  </div>
</template>

<script>
import {required, helpers} from 'vuelidate/lib/validators'
const telRegex = helpers.regex('alpha', /^7\d{10}/)
export default {
  data() {
    return {
      surname: '',
      name: '',
      patronymic: '',
      dateBirthday: '',
      tel: '',
      gender: '',
      clientGroup: [],
      doctor: '',
      sendCheck: '',
      postcode: '',
      country: '',
      region: '',
      city: '',
      street: '',
      house: '',
      documentType: '',
      passportSeries: '',
      passportRegion: '',
      passportID: '',
      issuedBy: '',
      dateOfIssue: '',
      validateForm: false
    }
  },
  validations: {
    surname: {
      required
    },
    name: {
      required
    },
    dateBirthday: {
      required
    },
    tel: {
      required,
      telRegex
    },
    clientGroup: {
      required
    },
    city: {
      required
    },
    documentType: {
      required
    },
    dateOfIssue: {
      required
    }
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch()

        return
      }

      this.validateForm = true
    }
  }
}
</script>

<style>
.form-control small {
  color: #e53935;
}

.form-control.invalid input {
  border-color: #e53935;
}
</style>

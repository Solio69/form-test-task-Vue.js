<template>
  <div class="form-wrapper">
    <form class="form" @submit.prevent="checkForm" novalidate>
      <div class="form_item">
        <label>Фамилия*</label>
        <div class="form_item-wrapper">
          <input
            :class="[$v.lastName.$error ? errorClass : '', activeClass]"
            v-model="lastName"
            @blur="$v.lastName.$touch()"
            type="text"
          />
          <div class="form_item-error" v-if="$v.lastName.$error">
            Поле обязательное для заполнения
          </div>
        </div>
      </div>
      <div class="form_item">
        <label>Имя*</label>
        <div class="form_item-wrapper">
          <input
            v-model="firstName"
            @blur="$v.firstName.$touch()"
            :class="[$v.firstName.$error ? errorClass : '', activeClass]"
            type="text"
          />
          <div class="form_item-error" v-if="$v.firstName.$error">
            Поле обязательное для заполнения
          </div>
        </div>
      </div>
      <div class="form_item">
        <label>Отчество</label>
        <input class="form_item-input" v-model="middleName" type="text" />
      </div>
      <div class="form_item">
        <label for="date">Дата рождения* </label>
        <div class="form_item-wrapper">
          <input
            :class="[$v.birthday.$error ? errorClass : '', activeClass]"
            type="date"
            id="date"
            name="date"
            v-model="birthday"
            @blur="$v.birthday.$touch()"
          />
          <div class="form_item-error" v-if="$v.birthday.$error">
            Поле обязательное для заполнения
          </div>
        </div>
      </div>
      <div class="form_item">
        <label>Номер телефона*</label>
        <div class="form_item-wrapper">
          <input
            v-model="phone"
            @blur="$v.phone.$touch()"
            :class="[$v.phone.$error ? errorClass : '', activeClass]"
            type="number"
          />
          <div
            class="form_item-error"
            v-if="$v.phone.$error && !$v.phone.required"
          >
            Поле обязательное для заполнения
          </div>
          <div
            class="form_item-error"
            v-if="$v.phone.$error && !$v.phone.checkFirstLetter"
          >
            Номер должен начинаться с 7
          </div>
          <div
            class="form_item-error"
            v-if="
              $v.phone.$error && (!$v.phone.minLength || !$v.phone.maxLength)
            "
          >
            Номер долден содержать 11 цифр
          </div>
        </div>
      </div>
      <div class="form_item">
        <span>Пол:</span>
        <label>Женский</label>
        <input type="radio" value="Женский" v-model="sex" />
        <label>Мужской</label>
        <input type="radio" value="Мужской" v-model="sex" />
      </div>
      <div class="form_item">
        <label>Группа клиентов*</label>
        <div>
          <select
            class="form_item-select"
            size="3"
            multiple
            name=""
            v-model="customerGroup"
            @blur="$v.customerGroup.$touch()"
            :class="{ errorValid: $v.customerGroup.$error }"
          >
            <option value="VIP">VIP</option>
            <option value="Проблемные">Проблемные</option>
            <option value="ОМС">ОМС</option>
          </select>
          <div class="form_item-error" v-if="$v.customerGroup.$error">
            Поле обязательное для заполнения
          </div>
        </div>
      </div>
      <div class="form_item">
        <label>Лечащий врач</label>
        <select
          class="form_item-select"
          size="3"
          name=""
          v-model="attendingDoctor"
        >
          <option value="Иванов">Иванов</option>
          <option value="Захаров">Захаров</option>
          <option value="Чернышева">Чернышева</option>
        </select>
      </div>
      <div class="form_item">
        <label>Не отправлять СМС</label>
        <input type="checkbox" v-model="notSMS" />
      </div>
      <h3>Адрес:</h3>
      <div class="form_item">
        <label>Индекс</label>
        <input class="form_item-input" type="text" v-model="index" />
      </div>
      <div class="form_item">
        <label>Страна</label>
        <input class="form_item-input" type="text" v-model="country" />
      </div>
      <div class="form_item">
        <label>Область</label>
        <input class="form_item-input" type="text" v-model="region" />
      </div>
      <div class="form_item">
        <label class="form_item">Город*</label>
        <div class="form_item-wrapper">
          <input
            :class="[$v.city.$error ? errorClass : '', activeClass]"
            type="text"
            v-model="city"
            @blur="$v.city.$touch()"
          />
          <div class="form_item-error" v-if="$v.city.$error">
            Поле обязательное для заполнения
          </div>
        </div>
      </div>
      <div class="form_item">
        <label>Улица</label>
        <input class="form_item-input" type="text" v-model="street" />
      </div>
      <div class="form_item">
        <label>Дом</label>
        <input class="form_item-input" type="text" v-model="houseNumber" />
      </div>
      <h3>Паспорт:</h3>
      <div class="form_item">
        <label>Тип документа*</label>
        <div class="form_item-wrapper">
          <select
            class="form_item-select"
            size="3"
            name=""
            v-model="documentType"
            @blur="$v.documentType.$touch()"
            :class="{ errorValid: $v.documentType.$error }"
          >
            <option value="Паспорт">Паспорт</option>
            <option value="Свидетельство о рождении">
              Свидетельство о рождении
            </option>
            <option value="Вод. удостоверение">Вод. удостоверение</option>
          </select>
          <div class="form_item-error" v-if="$v.documentType.$error">
            Поле обязательное для заполнения
          </div>
        </div>
      </div>
      <div class="form_item">
        <label>Серия</label>
        <input class="form_item-input" type="number" v-model="documentSeries" />
      </div>
      <div class="form_item">
        <label>Номер</label>
        <input class="form_item-input" type="number" v-model="documentNumber" />
      </div>
      <div class="form_item">
        <label>Кем выдан</label>
        <input class="form_item-input" type="text" v-model="lssuedBy" />
      </div>
      <div class="form_item">
        <label for="date">Дата выдачи*</label>
        <div class="form_item-wrapper">
          <input
            :class="[$v.dateOfIssue.$error ? errorClass : '', activeClass]"
            type="date"
            id="date"
            name="date"
            v-model="dateOfIssue"
            @blur="$v.dateOfIssue.$touch()"
          />
          <div class="form_item-error" v-if="$v.dateOfIssue.$error">
            Поле обязательное для заполнения
          </div>
        </div>
      </div>
      <input class="form_item-btn" type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";

const checkFirstLetter = (value) => value[0] == 7;

export default {
  props: ["showSuccess"],
  data() {
    return {
      lastName: "",
      firstName: "",
      middleName: "",
      birthday: "",
      phone: 7,
      sex: "",
      customerGroup: [],
      attendingDoctor: "",
      notSMS: false,
      index: "",
      country: "",
      region: "",
      city: "",
      street: "",
      houseNumber: "",
      documentType: "",
      documentSeries: "",
      documentNumber: "",
      lssuedBy: "",
      dateOfIssue: "",

      activeClass: "form_item-input",
      errorClass: "errorValid",
    };
  },
  validations: {
    lastName: {
      required,
    },
    firstName: {
      required,
    },
    birthday: {
      required,
    },
    phone: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
      checkFirstLetter, // должнен начинаться с 7
    },
    customerGroup: {
      required,
    },
    city: {
      required,
    },
    documentType: {
      required,
    },
    dateOfIssue: {
      required,
    },
  },

  methods: {
    checkForm() {
      this.$v.$touch();
      if (!this.$v.$error) {
        const formData = {
          lastName: this.lastName,
          firstName: this.firstName,
          middleName: this.middleName,
          birthday: this.birthday,
          phone: this.phone,
          sex: this.sex,
          customerGroup: this.customerGroup,
          attendingDoctor: this.attendingDoctor,
          notSMS: this.notSMS,
          index: this.index,
          country: this.country,
          region: this.region,
          city: this.city,
          street: this.street,
          houseNumber: this.houseNumber,
          documentType: this.documentType,
          documentSeries: this.documentSeries,
          documentNumber: this.documentNumber,
          lssuedBy: this.lssuedBy,
          dateOfIssue: this.dateOfIssue,
        };
        this.$emit("checkForm", formData);
      }
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
/* валидация */
.errorValid {
  border: 2px solid rgba(236, 108, 108, 0.7) !important;
  box-shadow: 0 0 10px rgb(236, 108, 108, 0.7) !important;
}
.form {
  padding: 15px;
}
.form-wrapper {
  background: rgba(112, 220, 228, 0.6);
  max-width: 380px;
  font-family: "Nunito", sans-serif;
}
.form_item {
  color: black;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  margin-bottom: 10px;
}
.form_item-wrapper {
  margin-left: 10px;
}
.form_item-input {
  outline: none;
  min-width: 200px;
  height: 25px;
  border-width: 1px;
  border-style: none;
  border-color: rgb(17, 104, 155, 0.5);
  border-radius: 4px;
}

.form_item-input:focus {
  border: 2px solid rgba(81, 203, 238, 1);
  box-shadow: 0 0 10px rgba(81, 203, 238, 1);
}
.form_item-error {
  font-size: 10px;
}

.form_item-select {
  min-width: 200px;
  border-style: none;
  border-color: rgb(17, 104, 155, 0.5);
  border-radius: 2px;
}

.form_item-select:focus {
  border: 2px solid rgba(81, 203, 238, 1);
  box-shadow: 0 0 10px rgba(81, 203, 238, 1);
  outline: none;
}
.form_item-select option {
  font-weight: normal;
}
.form_item-btn {
  width: 130px;
  height: 30px;
  border-radius: 13px;
  color: wheat;
  background-color: rgb(119, 159, 233);
  outline: none;
  font-size: 15px;
  border-color: wheat;
  cursor: pointer;
}
</style>

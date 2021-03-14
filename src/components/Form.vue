<template>
  <form @submit.prevent="checkForm" novalidate>
    <div>
      <label>Фамилия*</label>
      <input
        v-model="lastName"
        @blur="$v.lastName.$touch()"
        :class="{ errorValid: $v.lastName.$error }"
        type="text"
      />
      <span v-if="$v.lastName.$error">Поле обязательное для заполнения</span>
    </div>
    <div>
      <label>Имя*</label>
      <input
        v-model="firstName"
        @blur="$v.firstName.$touch()"
        :class="{ errorValid: $v.firstName.$error }"
        type="text"
      />
      <span v-if="$v.firstName.$error">Поле обязательное для заполнения</span>
    </div>
    <div>
      <label>Отчество</label>
      <input v-model="middleName" type="text" />
    </div>
    <div>
      <label for="date">Дата рождения*: </label>
      <input
        type="date"
        id="date"
        name="date"
        v-model="birthday"
        @blur="$v.birthday.$touch()"
        :class="{ errorValid: $v.birthday.$error }"
      />
      <span v-if="$v.birthday.$error">Поле обязательное для заполнения</span>
    </div>
    <div>
      <label>Номер телефона*</label>
      <input
        v-model="phone"
        @blur="$v.phone.$touch()"
        :class="{ errorValid: $v.phone.$error }"
        type="number"
      />
      <span v-if="$v.phone.$error && !$v.phone.required"
        >Поле обязательное для заполнения</span
      >
      <span v-if="$v.phone.$error && !$v.phone.checkFirstLetter"
        >Номер должен начинаться с 7</span
      >
      <span
        v-if="$v.phone.$error && (!$v.phone.minLength || !$v.phone.maxLength)"
        >Номер долден содержать 11 цифр</span
      >
    </div>
    <div>
      <span>Пол</span>
      <label>Женский</label>
      <input type="radio" value="Женский" v-model="sex" />
      <label>Мужской</label>
      <input type="radio" value="Мужской" v-model="sex" />
    </div>
    <div>
      <label>Группа клиентов*</label>
      <select
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
      <span v-if="$v.customerGroup.$error"
        >Поле обязательное для заполнения</span
      >
    </div>
    <div>
      <label>Лечащий врач</label>
      <select size="3" name="" v-model="attendingDoctor">
        <option value="Иванов">Иванов</option>
        <option value="Захаров">Захаров</option>
        <option value="Чернышева">Чернышева</option>
      </select>
    </div>
    <div>
      <label>Не отправлять СМС</label>
      <input type="checkbox" v-model="notSMS" />
    </div>
    <h3>Адрес:</h3>
    <div>
      <label>Индекс</label>
      <input type="text" v-model="index" />
    </div>
    <div>
      <label>Страна</label>
      <input type="text" v-model="country" />
    </div>
    <div>
      <label>Область</label>
      <input type="text" v-model="region" />
    </div>
    <div>
      <label>Город*</label>
      <input
        type="text"
        v-model="city"
        @blur="$v.city.$touch()"
        :class="{ errorValid: $v.city.$error }"
      />
      <span v-if="$v.city.$error">Поле обязательное для заполнения</span>
    </div>
    <div>
      <label>Улица</label>
      <input type="text" v-model="street" />
    </div>
    <div>
      <label>Дом</label>
      <input type="text" v-model="houseNumber" />
    </div>
    <h3>Паспорт:</h3>
    <div>
      <label>Тип документа*</label>
      <select
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
      <span v-if="$v.documentType.$error"
        >Поле обязательное для заполнения</span
      >
    </div>
    <div>
      <label>Серия</label>
      <input type="number" v-model="documentSeries" />
    </div>
    <div>
      <label>Номер</label>
      <input type="number" v-model="documentNumber" />
    </div>
    <div>
      <label>Кем выдан</label>
      <input type="text" v-model="lssuedBy" />
    </div>
    <div>
      <label for="date">Дата выдачи*</label>
      <input
        type="date"
        id="date"
        name="date"
        v-model="dateOfIssue"
        @blur="$v.dateOfIssue.$touch()"
        :class="{ errorValid: $v.dateOfIssue.$error }"
      />
      <span v-if="$v.dateOfIssue.$error">Поле обязательное для заполнения</span>
    </div>
    <input type="submit" value="Submit" />
  </form>
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
/* валидация */
.errorValid {
  border-color: red;
}</style
>>

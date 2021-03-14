<template>
  <div id="app">
    <form @submit.prevent="checkForm" novalidate v-if="!showSuccess">
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
        <span v-if="$v.dateOfIssue.$error"
          >Поле обязательное для заполнения</span
        >
      </div>
      <input type="submit" value="Submit" />
    </form>

    <div v-else>
      Новый клиент успешно создан
    </div>
    <!-- <div>
      <table class="table table-bordered">
        <tr>
          <td>Фамилия</td>
          <td>{{ lastName }}</td>
        </tr>
        <tr>
          <td>Имя</td>
          <td>{{ firstName }}</td>
        </tr>
        <tr>
          <td>Отчество</td>
          <td>{{ middleName }}</td>
        </tr>
        <tr>
          <td>Дата рождения</td>
          <td>{{ birthday }}</td>
        </tr>
        <tr>
          <td>Номер телефона</td>
          <td>{{ phone }}</td>
        </tr>
        <tr>
          <td>Пол</td>
          <td>{{ sex }}</td>
        </tr>
        <tr>
          <td>Группа клиентов</td>
          <td>{{ customerGroup }}</td>
        </tr>
        <tr>
          <td>Лечащий врач</td>
          <td>{{ attendingDoctor }}</td>
        </tr>
        <tr>
          <td>Не отправлять СМС</td>
          <td>{{ notSMS }}</td>
        </tr>
        <tr>
          <td>Индекс</td>
          <td>{{ index }}</td>
        </tr>
        <tr>
          <td>Страна</td>
          <td>{{ country }}</td>
        </tr>
        <tr>
          <td>Область</td>
          <td>{{ region }}</td>
        </tr>
        <tr>
          <td>Город</td>
          <td>{{ city }}</td>
        </tr>
        <tr>
          <td>Улица</td>
          <td>{{ street }}</td>
        </tr>
        <tr>
          <td>Дом</td>
          <td>{{ houseNumber }}</td>
        </tr>
        <tr>
          <td>Тип документа</td>
          <td>{{ documentType }}</td>
        </tr>
        <tr>
          <td>Серия</td>
          <td>{{ documentSeries }}</td>
        </tr>
        <tr>
          <td>Номер</td>
          <td>{{ documentNumber }}</td>
        </tr>
        <tr>
          <td>Кем выдан</td>
          <td>{{ lssuedBy }}</td>
        </tr>
        <tr>
          <td>Дата выдачи</td>
          <td>{{ dateOfIssue }}</td>
        </tr>
      </table>
    </div> -->
  </div>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";
const checkFirstLetter = (value) => value[0] == 7;
export default {
  name: "App",
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
      showSuccess: false,
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
        console.log("ok");
        this.showSuccess = true;
      }
    },
  },
};
</script>

<style scoped>
/* валидация */
.errorValid {
  border-color: red;
}
</style>

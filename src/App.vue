<template>
  <div id="app">
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
        <!-- <pre>{{ $v.lastName }}</pre> -->
      </div>
      <div>
        <label>Имя*</label>
        <input v-model="firstName" type="text" />
      </div>
      <div>
        <label>Отчество</label>
        <input v-model="middleName" type="text" />
      </div>
      <div>
        <label for="date">Дата рождения*: </label>
        <input type="date" id="date" name="date" v-model="birthday" />
      </div>
      <div>
        <label>Номер телефона*</label>
        <input
          v-model="phone"
          @blur="$v.phone.$touch()"
          :class="{ errorValid: $v.phone.$error }"
          type="number"
        />
        <span v-if="$v.phone.$error">Поле обязательное для заполнения</span>
        <!-- <pre>{{ $v.phone }}</pre> -->
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
        <select size="3" multiple name="" v-model="customerGroup">
          <option value="VIP">VIP</option>
          <option value="Проблемные">Проблемные</option>
          <option value="ОМС">ОМС</option>
        </select>
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
        <input type="number" v-model="index" />
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
        <input type="text" v-model="city" />
      </div>
      <div>
        <label>Улица</label>
        <input type="text" v-model="street" />
      </div>
      <div>
        <label>Дом</label>
        <input type="number" v-model="houseNumber" />
      </div>
      <h3>Паспорт:</h3>
      <div>
        <label>Тип документа*</label>
        <select size="3" name="" v-model="documentType">
          <option value="Паспорт">Паспорт</option>
          <option value="Свидетельство о рождении">
            Свидетельство о рождении
          </option>
          <option value="Вод. удостоверение">Вод. удостоверение</option>
        </select>
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
        <input type="date" id="date" name="date" v-model="dateOfIssue" />
      </div>
      <input type="submit" value="Submit" />
    </form>

    <hr />
    <div>
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
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
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
      // valName: "validatorName",
    };
  },
  validations: {
    lastName: {
      required,
    },
    // firstName: {
    //   required,
    // },
    // birthday: {
    //   required,
    // },
    phone: {
      required,
      // minLength: minLength(11),
      // maxLength: maxLength(11),
      checkFirstLetter,
    },
    // customerGroup: {
    //   required,
    // },
    // city: {
    //   required,
    // },
    // documentType: {
    //   required,
    // },
    // dateOfIssue: {
    //   required,
    // },
  },
  methods: {
    checkForm() {
      this.$v.$touch();
      if (!this.$v.$error) {
        console.log("ok");
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

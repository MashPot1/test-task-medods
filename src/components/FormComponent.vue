<template>
  <form @submit.prevent="submitForm">
    <div :class="screenWidth > 800 ? 'row' : ''">
      <label>Фамилия:*</label>
      <input v-model="surname" required />

      <label>Имя:*</label>
      <input v-model="firstName" required />
    </div>

    <label>Отчество:</label>
    <input v-model="patronymic" />

    <div :class="screenWidth > 800 ? 'row' : ''">
      <label>Дата рождения:*</label>
      <input type="date" v-model="birthDate" required />

      <label>Номер телефона:*</label>
      <input v-model="phoneNumber" pattern="7[0-9]{10}" required />
    </div>

    <div :class="screenWidth > 800 ? 'row' : ''">
      <label>Не отправлять СМС</label>
      <input type="checkbox" v-model="noSMS" />
    </div>

    <label>Пол:</label>
    <select v-model="gender">
      <option value="male">Мужской</option>
      <option value="female">Женский</option>
    </select>

    <label v-if="screenWidth > 800"
      >Группа клиентов:* (выбор нескольких вариантов можно с помощью зажатия
      Ctrl)</label
    >
    <label v-else>Группа клиентов:* </label>
    <select v-model="clientGroup" multiple required>
      <option value="VIP">VIP</option>
      <option value="Проблемные">Проблемные</option>
      <option value="ОМС">ОМС</option>
    </select>

    <label>Лечащий врач:</label>
    <select v-model="attendingDoctor">
      <option value="Иванов">Иванов</option>
      <option value="Захаров">Захаров</option>
      <option value="Чернышева">Чернышева</option>
    </select>

    <div :class="screenWidth > 800 ? 'row' : ''">
      <label>Индекс:</label>
      <input v-model="location.index" />

      <label>Страна:</label>
      <input v-model="location.country" />

      <label>Область:</label>
      <input v-model="location.region" />
    </div>

    <div :class="screenWidth > 800 ? 'row' : ''">
      <label>Город:*</label>
      <input v-model="location.city" required />

      <label>Улица:</label>
      <input v-model="location.street" />

      <label>Дом:</label>
      <input v-model="location.house" />
    </div>

    <label>Тип документа:*</label>
    <select v-model="document.type" required>
      <option value="Паспорт">Паспорт</option>
      <option value="Свидетельство о рождении">Свидетельство о рождении</option>
      <option value="Водительское удостоверение">
        Водительское удостоверение
      </option>
    </select>

    <div :class="screenWidth > 800 ? 'row' : ''">
      <label>Серия:</label>
      <input v-model="document.series" />

      <label>Номер:</label>
      <input v-model="document.number" />
    </div>

    <div :class="screenWidth > 800 ? 'row' : ''">
      <label>Кем выдан:</label>
      <input v-model="document.whoIssued" />

      <label>Дата выдачи:*</label>
      <input type="date" v-model="document.dateOfIssue" required />
    </div>

    <button type="submit">Создать Клиента</button>
  </form>
</template>

<script>
import { required } from "@vuelidate/validators";

export default {
  data() {
    return {
      surname: "",
      firstName: "",
      patronymic: "",
      birthDate: "",
      phoneNumber: "",
      gender: "",
      clientGroup: [],
      attendingDoctor: "",
      location: {
        index: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
      },
      document: {
        type: "",
        series: "",
        number: "",
        whoIssued: "",
        dateOfIssue: "",
      },
      noSMS: false,
      screenWidth: window.innerWidth,
    };
  },
  validations: {
    surname: { required },
    firstName: { required },
    birthDate: { required },
    phoneNumber: { required },
    location: { city: { required } },
    document: { type: { required }, dateOfIssue: { required } },
  },

  mounted() {
    window.addEventListener("resize", this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    submitForm() {
      alert("Форма успешно отправлена! Данные: " + JSON.stringify(this.$data));
      console.log("Данные формы:", this.$data);
    },
    handleResize() {
      this.screenWidth = window.innerWidth;
    },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

form {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

label {
  display: block;
  margin-top: 10px;
}

input,
select {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

input[type="checkbox"] {
  width: 20px;
  height: 20px;
}

button {
  margin-top: 10px;
  padding: 10px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.row {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row;
  gap: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>

<template>
  <div id="form" class="client">
    <div class="container">
      <p class="note">* Поля обязательны для заполнения</p>
      <br />
      <h5>Общие данные</h5>
      <br />
      <form>
        <div>
          <label for="фамилия">Фаимлия*</label>
          <input
            type="text"
            placeholder="Фаимлия"
            v-model.trim="$v.фамилия.$model"
            :class="{ 'is-invalid': validationStatus($v.фамилия) }"
          />
          <div
            v-if="!$v.фамилия.required"
            class="invalid-feedback"
          >Поле "Фамилия" обязательно для заполнения.</div>
          <label for="имя">Имя*</label>
          <input
            type="text"
            placeholder="Имя"
            v-model.trim="$v.имя.$model"
            :class="{ 'is-invalid': validationStatus($v.имя) }"
          />
          <div
            v-if="!$v.имя.required"
            class="invalid-feedback"
          >Поле "Имя" обязательно для заполнения.</div>
          <label for="отчество">Отчество</label>
          <input type="text" placeholder="Отчество" v-model="отчество" />
        </div>

        <div>
          <label for="дата_рождения">Дата рождения*</label>
          <div>
            <input
              type="date"
              placeholder="Дата рождения"
              v-model.trim="$v.дата_рождения.$model"
              :class="{ 'is-invalid': validationStatus($v.дата_рождения) }"
            />
            <div
              v-if="!$v.дата_рождения.required"
              class="invalid-feedback"
            >Поле "Дата рождения" обязательно для заполнения.</div>
          </div>
        </div>
        <div>
          <label for="номер_телефона">Номер телефона*</label>
          <div>
            <input
              type="tel"
              placeholder="7 *** *** **** "
              v-model.trim="$v.номер_телефона.$model"
              :class="{ 'is-invalid': validationStatus($v.номер_телефона) }"
            />
            <div
              v-if="!$v.номер_телефона.required"
              class="invalid-feedback"
            >Поле "Номер телефона" обязательно для заполнения.</div>
            <div
              v-if="!$v.номер_телефона.numeric"
              class="invalid-feedback"
            >Поле "Номер телефона" должно содержать только цифры</div>
            <div
              v-if="
                !$v.номер_телефона.minLength || !$v.номер_телефона.maxLength
              "
              class="invalid-feedback"
            >Поле "Номер телефона" должно содержаться из 11 цифр.</div>
          </div>
        </div>

        <fieldset>
          <legend>Пол</legend>
          <label for="Мужской">Мужской</label>
          <input type="radio" id="Мужской" value="Мужской" v-model="пол" />

          <label for="Женский">Женский</label>
          <input type="radio" id="Женский" value="Женский" v-model="пол" />
        </fieldset>

        <fieldset>
          <legend>Группа клиентов*</legend>
          <input
            type="checkbox"
            value="VIP"
            id="VIP"
            v-model.trim="$v.группа_клиентов.$model"
            :class="{ 'is-invalid': validationStatus($v.группа_клиентов) }"
          />
          <label for="VIP">VIP</label>
          <input
            type="checkbox"
            value="Проблемный"
            id="Проблемный"
            v-model.trim="$v.группа_клиентов.$model"
            :class="{ 'is-invalid': validationStatus($v.группа_клиентов) }"
          />
          <label for="Проблемный">Проблемный</label>

          <input
            type="checkbox"
            value="ОМС"
            v-model.trim="$v.группа_клиентов.$model"
            :class="{ 'is-invalid': validationStatus($v.группа_клиентов) }"
          />
          <label for="ОМС">ОМС</label>

          <div
            v-if="!$v.группа_клиентов.required"
            class="invalid-feedback"
          >Поле "Группа клиентов" обязательно для заполнения.</div>
        </fieldset>
        <div class="selector">
          <label for="лечащий_врач" class="col-sm-2 col-form-label">Лечащий врач</label>
          <div class="selected-items">
            <select id="лечащий_врач" class="form-control" v-model="лечащийВрач">
              <option v-for="врач in лечащий_врач" :key="врач">{{ врач }}</option>
            </select>
          </div>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            value="true"
            id="отправить_sms"
            v-model="отправить_sms"
          />
          <label class="form-check-label" for="отправить_sms">Отправить SMS</label>
        </div>

        <hr />
        <h5>Адрес</h5>
        <br />
        <div>
          <div>
            <input type="text" placeholder="Индекс" v-model="индекс" />
          </div>
          <div>
            <input type="text" placeholder="Страна" v-model="страна" />
          </div>
          <div>
            <input type="text" placeholder="Область" v-model="область" />
          </div>
          <div>
            <input
              type="text"
              placeholder="Город*"
              v-model.trim="$v.город.$model"
              :class="{ 'is-invalid': validationStatus($v.город) }"
            />
            <div
              v-if="!$v.город.required"
              class="invalid-feedback"
            >Поле "Город" обязательно для заполнения.</div>
          </div>
          <div>
            <input type="text" placeholder="Улица" v-model="улица" />
          </div>
          <div>
            <input type="text" placeholder="Дом" v-model="дом" />
          </div>
        </div>
        <hr />
        <h5>Паспорт</h5>
        <br />
        <div class="selector">
          <label for="тип_документа">Тип документа*</label>
          <div class="selected-items">
            <select
              id="тип_документа"
              v-model.trim="$v.типдокумента.$model"
              :class="{ 'is-invalid': validationStatus($v.типдокумента) }"
            >
              <option v-for="документ in тип_документа" :key="документ">{{ документ }}</option>
            </select>
          </div>
          <div
            v-if="!$v.типдокумента.required"
            class="invalid-feedback"
          >Поле "Тип документа" обязательно для заполнения.</div>
        </div>

        <div>
          <input type="text" class="form-control" placeholder="Серия" v-model="серия" />
        </div>
        <div>
          <input type="text" class="form-control" placeholder="Номер" v-model="номер" />
        </div>

        <div>
          <input type="text" placeholder="Kем выдан" v-model="кем_выдан" />
        </div>

        <div>
          <label for="Дата Выдачи">Дата выдачи*</label>

          <input
            type="date"
            placeholder="Дата выдачи"
            v-model.trim="$v.дата_выдачи.$model"
            :class="{ 'is-invalid': validationStatus($v.дата_выдачи) }"
          />
          <div
            v-if="!$v.дата_выдачи.required"
            class="invalid-feedback"
          >Поле "Дата выдачи" обязательно для заполнения.</div>
        </div>

        <div>
          <div>
            <button type="submit" class @submit.prevent="submit">Создать</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import {
  required,
  numeric,
  minLength,
  maxLength,
} from "vuelidate/lib/validators";

export default {
  data() {
    return {
      фамилия: "",
      имя: "",
      отчество: "",
      дата_рождения: "",
      номер_телефона: "",
      пол: "Мужской",

      группа_клиентов: [],
      лечащийВрач: "Захаров",
      лечащий_врач: ["Чернишова", "Иванов", "Захаров"],

      индекс: "",
      страна: "",
      область: "",
      город: "",
      улица: "",
      дом: "",

      типдокумента: "",
      тип_документа: [
        "Паспорт",
        "Свидетельство о рождении",
        "Водительское удостоверение",
      ],
      серия: "",
      номер: "",
      кем_выдан: "",
      дата_выдачи: "",

      отправить_sms: true,
    };
  },

  validations: {
    фамилия: { required },
    имя: { required },
    дата_рождения: { required },
    номер_телефона: {
      required,
      numeric,
      minLength: minLength(11),
      maxLength: maxLength(11),
    },
    группа_клиентов: { required },
    город: { required },
    типдокумента: { required },
    дата_выдачи: { required },
  },
  methods: {
    validationStatus(validation) {
      return typeof validation != "undefined" ? validation.$error : false;
    },
    submit() {
      this.$v.$touch();
      if (this.$v.$pendding || this.$v.$error) return;
      alert("клиент создан");
    },
  },
};
</script>

<style lang="scss" scoped>
.client {
  border: 1px solid #ccc;
  border-radius: 25px;
  box-shadow: 1px 1px 2px #4d5d75;
  background-color: #f7f7f7;
  font-size: 1em;
  margin: 2em auto;
  padding: 2em;
  width: 70%;
  input,
  select {
    outline: none;
  }
  label {
    padding: 0 0.5em 0 0.5em;
    margin-top: 0.3em;
  }
  .container {
    margin: auto;
    justify-content: start;
    width: 90%;
  }
  .note {
    color: #ff2768;
    text-align: right;
    margin-right: 4px;
  }
  h5 {
    text-align: center;
    font-size: 1.2em;
  }
  fieldset {
    margin-bottom: 2em;
    padding: 0.5em 0.7em;
    border-radius: 25px;
  }
  input {
    font-family: Georgia, "Times New Roman", Times, serif;
    border-radius: 25px;
    font-size: 1.1em;
    margin: 0.2em 0;
    padding: 0.5em;
    width: 100%;
    background-color: #fff;
    border: 1px solid #ddd;
  }
  input[type="radio"] {
    appearance: none;
    border-radius: 2em;
    background-color: #fff;
    cursor: pointer;
    height: 0.7em;
    width: 0.7em;
    margin-top: 0;
    vertical-align: text-top;
  }
  input[type="radio"]:checked:after {
    background-color: black;
    content: "\00a0";
    border-radius: 1em;
    display: block;
    position: relative;
    height: 0.4em;
    width: 0.4em;
  }
  .selected-items {
    display: inline-block;
    background-color: #fff;
    cursor: pointer;
    font-size: 1.1em;
    margin-bottom: 1.5em;
    padding: 0.25em 0;
    position: relative;
    width: 15em;
  }

  select {
    appearance: none;
    background-color: transparent;
    border: none;
    cursor: pointer;
    color: black;
    display: inline-block;
    font-size: 1em;
    margin: 0;
    padding: 0 1em 0 1em;
    width: 100%;
  }
  .invalid-feedback {
    position: relative;
    color: #ff2768;
    font-size: 0.7rem;
    margin-bottom: 0.7em;
    top: 0em;
  }
  input[type="checkbox"] {
    appearance: none;

    background-color: #fff;
    cursor: pointer;
    font-size: 1em;
    padding: 0.25em;
    height: 1em;
    width: 1em;
    vertical-align: text-top;
  }
  input[type="checkbox"]:checked:after {
    border: solid black;
    border-width: 0 4px 4px 0;
    content: "\00a0";
    display: block;
    height: 1em;
    width: 0.5em;
    margin-top: -0.9em;
    position: relative;
    transform: rotate(45deg);
  }
  button {
    border-radius: 25px;
    font-family: Georgia, "Times New Roman", Times, serif;
    box-shadow: inset 0 0 0 3px #4d5d75;
    background-color: #f7f7f7;
    cursor: pointer;
    color: black;
    float: right;
    font-size: 1.5em;
    padding: 0.25em 1em;
  }
  button:hover {
    background-color: #4d5d75;
    color: #f7f7f7;
  }
}
</style>
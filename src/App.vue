<template>
  <div id="app">
    <header>
      <h1>Создание нового клиента</h1>
    </header>

    <form @submit.prevent="submit">
      <div class="attributes">
        <div class="labels">
          <label for="surname" class="desktopLabels">Фамилия<span>*</span>:</label>
          <label for="name" class="desktopLabels">Имя<span>*</span>:</label>
          <label for="patron" class="desktopLabels">Отчество:</label>
          <label for="dateBirthday" class="desktopLabels">День рождения<span>*</span>:</label>
          <label for="phone" class="desktopLabels">Номер телефона<span>*</span>:</label>
          <label for="sex" class="desktopLabels">Пол:</label>
          <label for="group-clients" class="desktopLabels">Группа клиентов:</label>
          <label for="attending-doctor" class="desktopLabels">Лечащий врач:</label>
          <label for="sms" class="desktopLabels">СМС:</label>
        </div>

        <div class="inputs">
          <div class="surname">
            <input type="text" name="surname" v-model="$v.surname.$model">
            <div class="error" v-if="!$v.surname.required">Обязательно к заполнению!!!</div>
            <div class="error" v-if="!$v.surname.minLength">Должно содержать как минимум {{ $v.surname.$params.minLength.min }} знака.</div>
          </div>

          <div class="name">
            <input type="text" name="name" v-model="$v.name.$model">
            <div class="error" v-if="!$v.name.required">Обязательно к заполнению!!!</div>
            <div class="error" v-if="!$v.name.minLength">Должно содержать как минимум {{ $v.name.$params.minLength.min }} знака.</div>
          </div>

          <div class="patron">
            <input type="text" name="patron" v-model.lazy="$v.patron.$model">
            <div class="error" v-if="!$v.patron.minLength">Должно содержать как минимум {{ $v.patron.$params.minLength.min }} знаков.</div>
          </div>

          <div class="dateBirthday">
            <input type="date" name="dateBirthday" id="" v-model="$v.dateBirthday.$model">
            <div class="error" v-if="!$v.dateBirthday.required">Обязательно к заполнению!!!</div>
          </div>

          <div class="phone">
            <input type="tel" name="phone" id="" v-model="$v.phone.$model" placeholder="70000000000" pattern="[0-9]{11}">
            <div class="error" v-if="!$v.phone.required">Обязательно к заполнению!!!</div>
            <div class="error" v-if="!$v.phone.numeric">Только цифры!</div>
            <div class="error" v-if="!$v.phone.minLength || !$v.phone.maxLength">Номер должен содержать ровно {{ $v.phone.$params.minLength.min }} цифр.</div>
          </div>

          <div class="sex">
            <input type="radio" name="sex" id="male" value="Мужской" v-model="sex">Мужской
            <input type="radio" name="sex" id="female" value="Женский" v-model="sex">Женский
          </div>

          <div class="groupClients">
            <select id="group-clients" name="group-clients" size="4" v-model="$v.groupClient.$model" multiple>
              <option disabled value="">Выберите один или несколько вариантов</option>
              <option>VIP</option>
              <option>Проблемные</option>
              <option>ОМС</option>
            </select>
            <div class="error" v-if="!$v.groupClient.required">Обязательно к заполнению!!!</div>
          </div>

          <div class="attendingDoctor">
            <select id="attending-doctor" name="attending-doctor" v-model="attendingDoctor">
              <option disabled value="">Выберите один из вариантов</option>
              <option>Иванов</option>
              <option>Захаров</option>
              <option>Чернышёва</option>
            </select>
          </div>

          <input type="checkbox" name="sms" id="sms" v-model="sms">Не отправлять СМС
        </div>
      </div>

      <div class="adress">
        <div class="labels">
          <label for="index" class="desktopLabels">Индекс:</label>
          <label for="country" class="desktopLabels">Страна:</label>
          <label for="region" class="desktopLabels">Регион:</label>
          <label for="city" class="desktopLabels">Город<span>*</span>:</label>
          <label for="street" class="desktopLabels">Улица:</label>
          <label for="home" class="desktopLabels">Дом:</label>
        </div>

        <div class="inputs">
          <div class="index">
            <input type="text" name="index" v-model.lazy="$v.index.$model">
            <div class="error" v-if="!$v.index.minLength || !$v.index.maxLength">Индекс должен содержать ровно {{ $v.index.$params.minLength.min }} цифр.</div>
            <div class="error" v-if="!$v.index.numeric">Только цифры!</div>
          </div>

          <div class="contry">
            <input type="text" name="country" v-model.lazy="$v.country.$model">
            <div class="error" v-if="!$v.country.minLength">Должно содержать как минимум {{ $v.country.$params.minLength.min }} буквы.</div>
          </div>

          <div class="region">
            <input type="text" name="region" v-model.lazy="$v.region.$model">
            <div class="error" v-if="!$v.region.minLength">Должно содержать как минимум {{ $v.region.$params.minLength.min }} буквы.</div>
          </div>

          <div class="city">
            <input type="text" name="city" v-model="$v.city.$model">
            <div class="error" v-if="!$v.city.required">Обязательно к заполнению!!!</div>
            <div class="error" v-if="!$v.city.minLength">Должно содержать как минимум {{ $v.city.$params.minLength.min }} буквы.</div>
          </div>

          <div class="street">
            <input type="text" name="street" v-model.lazy="$v.street.$model">
            <div class="error" v-if="!$v.street.minLength">Должно содержать как минимум {{ $v.street.$params.minLength.min }} буквы.</div>
          </div>

          <div class="home">
            <input type="text" name="home" v-model.lazy="$v.home.$model">
            <div class="error" v-if="!$v.home.minLength">Должно содержать как минимум {{ $v.home.$params.minLength.min }} буквы.</div>
          </div>
        </div>
      </div>

      <div class="documentInformation">

        <div class="labels">
          <label for="typeDocument" class="desktopLabels">Тип документа<span>*</span>:</label>
          <label for="serialDocument" class="desktopLabels">Серия:</label>
          <label for="numberDocument" class="desktopLabels">Номер:</label>
          <label for="issued" class="desktopLabels">Кем выдан:</label>
          <label for="dateIssued" class="desktopLabels">Дата выдачи<span>*</span>:</label>
        </div>

        <div class="inputs">
          <div class="document">
            <select id="typeDocument" name="typeDocument" v-model="$v.typeDocument.$model">
              <option disabled value="">Выберите один из вариантов</option>
              <option>Паспорт</option>
              <option>Свидетельство о рождении</option>
              <option>Водительское удостоверение</option>
            </select>
            <div class="error" v-if="!$v.typeDocument.required">Обязательно к заполнению!!!</div>
          </div>

          <div class="serialDocument">
            <input type="text" name="serialDocument" v-model.lazy="$v.serialDocument.$model">
            <div class="error" v-if="!$v.serialDocument.minLength">Должно содержать как минимум {{ $v.serialDocument.$params.minLength.min }} знака.</div>
          </div>

          <div class="numberDocument">
            <input type="text" name="numberDocument" v-model.lazy="$v.numberDocument.$model">
            <div class="error" v-if="!$v.numberDocument.minLength">Должно содержать как минимум {{ $v.numberDocument.$params.minLength.min }} знаков.</div>
          </div>

          <div class="issued">
            <input type="text" name="issued" v-model.lazy="$v.issued.$model">
            <div class="error" v-if="!$v.issued.minLength">Должно содержать как минимум {{ $v.issued.$params.minLength.min }} знаков.</div>
          </div>

          <div class="dateIssued">
            <input type="date" name="dateIssued" id="" v-model="$v.dateIssued.$model">
            <div class="error" v-if="!$v.dateIssued.required">Обязательно к заполнению!!!</div>
          </div>
        </div>
      </div>

      <div class="submit">
        <input class="button" type="submit" value="Отправить" :disabled="submitStatus === 'PENDING'">
        <p class="typo__p" v-if="submitStatus === 'OK'">Новый клиент успешно создан!</p>
        <p class="typo__p" v-if="submitStatus === 'ERROR'">Пожалуйста заполните корректно все требуемые поля!</p>
        <p class="typo__p" v-if="submitStatus === 'PENDING'">Создание нового клиента...</p>
      </div>
    </form>
  </div>
</template>

<script>
import { required, minLength, maxLength, numeric } from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      surname: null,
      name: null,
      patron: null,
      dateBirthday: null,
      phone: null,
      sex: 'Мужской',
      groupClient: [],
      attendingDoctor: '',
      sms: false,
      index: null,
      country: null,
      region: null,
      city: null,
      street: null,
      home: null,
      typeDocument: '',
      serialDocument: null,
      numberDocument: null,
      issued: null,
      dateIssued: null,
      submitStatus: null
    }
  },
  validations: {
    surname: {
      required,
      minLength: minLength(3)
    },
    name: {
      required,
      minLength: minLength(2)
    },
    patron: {
      minLength: minLength(5)
    },
    dateBirthday: {
      required
    },
    phone: {
      required,
      numeric,
      minLength: minLength(11),
      maxLength: maxLength(11)
    },
    groupClient: {
      required
    },
    index: {
      numeric,
      minLength: minLength(6),
      maxLength: maxLength(6)
    },
    country: {
      minLength: minLength(3)
    },
    region: {
      minLength: minLength(4)
    },
    city: {
      required,
      minLength: minLength(2)
    },
    street: {
      minLength: minLength(5)
    },
    home: {
      minLength: minLength(2)
    },
    typeDocument: {
      required
    },
    serialDocument: {
      minLength: minLength(2)
    },
    numberDocument: {
      numeric,
      minLength: minLength(6)
    },
    issued: {
      minLength: minLength(6)
    },
    dateIssued: {
      required
    }
  },
  methods: {
    submit () {
      this.$v.$touch()
      if (this.$v.$error) {
        this.submitStatus = 'ERROR'
      } else {
        this.submitStatus = 'PENDING'
        setTimeout(() => {
          this.submitStatus = 'OK'
        }, 500)
      }
    }
  }
}
</script>

<style lang="scss">

body {
  margin: 0;
}

header {
  display: flex;
  background-color: #3dafcb;
  h1 {
    color: #ffffff;
    margin-left: 25px;
  }
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.attributes, .adress, .documentInformation {
  display: flex;
}

.labels {
  display: flex;
  flex-direction: column;
  background-color: #f6f6f6;
  border-right: 1px solid #cdcdcd;
}

input {
  border-radius: 5px;
}

.desktopLabels span, .error {
  color: red;
}

</style>

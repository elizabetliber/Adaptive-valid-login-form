<template>
  <div id="app">
    <div>
      <div class="container">
        <form @submit.prevent="checkForm">
          <div class="row">
            <h3>Личные данные:</h3>
          </div>

          <div class="row">
            <div class="col-25">
              <label for="lastName">Фамилия<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <input
                  id="lastname"
                  v-model.trim="form.lastName"
                  type="text"
                  placeholder="Введите фамилию">
              <strong v-if="$v.form.lastName.$dirty && !$v.form.lastName.required">
                * Заполните поле фамилия.
              </strong>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label for="name">Имя<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <input
                  id="name"
                  v-model.trim="form.name"
                  type="text"
                  name="name"
                  placeholder="Введите имя">
              <strong v-if="$v.form.name.$dirty && !$v.form.name.required">
                * Заполните поле имя.
              </strong>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Отчество</label>
            </div>
            <div class="col-75">
              <input
                  type="text"
                  placeholder="Введите отчество"/>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label for="data">Дата рождения<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <input
                  type="date"
                  v-model="form.data"
                  id="data"
              />
              <strong v-if="$v.form.data.$dirty && !$v.form.data.required">
                * Заполните поле дата.
              </strong>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label for="number">Номер телефона<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <input
                  type="text"
                  v-model.trim="form.number"
                  id="number"
              />
              <strong v-if="$v.form.number.$dirty && !$v.form.number.required">
                * Заполните поле номер телефона.
              </strong>
              <strong v-if="$v.form.number.$dirty && !$v.form.number.numeric">
                * Укажите корректный номер в формате: +7(903)-888-88-88 или 8(999)-99-999-99)
              </strong>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Пол</label>
            </div>
            <div class="col-75">
              <select>
                <option disabled value="">Выберите один из вариантов</option>
                <option>Мужской</option>
                <option>Женский</option>
              </select>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Группа клиентов<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <select v-model="form.group" multiple>
                <option disabled value="">Выберите несколько вариантов</option>
                <option v-for="(group,index) in form.groupClient"
                        :key="index"
                >
                  {{ group.label }}
                </option>
              </select>
              {{ form.group }}
              <strong v-if="$v.form.group.$dirty && !$v.form.group.maxCount">
                * Выберите два варианта из предложенных.
              </strong>
              <strong v-if="$v.form.group.$dirty && !$v.form.group.required">
                * Заполните поле группа клиентов.
              </strong>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Лечащий врач</label>
            </div>
            <div class="col-75">
              <select>
                <option disabled value="">Выберите один из вариантов</option>
                <option>Иванов</option>
                <option>Захаров</option>
                <option>Чернышева</option>
              </select>
            </div>
          </div>


          <div class="row">
            <input type="checkbox"
                   checked="checked"> Не отправлять СМС
          </div>

          <div class="row">
            <h3>Адрес:</h3>
          </div>
          <div class="row">
            <div class="col-25">
              <label>Индекс</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder="Индекс">
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Страна</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder="Страна">
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Область</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder="Область"/>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label for="city">Город<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <input
                  type="text"
                  v-model="form.city"
                  placeholder="Город"
                  id="city"
              >
              <strong v-if="$v.form.city.$dirty && !$v.form.city.required">
                * Заполните поле город.
              </strong>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Улица</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder="Улица"/>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Дом</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder="Дом"/>
            </div>
          </div>
          <div class="row">
            <h3>Паспорт:</h3>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Тип документа<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <select v-model="form.selected">
                <option disabled value="">Выберите один из вариантов</option>
                <option v-for="(selected,index) in form.typeDocument"
                        :key="index"
                >
                  {{ selected.type }}
                </option>
              </select>
              <strong v-if="$v.form.selected.$dirty && !$v.form.selected.required">
                * Заполните поле тип документа.
              </strong>
            </div>

          </div>
          <div class="row">
            <div class="col-25">
              <label>Серия</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder=""/>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Номер</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder=""/>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label>Кем выдан</label>
            </div>
            <div class="col-75">
              <input type="text" placeholder=""/>
            </div>
          </div>

          <div class="row">
            <div class="col-25">
              <label for="dateDocument">Дата выдачи<sup style="color:red;">*</sup></label>
            </div>
            <div class="col-75">
              <input
                  type="date"
                  placeholder=""
                  v-model="form.dateDocument"
                  id="dateDocument"
              >
              <strong v-if="$v.form.dateDocument.$dirty && !$v.form.dateDocument.required">
                * Заполните поле дата выдачи.
              </strong>
            </div>
          </div>
          <div class="row">
            <h4><em style="color:red;">*</em> Поле обязательное для заполнения.</h4>
          </div>

          <div class="row">
            <input type="submit" value="Подтвердить"/>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import {validationMixin} from 'vuelidate'
import {required} from 'vuelidate/lib/validators'

const numeric = value => {
  if (typeof value === 'undefined' || value === null || value === '') {
    return true
  }
  return /^\+?[78][-(]?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$/.test(value)
}

export default {
  mixins: [validationMixin],
  data() {
    return {
      form: {
        lastName: '',
        name: '',
        data: '',
        number: '',
        group: [],
        selected: [],
        typeDocument: [
          {type: 'Паспорт'},
          {type: 'Свидетельство о рождении'},
          {type: 'Водительское удостоверение'}
        ],
        groupClient: [
          {label: 'VIP'},
          {label: 'Проблемные'},
          {label: 'ОМС'}
        ],
        city: '',
        dateDocument: ''
      }
    }
  },
  validations: {
    form: {
      lastName: {required},
      name: {required},
      data: {required},
      number: {required, numeric},
      selected: {required},
      city: {required},
      dateDocument: {required},
      group: {required,
        maxCount(value) {
          return value.length < 2
        }
      }
    }
  },
  methods: {
    checkForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        alert('Валидация прошла успешно')
      }
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

input[type=text], input[type=date], select {
  width: 100%;
  padding: 12px;
  border: 1px solid lightsteelblue;
  border-radius: 4px;
  box-sizing: border-box;
  resize: vertical;
}

label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}

input[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  float: right;
}

.container {

  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}

.col-25 {
  float: left;
  width: 25%;
  margin-top: 6px;
}

.col-75 {
  text-align: right;
  float: left;
  width: 75%;
  margin-top: 6px;
}

.row:after {
  content: "";
  display: table;
  clear: both;
}

@media screen and (max-width: 600px) {
  .col-25, .col-75, input[type=submit] {
    width: 100%;
    margin-top: 0;
  }
}

.row {
  clear: both;
  text-align: right;
}

strong {
  color: red;
  font-size: 13px;
}
</style>

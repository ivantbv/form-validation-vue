<template>
    <div class="register container">
        <form class="card-panel green-text" @submit.prevent="registerClient" novalidate>

            <div id="myModal" class="modal">
            <div class="modal-content">
            <span class="close">&times;</span>
            <p>Новый клиент успешно создан! ✔</p>
            </div>
            </div>

            <h2>Регистрация Клиента</h2>

             <div class="field">
                <label for="surname">Фамилия*</label>
                <input type="text" id="surname" v-model="register.surname" placeholder="Ведите фамилию"
                @blur="$v.register.surname.$touch()">
                <template v-if="$v.register.surname.$error">
                    <p class="error-message" v-if="!$v.register.surname.required">Пожалуйста, введите фамилию*</p>
                </template>
            </div>

            <div class="field">
                <label for="name">Имя*</label>
                <input type="text" id="name" v-model="register.name" placeholder="Ведите имя"
                @blur="$v.register.name.$touch()">
                <template v-if="$v.register.name.$error">
                    <p class="error-message" v-if="!$v.register.name.required">Пожалуйста, введите имя*</p>
                    <p class="error-message" v-if="!$v.register.name.minLength">Имя должно содержать 2 или больше знаков*</p>
                </template>
            </div>

            <div class="field">
                <label for="patronymic">Отчество</label>
                <input type="text" id="patronymic" placeholder="Ведите отчество"
                >
            </div>

            <div class="date">
                <label for="date">Дата Рождения*</label>
                <input type="date" id="date" v-model="register.date" class="datepicker"
                required
                @blur="$v.register.date.$touch()">
                <template v-if="$v.register.date.$error">
                    <p class="error-message" v-if="!$v.register.date.required">Пожалуйста, введите дату рождения*</p>
                </template>
            </div>

            <div class="field">
                <label for="phoneNumber">Номер Телефона*</label>
                <input type="text" id="phoneNumber" v-model="register.phoneNumber" placeholder="Ведите номер телефона"
                @blur="$v.register.phoneNumber.$touch()">
                <template v-if="$v.register.phoneNumber.$error">
                    <p class="error-message" v-if="!$v.register.phoneNumber.required">Пожалуйста, укажите номер*</p>
                    <p class="error-message" v-if="!$v.register.phoneNumber.numeric">Номер телефона должен содержать только числа*</p>
                     <p class="error-message" v-if="!$v.register.phoneNumber.only11DigitsLong">Номер телефона должен состоять из 11 цифр*</p>
                <p class="error-message" v-if="!$v.register.phoneNumber.startWith7">Номер телефона должен начинаться на 7*</p>
                </template>
            </div>
            
            <div class="radio">
            <label for="gender">Пол</label> 
                    <label>
                        <input type="radio"  v-model="register.gender" name="gender" value="female"> <div id="f"> Женщина</div> <br>
                    </label>
                    <label>
                        <input type="radio" name="gender" value="male"> <div id="m">Мужчина</div> <br>
                </label>
            </div>

            <div class="select">
               <label for="selected">Группа клиентов*</label> 
           <select v-model="register.selected" name="selected"
            @blur="$v.register.selected.$touch()"
            multiple id="group-clients">
                <option value="VIP">VIP</option>
                <option value="problem">Проблемные</option>
                <option value="OMS">ОМС</option>
                </select>
                <template>
                    <p class="error-message" v-if="$v.register.selected.$error">Пожалуйста, укажите группу*</p>
                </template>
            </div>

            <div class="doctor">
            <label for="doctor">Лечащий врач</label>    
           <select v-model="register.doctor" name="selected"
            @blur="$v.register.doctor.$touch()">
                <option value="Ivanov">Иванов</option>
                <option value="Zaharov">Захаров</option>
                <option value="Chernysheva">Чернышева</option>
                </select>
            </div>

           <link href="https://cdnjs.cloudflare.com/ajax/libs/materialize/0.100.2/css/materialize.min.css" rel="stylesheet" />
            <p id="sms">
            <input type="checkbox" id="check" />
            <label for="check">Не отправлять СМС</label>
            </p>

            <h2>Aдрес</h2>

            <div class="field">
                <label for="index">Индекс</label>
                <input type="number" id="index" v-model="register.index" placeholder="Введите индекс"
                @blur="$v.register.index.$touch()">
            </div>

            <div class="field">
                <label for="country">Страна</label>
                <input type="text" id="country" v-model="register.country" placeholder="Введите страна"
                @blur="$v.register.country.$touch()">
            </div>

            <div class="field">
                <label for="region">Область</label>
                <input type="text" id="region" v-model="register.region" placeholder="Введите область"
                @blur="$v.register.region.$touch()">
            </div>

            <div class="field">
                <label for="location">Город*</label>
                <input type="text" id="location" v-model="register.location" placeholder="Ведите город"
                @blur="$v.register.location.$touch()">
                <template v-if="$v.register.location.$error">
                    <p class="error-message" v-if="!$v.register.location.required">Пожалуйста, укажите город*</p>
                </template>
            </div>

            <div class="field">
                <label for="street">Улица</label>
                <input type="text" id="street" v-model="register.street" placeholder="Введите улица"
                @blur="$v.register.street.$touch()">
            </div>

            <div class="field">
                <label for="home">Дом</label>
                <input type="text" id="home" v-model="register.home" placeholder="Введите дом"
                @blur="$v.register.home.$touch()">
            </div>

            <h2>Паспорт</h2>

             <div class="select">
               <label for="docType">Тип документа*</label> 
           <select v-model="register.docType" name="docType"
            @blur="$v.register.docType.$touch()"
            id="docType">
                <option value="passport">Паспорт</option>
                <option value="birth-cert">Свидетельство о рождении</option>
                <option value="drivers-license">Вод. удостоверение</option>
                </select>
                <template>
                    <p class="error-message" v-if="$v.register.docType.$error">Пожалуйста, укажите документ*</p>
                </template>
            </div>

            <div class="field">
                <label for="series">Серия</label>
                <input type="number" id="series" v-model="register.series" placeholder="Введите серия"
                @blur="$v.register.series.$touch()">
            </div>

            <div class="field">
                <label for="num">Номер</label>
                <input type="number" id="num" v-model="register.num" placeholder="Введите номер"
                @blur="$v.register.num.$touch()">
            </div>

            <div class="field">
                <label for="issuedBy">Кем выдан</label>
                <input type="text" id="issuedBy" v-model="register.issuedBy" placeholder="Введите кем выдан"
                @blur="$v.register.issuedBy.$touch()">
            </div>

            <div class="date">
                <label for="issuedDate">Дата выдачи*</label>
                <input type="date" id="date" v-model="register.issuedDate" class="datepicker"
                required
                @blur="$v.register.issuedDate.$touch()">
                <template v-if="$v.register.issuedDate.$error">
                    <p class="error-message" v-if="!$v.register.issuedDate.required">Пожалуйста, введите дату выдачи документа*</p>
                </template>
            </div>

            <div class="field center">
                <button class="btn blue" :disabled="$v.$invalid">
                    Регистрация
                </button>
            </div>

        </form>
    </div>
</template>

<script>
import {required, minLength, numeric} from 'vuelidate/lib/validators'
// import * as ModalSuccess from '../assets/ModalSuccess.js'
export default {
    name: 'Register',
    data() {
        return {
            register: {
                surname: '',
                name: '',
                date: '',
                phoneNumber: '',
                gender: '',
                selected: [],
                doctor: [],
                sms: '',
                index: '',
                country: '',
                region: '',
                location: '',
                street: '',
                home: '',
                docType: [],
                series: '',
                num: '',
                issuedBy: '',
                issuedDate: '', 
            },
            feedback: ''
        }
    },
    methods: {
        registerClient(e) {
            this.$v.$touch();
            if (!this.$v.$invalid) {
                this.modal = document.getElementById("myModal");
                this.modalSpan = document.getElementsByClassName("close")[0]; 
                
                this.modal.style.display = "block";
               
                this.modalSpan.addEventListener('click', () => {
                this.modal.style.display = "none";
                })

                 window.addEventListener('click', (e) => {
                    if (e.target == this.modal) {
                    this.modal.style.display = "none";
                    }
                })
                
            }
        }
    },
    validations: {
        register: {
            surname: {
                required,
            },
            name: {
                required,
                minLength: minLength(2),
            },
            date: {
                required,
            },
            phoneNumber: {
                required,
                numeric,
                only11DigitsLong(value) {
                    return value.trim().length === 11;
                },
                startWith7(value) {
                    return `${value}`.indexOf(7) === 0
                }
            }, 
            gender: {
            },
            selected: {
                required,
            },
            doctor: {
            },
            sms: {
            },
            index: {
                numeric,
            },
            country: {
            },
            region: {
            },
            location: {
                required,
            },
            street: {
            },
            home: {
            },
            docType: {
                required,
            },
            series: {
                numeric,
            },
            num: {
                numeric,
            },
            issuedBy: {
            },
            issuedDate: {
                required,
            }
        }
    }
}
</script>

<style scoped>
    .register {
        max-width: 600px;
        margin-top: 60px;
    }

    .register h2 {
        font-size: 2.4em;
    }

    .register .field {
        margin-bottom: 16px;   
    }

    .error-message {
        color: rgb(236, 79, 79) !important;
    }

    input[type="radio"] {
        opacity: 1;
    }

    .radio {
        display: grid;
    }

    #f, #m {
        padding-top: 10px;
        font-size: 13px;
        color: #4CAF50 !important;
    }

    label {
        font-size: 13px;
    }

    select {
        display: block !important;
        border: 1px solid #311414;
        height: 2.5rem;
    }

    .select {
        padding-bottom: 20px !important;
    }

    .doctor {
        padding-top: 10px;
        padding-bottom: 15px;
    }
    #group-clients {
        height: 5rem;
    }

    #sms {
        text-align: center;
    }

    .modal {
    display: none; 
    position: fixed;
    z-index: 1;
    left: 0;
    overflow: auto;
}
.modal-content {
    background-color: #fefefe;
    margin: auto;
    padding: 20px;
    width: 77%;
  }

  .modal-content p {
      padding-top: 20px;
      padding-bottom: 20px;
      text-align: center;
  }
  
  .close {
    color: #aaaaaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }
  
  .close:hover,
  .close:focus {
    color: #000;
    text-decoration: none;
    cursor: pointer;
  }

/* .green-text {
    color: #415daa !important;
} */
</style>
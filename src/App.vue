<script>
import axios from 'axios';
export default {
    data() {
        return {
            city: '',
            error: "",
            info: null
        }
    },
    computed: {
        cityName() {
            return "<" + this.city + ">"
        },
        showTemp() {
            return "Температура: " + this.info.main.temp
        },
        showFeelslike() {
            return "Ощущается как:" + this.info.main.feels_like
        },
        showMinTemp() {
            return "Минимальная температура: " + this.info.main.temp_min
        },
        showMaxTemp() {
            return "Максимальная температура: " + this.info.main.temp_max
        }
    },
    methods: {
        getWeather() {
            if(this.city.trim().length < 2) {
                this.error = "Нужно название более одного символа :)"
                return false
            }
            this.error = ""

            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=365782d4e42a8a14299937c2ea9b05ea`)
            .then(res => (this.info = res.data))
        }
    },
}


</script>
<script setup>

</script>

<template>
    <div class="wrapper">
        <h1>Погодные приложение </h1>
        <p>Узнать погоду в {{ city == "" ? "Вашем городе" : cityName }}</p>
        <input type="text" v-model="city" placeholder="Введите город">
        <button v-if="city != ''" @click="getWeather()">Получить погоду</button>
        <button disabled v-else>Введите название города</button>
        <p class="error">{{ error }}</p>

        <div v-if="info != null">
        <p>{{ showTemp }}</p>
        <p>{{ showFeelslike }}</p>
        <p>{{ showMinTemp }}</p>
        <p>{{ showMaxTemp }}</p>
        </div>
    </div>


</template>

<style scoped>
.error {
    color: red;
}

.wrapper {
    width: 90%;
    max-width: 900px;
    height: auto;
    min-height: 500px;
    border-radius: 50px;
    padding: 20px;
    background: black;
    text-align: center;
    color: wheat;
    margin: 0 auto; /* Center the wrapper */
}

.wrapper h1 {
    margin-top: 20px;
}

.wrapper p {
    margin-top: 20px;
}

.wrapper input {
    width: 80%; /* Responsive width */
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid green;
    color: wheat;
    font-size: 16px; /* Larger font size for better readability */
    padding: 10px 8px;
    outline: none;
}

.wrapper input:focus {
    border-bottom-color: rgb(58, 224, 8);
}

.wrapper button:disabled {
    background: rgb(255, 102, 0);
}

.wrapper button {
    background: orange;
    color: white;
    border-radius: 10px;
    border: 2px solid orange;
    padding: 12px 18px;
    margin-top: 20px; /* Add margin top for better spacing */
    cursor: pointer;
    transition: transform 500ms ease;
}

.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}

/* Media Queries for Tablet */
@media (min-width: 481px) and (max-width: 768px) {
    .wrapper {
        padding: 15px;
        border-radius: 25px;
    }

    .wrapper h1, .wrapper p {
        margin-top: 15px;
    }

    .wrapper input, .wrapper button {
        font-size: 14px;
    }
}

/* Media Queries for Mobile Phones */
@media (max-width: 480px) {
    .wrapper {
        padding: 10px;
        border-radius: 20px;
    }

    .wrapper h1 {
        font-size: 18px; /* Smaller font size for smaller screens */
    }

    .wrapper p {
        font-size: 14px;
    }

    .wrapper input, .wrapper button {
        font-size: 12px;
    }

    .wrapper button {
        padding: 10px 12px;
    }
}

/* Media Queries for Desktop */
@media (min-width: 769px) {
    .wrapper {
        max-width: 1200px; /* Larger max-width for desktop screens */
        padding: 30px; /* More padding for larger screens */
        border-radius: 60px; /* Larger border-radius for aesthetic adjustment */
    }

    .wrapper h1 {
        font-size: 32px; /* Larger font size for desktop */
    }

    .wrapper p {
        font-size: 20px; /* Larger font size for desktop */
    }

    .wrapper input {
        font-size: 18px; /* Larger input font size for better readability */
    }

    .wrapper button {
        padding: 15px 20px; /* Larger padding for buttons */
        font-size: 16px; /* Larger font size for buttons */
    }
}
</style>

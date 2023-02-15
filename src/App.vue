<script>
import axios  from 'axios'
export default{
    data(){
        return{
            city: "",
            error:"",
            info: null
        }
    },
    computed:{
        cityName(){
            return "'"+this.city+"'"
        },
        showTemp(){
            return "Температура: "+this.info
        }
    },
    methods:{ //функция
        clickButt(){
            if(this.city.trim().length<2){
                this.error="Нужное название больше 1 символа"
                return false
            }
            this.error=""
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&APPID=0ccfe09cfacfd5161654a192d2f6bcad`)
                .then(res => (this.info = res.data.main.temp))
        }
    }
}
</script>

<template>
    <div class="wrapper">
        <h1>Погодное приложение</h1>
        <p>Узнать погоду в {{ city==""?"вашем городе": cityName}}</p>
        <input type="text" v-model="city"  placeholder="Введите название города">
        <button v-if="city != ''" @click="clickButt()">Узнать погоду</button>
        <button disabled v-else>Введите название города</button>
        <p class="error">{{ error }}</p>
        <div v-if="info != null">
            <p>{{ showTemp }}</p>
        </div>
       
    </div>
</template>

<style scoped>
    .error{
        color:rgb(245, 48, 48)
    }
</style>

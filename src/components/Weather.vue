
<script>

export default {
    data: () => ({
        city: '',
        temp: null,
        desc: '',
        wind: null
    }),

    created() {
        this.Weather()
    },

    methods: {
        async Weather() {
            let apiKey = '396f33a1e8d9bc6213615581d6e88c6f';
            let city = 'wuhan';
            let url = `http://api.openweathermap.org/data/2.5/weather?q=${city}&lang=zh_cn&units=metric&appid=${apiKey}`
            
            let body = await (await fetch(url)).json();
            if(body){
                this.city = body.name;
                this.temp = body.main.temp;
                this.wind = body.wind.speed;
                console.log('${body.main.temp} in ${body.name}');
            }
        }
    }
}
</script>

<template>
  <div id="weather">
    <button @click="Weather()">获取当前天气</button>
    <p>城市: {{ city }}</p>
    <p>温度: {{ temp }}</p>
    <p>风速: {{ wind }}</p>
  </div>
</template>
<template>
  <div class="clima">
    <div class="dprtmnt">
        <div>
            <input class="depart"  type="text" v-model="dprtmnt" v-on:keyup.enter="dprtmnt.length >2 ?pedirTiempo(dprtmnt) :error = 'La ciudad que buscas no esta registrada'">
            <button :class="[{'btn-ctv': dprtmnt.length > 2},'btn-nctv']"  v-on:click.enter="dprtmnt.length >2 ?pedirTiempo(dprtmnt) :error = 'La ciudad que buscas no esta registrada'">Chequear</button>
        </div>
        <b>{{error}}</b>
    </div>
    <div class="info">
        <div class="desc">
            <b>{{ct}}</b>
            <img ref="img" alt="Imagen del clima">
            <p>{{desc}}</p>
        </div>
        <div class="datos">
            <p>Temperatira: {{temp}}°C</p>
            <p>Presion: {{prsn}} hPa</p>
            <p>Viento: {{vnt}} m/s</p>
        </div>
    </div>
  </div>
</template>

<script>
    export default {
        data(){
            return{
                dprtmnt: "",
                error: "",
                ct: "",
                img: "",
                desc: "",
                temp: "",
                prsn: "",
                vnt: ""
            }
        },
        methods: {
            async pedirTiempo(ct){
                try{
                    let respuesta = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${ct}&units=metric&lang=es&appid=631b7ccc8feaac7191f5011c66d1e376`),
                        data = await respuesta.json(),
                        urlImg = `http://openweathermap.org/img/w/${data.weather[0].icon}.png`;
                    this.$refs.img.setAttribute("src", urlImg);
                    this.ct = data.name;
                    this.desc = data.weather[0].description;
                    this.temp = Math.round(data.main.temp);
                    this.prsn = data.main.pressure;
                    this.vnt = data.wind.speed;
                    this.error = "";
                    this.dprtmnt = "";
                }catch(e){
                  this.error = "La ciudad que buscas no esta registrada";
                }
            }
        },
        created(){
          this.pedirTiempo("bogota");
        }
    }
</script>

<style>
    img{
        display: block;
        margin: 10px;
    }

    button, input{
        border: none;
        outline: none;
    }

    .clima{
        width: 70%;
        margin: 10px auto;
    }

    .depart{
        height: 23px;
        border-radius: 5px;
        padding: 0 2px;
        transition: .9s;
    }

    .depart:hover{
        background-color: #eee;
    }

    .dprtmnt{
        display: block;
    }

    .dprtmnt > div{
        margin-bottom: 10px;
    }

    .dprtmnt > b{
        color: #e01;
    }

    .btn-nctv{
        height: 23px;
        border-radius: 5px;
    }

    .btn-ctv{
        background-color: #a0e;
        height: 23px;
        border-radius: 5px;
        color: #fff;
        cursor: pointer;
    }

    .info{
        display: flex;
        justify-content: space-around;
        align-items: center;
        width: 70%;
        height: fit-content;
        margin: 30px auto;
        padding: 10px 0;
        box-shadow: 5px 4px 8px #000;
    }

    .desc{
        display: block;
    }
    
    .desc > img{
        width: 15vw;
        max-width: 100px;
        margin: 10px auto;
    }

    @media screen and (max-width:680px) {
        .info{display: block;}

        .desc{margin: 20px 0;}

        .desc > img{margin: 10px auto;}

        .datos{margin-top: 40px;}
    }

</style>

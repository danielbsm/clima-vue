<template>
  <div class="logo">
    <img src="./assets/clima.png" alt="logo" />
  </div>
  <div class="cidade">
    Cidade atual:
    <a href="#">{{ cidade }}, GO</a>
  </div>
  <div class="clima">
    <h4>CLIMA ATUAL</h4>
    <h5>{{ time }}</h5>
    <img class="img_cloud" :src="img" alt="tempo" />
    <span class="temperatura">{{ temperatura }}°</span>
    <div class="info_temperatura">
      <span class="tipo_temperatura">{{ tipo_temperatura }}</span>
      <span class="sensacao_termica">
        Sensação térmica: {{ temperatura }}°</span
      >
    </div>
    <div class="detalhes_previsao">
      <div class="detalhe_vento">
        <h3>Vento</h3>
        <span class="vento"> {{ vento }} km/h</span>
      </div>
      <div class="detalhe_umidade">
        <h3>Umidade</h3>
        <span class="umidade"> {{ umidade }}% </span>
      </div>
      <div class="detalhe_visibilidade">
        <h3>Visibilidade</h3>
        <span class="visibilidade"> {{ visibilidade }} km</span>
      </div>
      <div class="detalhe_pressao">
        <h3>pressão</h3>
        <span class="pressao"> {{ pressao }} mb</span>
      </div>
      <div class="detalhe_uv">
        <h3>Raios UV</h3>
        <span class="uv"> {{ uv }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      time: "10:32",
      cidade: "Itapuranga",
      temperatura: 0,
      img: "",
      tipo_temperatura: "",
      vento: 0,
      umidade: 0,
      visibilidade: 0,
      pressao: 0,
      uv: 0,
    };
  },
  methods: {
    buscarClima() {
      const cidade = this.cidade;

      fetch(
        `https://api.weatherapi.com/v1/current.json?key=c1f555ff79af4abea45143004211912&q=${cidade}&aqi=no&lang=pt`
      )
        .then((r) => r.json())
        .then((r) => {
          this.time = new Date(r.location.localtime).toLocaleTimeString([], {
            hour: "2-digit",
            minute: "2-digit",
          });
          this.img = r.current.condition.icon;
          this.temperatura = Math.round(r.current.temp_c);
          this.tipo_temperatura = r.current.condition.text;
          this.vento = Math.round(r.current.wind_kph);
          this.umidade = r.current.humidity;
          this.visibilidade = r.current.vis_km;
          this.pressao = r.current.pressure_mb;
          this.uv = r.current.uv;
        });
    },
  },
  created() {
    this.buscarClima();
  },
};
</script>

<style>
body {
  padding: 0;
  margin: auto;
  background: rgb(2, 0, 36);
  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(116, 92, 12, 1) 42%,
    rgba(0, 212, 255, 1) 100%
  );
}

div {
  display: block;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.logo {
  margin: 30px 0 50px 0;
}

.cidade {
  color: #fff;
  margin-bottom: 10px;
  max-width: 900px;
  margin: auto;
  margin-bottom: 10px;
}

.clima {
  margin: auto;
  max-width: 900px;
  height: 230px;
  border: 2px solid #000;
  border-radius: 6px;
  background: #2c3e50;
}

.clima h4 {
  text-transform: uppercase;
  width: 100%;
  margin: 10px 5px 0px 10px;
  text-align: initial;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  color: rgba(255, 255, 255, 0.8);
}

.clima h5 {
  width: 100%;
  margin: 0px 5px 0px 10px;
  text-align: initial;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  color: rgba(255, 255, 255, 0.8);
}

.img_cloud {
  padding-top: 15px;
  float: left;
  margin: 0 5px;
  width: 80px;
  height: 80px;
}

.temperatura {
  color: #fff;
  float: left;
  padding: 20px 0px 0px 10px;
  font-size: 4rem;
}

.info_temperatura {
  padding-top: 30px;
  float: left;
  padding-left: 50px;
}

.tipo_temperatura {
  font-size: 18px;
  line-height: 24px;
  font-weight: 600;
  color: #fff;
  display: block;
  text-align: left;
  padding-bottom: 10px;
}

.sensacao_termica {
  text-transform: uppercase;
  font-size: 14px;
  line-height: 16px;
  opacity: 0.8;
  float: left;
  color: #fff;
}

.detalhes_previsao {
  display: flex;
  flex-wrap: wrap;
  width: 90%;
  margin: 130px 0 0 15px;
}

.detalhes_previsao h3 {
  text-transform: uppercase;
  font-size: 12px;
  font-weight: normal;
  line-height: 16px;
  opacity: 0.8;
  color: #fff;
  margin: 0;
}

.detalhe_vento {
  margin: 0 80px 0 0;
}

.vento {
  display: flex;
  color: #fff;
  font-size: 16px;
  line-height: 22px;
  font-weight: normal;
}

.detalhe_umidade {
  margin: 0 80px 0 0;
}

.umidade {
  display: flex;
  color: #fff;
  font-size: 16px;
  line-height: 22px;
  font-weight: normal;
}

.detalhe_visibilidade {
  margin: 0 80px 0 0;
}

.visibilidade {
  display: flex;
  color: #fff;
  font-size: 16px;
  line-height: 22px;
  font-weight: normal;
}

.detalhe_pressao {
  margin: 0 80px 0 0;
}

.pressao {
  display: flex;
  color: #fff;
  font-size: 16px;
  line-height: 22px;
  font-weight: normal;
}

.detalhe_uv {
  margin: 0 0 0 0;
}

.uv {
  color: #fff;
  font-size: 16px;
  line-height: 22px;
  font-weight: normal;
}
</style>

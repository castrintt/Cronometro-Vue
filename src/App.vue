<template>
  <div id="app">
    <img src="./assets/cronometro.png" />
    <a class="timer">{{ numero }}</a>
    <div class="area__btn">
      <button class="botao" @click="vai">{{ botao }}</button>
      <button class="botao" @click="limpar">Limpar</button>
    </div>

    <div class="list" v-show="this.historico.length > 0">
      <ul>
        <li v-for="item in historico" :key="item">Você fez uma pausa em:{{ item }}</li>
    <button class="botao" id="botao__historico" @click="limparHistorico">Limpar historico</button>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  name: "App",
  data() {
    return {
      numero: 0,
      botao: "Vai",
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historico:[]
    };
  },
  methods: {
    vai() {
      if (this.timer != null) {
        clearInterval(this.timer);
        this.timer = null;
        this.botao = "Vai";
        if(this.ss !== 0){
          this.historico.push(this.numero)
        }
      } else {
        this.botao = "Pausar";
        this.timer = setInterval(() => {
          this.rodarTimer();
        }, 1000); //1 segundo = 1000 milisegundos
      }
    },
    limpar() {
     if(this.timer !== null){
        clearInterval(this.timer)
        this.timer = null
     }
      this.ss = 0
      this.mm = 0
      this.hh = 0
      this.numero = 0
      this.botao = 'Vai'
    },
    rodarTimer() {
      this.ss++;

      if (this.ss == 59) {
        this.ss = 0;
        this.mm++;
      }
      if (this.mm == 59) {
        this.mm = 0;
        this.hh++;
      }
      let format =
        (this.hh < 10 ? "0" + this.hh : this.hh) +
        ":" +
        (this.mm < 10 ? "0" + this.mm : this.mm) +
        ":" +
        (this.ss < 10 ? "0" + this.ss : this.ss);

      return (this.numero = format);
    },
    limparHistorico(){
      return this.historico = []
    }

  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
  color: white;
}
.timer {
  position: absolute;
  font-size: 80px;
  top: 30%;
}
.area__btn {
  display: flex;
  justify-content: space-between;
  width: 250px;
  margin-top: 20px;
}
.botao {
  padding: 10px;
  width: 100px;
  height: 50px;
  border-radius: 10px;
  outline: none;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
}

.botao:hover {
  opacity: 0.8;
  transition: all 0.5s;
}
.list{
  text-align: center;
  padding: 0;
  list-style: none;
  width: 300px;
  margin-right: 40px;
}
ul li {
  margin-top: 4px;
  padding: 15px;
  background-color:rgb(70,70,70) ;
  list-style: none;
  color: #fff;
  font-size: 18px;
  border-radius:6px ;

}
#botao__historico {
  margin-top: 10px;
  height: 70px;
}
</style>
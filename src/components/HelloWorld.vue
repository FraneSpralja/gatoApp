<template>
    <h1>Random Gato Gif</h1>
  <div id="gatoForm">
    <form @submit.prevent="getGatitosGif">
      <label>Título</label>
      <input type="text" v-model="titulo">
      <br>
      <label>Filtro</label>
      <select name="filters" id="selectFilters" v-model="filterGato">
        <option value="default" selected>Elige un filtro</option>
        <option v-for="filter in filters" :key="filter" :value="filter">{{filter}}
        </option>
      </select>
      <br>
      <label for="">Color</label>
      <select name="" id="" v-model="colorGato">
        <option value="default" selected>Elige un color</option>
        <option v-for="color in colors" :key="color" :value="color">{{color}}</option>
      </select>
      <div id="circleColor" :style="{'background-color':colorGato}"></div>

      <label for="">Tamaño</label>
      <input type="number" v-model="size">

      <button type="submit">Quiero mi gato</button>
    </form>
  </div>

  <div id="pintarGato">
    <img :src="giftGato">
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      titulo: "",
      size: "",
      colors: ["green", "red", "blue", "yellow","orange", "white", "black"],
      filters: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      giftGato: "",
      activeColor: true,
      colorGato: "",
      filterGato: "",
    }
  },
  methods:{
    getGatitosGif(){
      fetch(`https://cataas.com/cat/gif//says/${this.titulo}?size=${this.size}&color=${this.colorGato}&filter=${this.filterGato}`)
        .then((res) => res.blob())
        .then((blob) => {
          let url = URL.createObjectURL(blob)
          this.giftGato = url
        })
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#gatoForm{
  padding: 2em;
  background-color: rosybrown;
}

h1{
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  text-align: center;
  font-size: 3em;
  padding: 1em;
}

form {
  width: 60%;
  border: 1px solid #000;
  border-radius: 7px;
  padding: 2em;
  display: flex;
  flex-flow: column;
  margin: 0 auto;
  box-shadow: 0 0 12px #000;
}

label {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-size: 1.5em;
}

input, select {
  width: 100%;
  margin: 15px auto;
  text-align: center;
  height: 35px;
  font-size: 17px;
}

button {
  cursor: pointer;
  margin: 15px auto;
  width: 40%;
  padding: 7px 10px;
  background-color: #ff9090;
  font-size: 18px;
  border-radius: 15px;
  box-shadow: 0 0 7px #000;
  transition-property: background-color, box-shadow;
  transition-duration: .3s;
  transition-timing-function: linear;
  transition-delay: .2s;
}

button:hover {
  background-color: #8585ff;
  box-shadow: 0 0 17px #ffff06;
}

#pintarGato{
  max-width: 100%;
  height: auto;
  margin: 20px auto;
}

#pintarGato img {
  display: block;
  margin: 0 auto;
  padding: 2em;
}

#colorBlock{
  display: flex;
  flex-flow: row;
  column-gap: 20px;
}

#circleColor{
height: 25px;
width: 25px;
border-radius: 50%;
background-color: #fff;
border: 1px solid #949494;
}

</style>

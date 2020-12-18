<template>
  <div id='app'> 
    <div class="header">
      <h1> Inventario </h1>
      <div class="cont_consulta">
        <select name="inventario" id="li_inventario">
          <option value="Papa">Papa</option>
          <option value="Cebolla">Cebolla</option>
          <option value="Arroz">Arroz</option>
        </select>
        <button type="submit" v-on:click="consultarinventario" >Consultar</button>
      </div>
      <div class="cont_actualizar">
        <input type="number" name="Cambio de precio" id="inp_cambio" value=0>
        <button type="submit" v-on:click="actualizarprecio">Cambiar precio</button>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
    export default {
        name: 'App',
        components: {},

      data: {
        nuevaConsulta: ''
      },

      methods: {
        consultarinventario: function(){
        axios.get("https://despensapp-b.herokuapp.com/inventario/"+li_inventario.value)
          .then((result) => {
          var datos = JSON.stringify(result.data)
          alert(datos+"\n Si aun no se ven los cambios consulte en unos segundos nuevamente")
          })
          .catch((error) => {
            console.log("Error en servidor")
          })
      },
      actualizarprecio: function(){
        var update = {
          producto : li_inventario.value,
          precio : inp_cambio.value
        }
        axios.put("https://despensapp-b.herokuapp.com/inventario/actualizar_precio", update,{headers: {}})
        .then((result) => {
          alert("Valor cambiado correctamente")
        })
        .catch((error) => {
            console.log("Error en servidor")
          })
      }
    }
  }

</script>

<style>
  body{
  background: rgb(34,193,195);
  background: radial-gradient(circle, rgba(34,193,195,1) 0%, rgba(253,187,45,1) 100%);
  }
  .header{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>

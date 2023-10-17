<template>
  <div>
    <h1>Araç Vergi Hesaplama</h1>
    <div>
      <label for="yas">Araç Yaşı: </label>
      <select id="yas" v-model="yas" @change="hesaplaVergi">
        <option value="0">0 - 9 Yaş</option>
        <option value="10">10 Yaş ve Üzeri</option>
      </select>
    </div>


    <br>
    <div>
      <label for="tip">Araç Tipi: </label>
      <select id="tip" v-model="tip" @change="hesaplaVergi">
        <option value="motor">Motor</option>
        <option value="araba">Araba</option>
        <option value="traktor">Traktör</option>
      </select>
    </div>

    <br>
  
    <div>
      <label for="motorGucu">Motor Gücü: </label>
      <select id="motorGucu" v-model="motorGucu" @change="hesaplaVergi">
        <option value="dusuk">Düşük</option>
        <option value="yuksek">Yüksek</option>
      </select>
    </div>
    <br>
    <div>
      <h2>Vergi Tutarı: {{ vergiTutari }} TL</h2>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'; // computed'ı import etmek gereklidir.

export default {
  setup() {
    const yas = ref(0);
    const tip = ref('motor');
    const motorGucu = ref('dusuk');

    const vergiTutari = ref(0);

    const hesaplaVergi = () => {
      let vergiMiktarı = 0;

      if (yas.value < 10) {  //yasına göre vergi hesaplama
        if (tip.value === 'motor') {
          vergiMiktarı = 1000;
        } else if (tip.value === 'araba') {
          if (motorGucu.value === 'dusuk') { // Motor gücüne göre vergi hesaplama
            vergiMiktarı = 1500;
          } else {
            vergiMiktarı = 2000;
          }
        } else if (tip.value === 'traktor') {
          vergiMiktarı = 1200;
        }
      }
      else {    // araç yaşı 10 dan büyükse vergi artacak burada 
        if (tip.value === 'motor') {
          vergiMiktarı = 1200;
        } else if (tip.value === 'araba') {
          if (motorGucu.value === 'dusuk') {
            vergiMiktarı = 1800;
          } else {
            vergiMiktarı = 2000;
          }
        } else if (tip.value === 'traktor') {
          vergiMiktarı = 1500;
        }
      }
      vergiTutari.value = vergiMiktarı;  // if elseler sonrasında son aşamada belirlenen vergi miktarını vergi tutarı değişkeni içerisinde p etiketinde yazdırma

    };

    return { yas, tip, motorGucu, vergiTutari, hesaplaVergi, } ;
  }

  



};
    
 
</script>


<style>
#app {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: #333;
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin: 0 auto;
}

h1 {
  color: #007BFF;
}

label {
  font-weight: bold;
  margin-right: 10px;
}

select {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #007BFF;
  border-radius: 5px;
  background-color: #fff;
  color: #333;
  transition: border-color 0.2s;
}

select:focus {
  outline: none;
  border-color: #333;
}

h2 {
  color: #007BFF;
  margin-top: 20px;
}

</style>

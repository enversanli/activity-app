<template>
    <div>
      <form action="/etkinlik-ara">
        <h2 clasS="text-center text-2xl">Aradığın Tüm Etkinlikler Netsekki'de !</h2>
        <div class="grid lg:grid-cols-4 md:grid-cols-4 sm:grid-cols-1 text-lg text-theme-color mt-10 w-2/3 mx-auto">

          <select name="kategori"
                  class="h-9 m-3 p-1 bg-white shadow-md rounded-lg transition duration-700 hover:shadow-xl cursor-pointer animate__animated animate__fadeIn">
            <option value="">Kategori</option>
            <option v-for="category in categories" :value="category.slug">{{ category.name }}</option>
          </select>
          <select name="sehir"
                  class="h-9 m-3 p-1 bg-white shadow-md rounded-lg transition duration-700 hover:shadow-xl cursor-pointer animate__animated animate__fadeIn">
            <option value="">Şehir</option>
            <option v-for="city in cities" :value="city.slug">{{ city.name }}</option>
          </select>
          <select
              @change="selectDate($event)"
              class="h-9  m-3 p-1 bg-white shadow-md rounded-lg transition duration-700 hover:shadow-xl cursor-pointer animate__animated animate__fadeIn ">
            <option :value="false">Tarih</option>
            <option :value="false">Bu Hafta</option>
            <option :value="false">Haftasonu</option>
            <option :value="false">Gelecek Hafta</option>
            <option @click="selectDate()" :value="true">Tarih Belirle</option>
          </select>
          <button type="submit" class="h-9  m-3 p-1 bg-white shadow-md rounded-lg transition duration-700 hover:shadow-xl cursor-pointer animate__animated animate__fadeIn ">Ara</button>
        </div>
      </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
          categories:null,
          cities: null,
          dateSelectOption:true
        }
    },

    mounted() {
        this.getCities();
        this.getCategories();
    },

    methods: {
      getCities() {
        axios.get('/cities').then(response => {
          this.cities = response.data.data;
        })
      },

      getCategories() {
        axios.get('/categories').then(response => {
          this.categories = response.data.data;
        })
      },

      selectDate($event){
        if ($event.target.value === true){
          alert("DATE SELECT");
        }

      }
    }
}
</script>

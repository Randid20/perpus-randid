<template>
  <div class="container-fluid">
    <div class="row"> 
      <div class="col-lg-12">
        <div class="my-3">
          <form @submit.prevent="getbuku">
          <input
            v-model="keyword"
            type="search"
            class="form-control rounded-5"
            placeholder="mau baca apa hari ini?"
            />
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan 3 dari 3</div>
      </div>
    </div>
    <div class="row justify-content-evenly">
      <div v-for="(buku, i) in books" :key="i" class="card" style="width: 18rem;">
        <nuxt-link :to="`/buku/${buku.id}`">
        <img :src="buku.cover" class="card-img-top" :alt="buku.judul">
        <div class="card-body">
          <p class="card-text">{{ buku.judul }}</p>
        </div>
        </nuxt-link>
      </div>
    </div>
   
    <div class="row">
      <nuxt-link to="/">
        <button type="submit" class="btn btn-danger btn-lg rounded-5 px-5">kembali</button>
      </nuxt-link>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const keyword = ref("")
const books = ref([])
const getbuku = async () => {
  const { data, error} = await supabase.from('Buku').select('* kategori(*)').ilike("judul", `%${keyword.value}%`)
  if(data) books.value= data

}
onMounted(() => {
  getbuku()
})
</script>

<style scoped>
.btn-dark {
  box-shadow: 1px 1px 10px #e4ecea !important;
}
.btn-light {
  background-color: #5fd8fe !important;
  box-shadow: 1px 1px 10px #5fd8fe !important;
}

</style>
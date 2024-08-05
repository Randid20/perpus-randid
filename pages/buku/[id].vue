<template>
  <div class="container">
  <div class="row mt-5">
      <div class="col-md-3 card">
          <img :src="buku.cover">
      </div>
      <div class="p-5 col-md-9">
          <div class="badge bg-primary p-2">{{ buku.kategori }}</div>
          <ul class="text">
              <li class="list-group-item">Judul: {{ buku.judul }}</li>
              <li class="list-group-item">Penulis: {{ buku.penulis }}</li>
              <li class="list-group-item">Penerbit: {{ buku.penerbit }}</li> 
              <li class="list-group-item">Tahun Terbit: {{ buku.tahun_terbit }}</li> 
              <li class="list-group-item">Deskripsi: {{ buku.deskripsi }}</li> 
          </ul>
      </div>
  </div>
</div>
<div class="form-kembali">
        <nuxt-link to="../">
          <button class="btn btn-danger btn-lg rounded-4 px-4">KEMBALI</button>
        </nuxt-link>
        </div>
</template>

<style scoped>
.form-kembali {
position: fixed;
bottom: 10px;
left: 95%;
transform: translateX(-50%);
}
.btn-dark {
box-shadow: 1px 1px 10px #e4ecea !important;
}
.btn-light {
background-color: #5fd8fe !important;
box-shadow: 1px 1px 10px #5fd8fe !important;
}

.text {
  font-size: 1rem;
  line-height: 25px;
}
</style>

<script setup>
const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref([])

const getBookById = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
  .eq('id', route.params.id)
  if(data) buku.value = data[0]
}

onMounted(() =>{
  getBookById()
})
</script>
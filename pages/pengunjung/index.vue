<template>

  <div class="container-fluid">
    <div class="col-lg-12">
      <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
      <div class="my-3">
        <input type="search" class="form-control from-control-lg rounded-5" placeholder="Filter...">
      </div>
      <div class="my-3 text-muted">menampilkan 3 dari 3</div>
      <table class="table">
        <thead>
          <tr>
            <td>No</td>
            <td>NAMA</td>
            <td>KEANGGOTAAN</td>
            <td>WAKTU</td>
            <td>KEPERLUAN</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(visitor, i) in visitors" :key="i">
              <td>{{ i + 1 }}</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan.nama }}</td>
              <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
              <td>{{ visitor.keperluan.nama }}</td>
          </tr>
        </tbody>
      </table>
      <nuxt-link to="/">
        ><button
            class="btn btn-light btn-lg rounded-4 px-4"
            style="float: left"
          >
            KEMBALI
          </button></nuxt-link
        >
        <!-- button -->
        <div class="form-footer">
          <nuxt-link to="/buku"
            ><button class="btn btn-light btn-lg rounded-4 px-4">
              BUKU
            </button></nuxt-link
          >
        </div>
      </div>
    </div> 
</template>

<script setup>
const supabase = useSupabaseClient();
const keyword = ref("");
const visitors = ref([]);

const getPengunjung = async () => {
  const { data, error } = await supabase
    .from("pengunjung")
    .select(`*, keanggotaan(*), keperluan(*)`)
    .ilike("nama", `%${keyword.value}%`)
    .order(`id`, { ascending: false });
  if (data) visitors.value = data;
};
// const totalPengunjung = async () => {
//   const { data, count } = await supabase
//     .from("pengunjung")
//     .select("*", { count: "exact" });
//   if (data) jumlah.value = count;
// };
onMounted(() => {
  getPengunjung();
  // totalPengunjung();
});
</script>

<style scoped>

.form-footer {
  position: fixed;
  bottom: 10; 
  right: 0%;
  transform: translateX(-50%);
}
.btn-dark {
  box-shadow: 1px 1px 10px #e4ecea !important;
}
.btn-light {
  background-color: #5fd8fe !important;
  box-shadow: 1px 1px 10px #5fd8fe !important;
}
</style>

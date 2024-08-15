<template>
  <div>
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
      <div class="col-md-6">
        <img src="~/assets/img/h.png" alt="buku 1" height="250px" width="250px">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">penulis :penulis :andrea{{ buku.penulis }}</li>
          <li class="list-group-item">tahun_terbit :2015 {{ buku.tahun_terbit }}</li>
          <li class="list-group-item">rak :1 {{ buku.rak }}</li>
          <li class=" list-group-item">deskripsi :persahabatan antara tiga orang kawan, yakni Sabari, Ukun, dan Tamat.  {{ buku.deskripsi }}</li>
        </ul>
      </div>
    </div>
  </div>
  <div>
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
      <div class="col-md-6">
        <img src="~/assets/img/m.jpg" alt="buku 1" height="250px" width="250px">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">penulis :penulis :Haykal Bukhar{{ buku.penulis }}</li>
          <li class="list-group-item">tahun_terbit :2019 {{ buku.tahun_terbit }}</li>
          <li class="list-group-item">rak :1 {{ buku.rak }}</li>
          <li class=" list-group-item">deskripsi: mengisahkan seorang gadis cantik bernama Natasha Kay Loovi atau kerap disapa Acha yang memperjuangkan cintanya terhadap seorang laki-laki berhati beku dan super dingin bagaikan es dengan kehidupannya yang serba monoton, bernama Iqbal.  {{ buku.deskripsi }}</li>
        </ul>
      </div>
    </div>
  </div>
  <div>
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
      <div class="col-md-6">
        <img src="~/assets/img/k.jpg" alt="buku 1" height="250px" width="250px">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">penulis :penulis :Nadhifa Allya Tsana,{{ buku.penulis }}</li>
          <li class="list-group-item">tahun_terbit :2016 {{ buku.tahun_terbit }}</li>
          <li class="list-group-item">rak :1 {{ buku.rak }}</li>
          <li class=" list-group-item">deskripsi :hati bintara yang penuh bimbang.  {{ buku.deskripsi }}</li>
        </ul>
      </div>
    </div>
  </div>
 <nuxt-link to="/">
 <button type="submit" class=" n btn btn-dark btn-lg rounded-5 px-5 abu ">kembali</button>
 </nuxt-link>
</template>

<script setup>
import { onMounted } from 'vue';

const supabase = useSupabaseClient()
const route = useRoute()
const buku = ref([])

const getBukuByID = async () => {
  const { data, error } = await supabase
    .from('Buku')
    .select(`*, kategori_buku(*)`)
    .eq('id', route.params.id)
    .single()
  if (data) buku.value = data
}

onMounted(() => {
  getBukuByID()
})
</script>
<style scoped>
.cover {
  width: 100%;
}
</style>
<template>
  <div>
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
      <div class="col-md-6">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">penulis : {{ buku.penulis }}</li>
          <li class="list-group-item">tahun_terbit : {{ buku.tahun_terbit }}</li>
          <li class="list-group-item">rak : {{ buku.rak }}</li>
          <li class=" list-group-item">deskripsi : {{ buku.deskripsi }}</li>
        </ul>
      </div>
    </div>
    <nuxt-link to="/">
      <button type="submit" class=" n btn btn-dark btn-lg rounded-5 px-5 abu ">kembali</button>
    </nuxt-link>
  </div>
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
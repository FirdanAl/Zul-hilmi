<template>
  <div>
      <h2 class="text-start my-4">{{ buku.judul }}</h2>
      <div class="row">
          <div class="col-md-3">
              <div class="card">
                  <div class="card-body">
                      <span v-if="buku.cover"><img class="cover" :src="buku.cover" :alt="buku.judul"></span>
              <span v-else><img src="https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.svgrepo.com%2Fsvg%2F508699%2Flandscape-placeholder&psig=AOvVaw2-SWmfk33NzXubPfqn0P16&ust=1714794757874000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCNjln7nK8IUDFQAAAAAdAAAAABAE://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.svgrepo.com%2Fsvg%2F508699%2Flandscape-placeholder&psig=AOvVaw2-SWmfk33NzXubPfqn0P16&ust=1714794757874000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCNjln7nK8IUDFQAAAAAdAAAAABAE" class="cover"></span>
                  </div>
              </div>
          </div>
          <div class="col-md-6">
            <img src="~/assets/img/h.png" alt="buku 1" height="100px" width="100px">
              <ul class="list-group list-group-flush">
                  <li class="list-group-item">penulis :andrea{{  buku.penulis }}</li>
                  <li class="list-group-item">tahun_terbit : 2015{{  buku.tahun_terbit }}</li>
                  <li class="list-group-item">rak :1 {{ buku.rak }}</li>
                  <li class=" list-group-item">deskripsi : persahabatan antara tiga orang kawan, yakni Sabari, Ukun, dan Tamat.  {{ buku.deskripsi }}</li>
              </ul>
          </div>
      </div>
      <NuxtLink to="/buku" class="btn btn-light btn-lg rounded-5 px-5">
      kembali
      </NuxtLink>
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
  if(data) buku.value = data
}

onMounted(() => {
  getBukuByID()
})
</script>
<style scoped>
.cover{
  width: 100%;
}
</style>
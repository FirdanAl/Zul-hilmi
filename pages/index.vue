<template>
  <div class="container-fluid">
      <div class="row my-5">
          <div class="col-lg-6 box ">
              <nuxt-link to="../pengunjung/tambah">
                  <div class="card bg-pengunjung rounded-5">
                      <div class="card-body">
                          <h2>Pengunjung</h2>
                      </div>
                  </div>
              </nuxt-link>
          </div>
          <div class="col-lg-6 box">
            <nuxt-link to="../buku">
                  <div class="card bg-buku rounded-5">
                      <div class="card-body">
                          <h2>Cari Buku</h2>
                      </div>
                  </div>
            </nuxt-link>
          </div>
      </div>
  </div>
  <h2 style="margin: 30px"><strong> STATISTIK </strong></h2>
<div class="Container-fluid">
  <div class="row justify-content-evenly rounded-3">
    <div class="col-5">
      <div class="card1">
        <div class="raccing">
          <h2><span class="no">{{ jml_pengunjung }}</span> pengunjung </h2>
        </div>
      </div>
    </div>
    <div class="col-5">
      <div class="raccing1">
        <h2><span class="no">{{ jml_buku }}</span> Buku </h2>
      </div>
    </div>
  </div>
  <div class="line">
    <statistik/>
  </div>
</div>

</template>
<script setup>
  const supabase = useSupabaseClient()
  const jml_pengunjung = ref( 3 )
  const jml_buku = ref( 8 )

  async function getjml_pengunjung() {
  const{ error , data, count } = await supabase
  .from("Pengunjung")
  .select('*', { count: 'exact' })
  if (count) jml_pengunjung.value = count

  }
  async function getjml_buku() {
  const{ error , data, count } = await supabase
  .from("Buku")
  .select('*', { count: 'exact' })
  if (count) jml_buku.value = count

  }


  onMounted(() => {
  getjml_pengunjung()
  getjml_buku()
  })
</script>

<style scoped>
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #d9ce3b;
}
.card.bg-pengunjung {
  background-image: url('../assets/img/kunjungan.jpeg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}
.card.bg-buku {
  background: url('../assets/img/bg-home-cari-buku.jpg') no-repeat center center;
  background-size: cover;
}
.raccing {
height: 200px;
box-shadow: 1px 1px 10px;
border-radius: 20px;
display: flex;
justify-content: center;
align-items: center;
background-color:   #d8eb2c;
}
.raccing1 {
height: 200px;
box-shadow: 1px 1px 10px;
border-radius: 20px;
display: flex;
justify-content: center;
align-items: center;
background-color:   #007202;
}
.card-body h2{
  color:black;
}
.box {
width: 50%;
}
.box a{
text-decoration: none;
}
</style>




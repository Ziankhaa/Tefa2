<template>
    <div class="container-fluid">
        <div class="row my-5">
            <div class="col-lg-6">
                <nuxt-link to="/pengunjung/tambah">
                    <div class="card bg-pengunjung rounded-5 m-3">
                        <div class="card-body">
                            <h2>Pengunjung</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>

            <div class="col-lg-6">
                <nuxt-link to="/buku">
                    <div class="card bg-buku rounded-5 m-3">
                        <div class="card-body">
                            <h2>Cari Buku</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>
        </div>
    </div>
    <h2 style="margin : 30px;"><strong>STATISTIK</strong></h2>
    <div class="container-fluid">
        <div class="row justify-content-evenly rounded-5">
            <div class="col-5">
                <div class="jeep">
                    <nuxt-link to="/pengunjung">
                        <h2> {{ visitors.length }} pengunjung </h2>
                    </nuxt-link>
                </div>
            </div>
            <div class="col-5">
                <div class="raccing1">
                    <h2>{{ books.length }} buku </h2>
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>
.card {
    height:250px;
    box-shadow: 1px 1px 10px #424242;
}
.card.bg-pengunjung {
    background: url('../assets/img/bg-home-kunjungan.jpeg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    margin-bottom: 30px;
}
.card.bg-buku {
    background: url('../assets/img/bg-home-cari-buku.jpg') no-repeat center center;
    background-size: cover;
}

.jeep{
    height: 200px;
    box-shadow: 1px 1px 10px;
    border-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #E1B4F1;
}

.raccing1{
    height: 200px;
    box-shadow: 1px 1px 10px;
    border-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #C1F5E9;
}
</style>

<script setup>

const supabase = useSupabaseClient()
const visitors = ref ([])
const books = ref ([])

const getPengunjung = async () => {
    const { data,error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
    if(data) visitors.value = data
}

const getBooks = async () => {
    const { data,error } = await supabase.from('buku').select(`*, kategori(*)`)
    if (data) books.value = data
}

onMounted (() => {
    getPengunjung()
    getBooks()
}
)


</script>

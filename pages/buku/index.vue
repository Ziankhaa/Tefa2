<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">PILIHLAH BUKU YANG INGIN ANDA BACA</h2>
                <div class="my-3">
                    <form @submit.prevent="getBooks">
                    <input v-model="keyword" type="search" class="form-contol rounded-5" placeholder="mau baca apa hari ini ?">
                    </form>
                </div>
                <div class="my-3 text-muted fs-6">menampilkan {{  books.length }} dari {{ jumlah }}</div>
                <div class="row">
                    <div v-for="(book,i) in books" :key="i" class="col-lg-2 pb-5">
                        <div class="card mb-3 dcdc">
                            <div class="card-body">
                                <nuxt-link :to="`/buku/${book.id}`">
                                    <img :src="book.cover" alt="" width="155" height="200">
                                    <h6>{{ book.judul }}</h6>
                                </nuxt-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <nuxt-link to="/" class="btn btn-dark btn-lg rounded-5 px-5">kembali</nuxt-link>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const books = ref([])
const jumlah =(0)
const keyword = ref('')


const getBooks= async () => {
    const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
        .ilike('judul', `%${keyword.value}%`)
        if(data) books.value = data
}

    const totalBuku = async () => {
        const { data, count } = await supabase.from('buku').select("*", {count: 'exact'})
        if (data) jumlah.value = count
    }

onMounted(() => {
    getBooks()
    totalBuku()
})

</script>

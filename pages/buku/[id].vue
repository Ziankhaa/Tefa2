<template>
    <div class="container">
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
      <div class="col-md-3">
        <img :src="buku.cover" class="cover" alt="cover buku">
      </div>
      <div class="col-md-6">
        <div class="badge bg-primary p-2">{{ buku.kategori }}</div>
        <ul class="list-group lish-group-plush">
          <li class="list-group-item">penulis: {{ buku.penulis }}</li>
          <li class="list-group-item">tahun_terbit: {{ buku.tahun_terbit }}</li>
          <li class="list-group-item">penerbit: {{ buku.penerbit  }}</li>
          <li class="list-group-item">Deskripsi: {{ buku.deskripsi }}</li>
        </ul>
      </div>
    </div>
  </div>
    <div class="row">
          <div class="col-lg-12 mt-5">
            <nuxt-link to="/buku/">
            <button type="submit" class="btn btn-dark rounded-3 px-5">Kembali</button>
            </nuxt-link>
          </div>
    </div>
  </template>
  <script setup>
  const supabase = useSupabaseClient()
  const route = useRoute()
  const buku = ref ([])
  
  const getBookById = async () => {
    const {data, error} = await supabase
      .from('buku')
      .select(`*, kategori(*)`)
      .eq('id', route.params.id)
      .single()
    if(data) buku.value = data
  }
  onMounted(() =>{
    getBookById()
  })
  
  </script>
  <style scoped>
  img{
    width: 70%;
  }
  </style>
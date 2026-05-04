<template>
  <NavBar />
  <PostData @data-added="refreshData"/>
  <GetData ref="getDataComp"/>
  <UpdateData @data-added="refreshData" ref="updateDataComp"/>
  <DeleteData @data-added="refreshData" ref="deleteDataComp" />
</template>

<script>
import NavBar from './components/NavBar.vue';
import PostData from './components/PostData.vue';
import GetData from './components/GetData.vue';
import UpdateData from './components/UpdateData.vue';
import DeleteData from './components/DeleteData.vue';

export default {
  name: 'App',
  components: {
    NavBar,
    PostData,
    GetData,
    UpdateData,
    DeleteData
  },
    methods: {
    refreshData() {
      this.$refs.getDataComp.fetchData();
      this.$refs.updateDataComp.fetchData();
      this.$refs.deleteDataComp.fetchData();
    }
  }
}
</script>

<style>
body {
    background-color: #f5f7fa;
}

.card {
    border-radius: 12px;
    border: none;
}

.card-header h5 {
    font-weight: 600;
    letter-spacing: 0.5px;
}

.table td, .table th {
    vertical-align: middle;
}

.btn {
    border-radius: 6px;
}

.btn:hover {
    opacity: 0.9;
    transition: 0.2s;
}
html{
    scroll-behavior: smooth;
}
#post, #get, #update, #delete {
    scroll-margin-top: 80px;
}
i.bi {
    vertical-align: middle;
}
</style>

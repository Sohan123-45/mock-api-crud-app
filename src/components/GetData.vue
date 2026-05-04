<template>
    <div id="get" class="container mt-4">
        <div class="card shadow">
            <div class="card-header bg-primary text-white">
                <h5 class="mb-0">
                    <i class="bi bi-table me-2"></i>Employee Records
                </h5>
            </div>

            <div class="card-body p-0">
                <div class="table-responsive">
                    <table class="table table-striped table-hover mb-0">
                        <thead class="table-dark">
                            <tr>
                                <th>ID</th>
                                <th>Name</th>
                                <th>Designation</th>
                                <th>Salary</th>
                            </tr>
                        </thead>
    
                        <tbody>
                            <tr v-for="list in lst" :key="list.id">
                                <td>{{ list.id }}</td>
                                <td>{{ list.Name }}</td>
                                <td>{{ list.Designation }}</td>
                                <td>₹ {{ list.Salary }}</td>
                            </tr>
    
                            <tr v-if="lst.length === 0">
                                <td colspan="4" class="text-center py-4 text-muted">
                                    No data available
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
    export default{
        name:'GetData',
        data(){
            return{
                lst:[]
            }
        },
        methods:{
            async fetchData(){
                await axios.get('https://69e7504d68208c1debe8a892.mockapi.io/api/p1/Employees')
                .then((res)=>{
                    this.lst=res.data;
                })
                .catch((err)=>{
                    console.log(err);
                })
            }
        },
        mounted(){
            this.fetchData();
        }
    }
</script>

<style>
    .card {
        border-radius: 10px;
    }

    .table td, .table th {
        vertical-align: middle;
    }
</style>
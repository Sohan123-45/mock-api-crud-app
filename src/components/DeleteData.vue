<template>
    <div id="delete" class="container mt-4">
        <div class="card shadow">
            
            <div class="card-header bg-danger text-white">
                <h5 class="mb-0">
                    <i class="bi bi-trash-fill me-2"></i>Delete Employee
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
                                <th class="text-center">Delete</th>
                            </tr>
                        </thead>
    
                        <tbody>
                            <tr v-for="list in lists" :key="list.id">
                                <td>{{ list.id }}</td>
                                <td>{{ list.Name }}</td>
                                <td>{{ list.Designation }}</td>
                                <td>₹ {{ list.Salary }}</td>
                                <td class="text-center">
                                    <button 
                                        class="btn btn-danger btn-sm"
                                        @click="deleteData(list)">
                                        <i class="bi bi-trash"></i>
                                    </button>
                                </td>
                            </tr>
    
                            <!-- Empty state -->
                            <tr v-if="lists.length === 0">
                                <td colspan="5" class="text-center py-4 text-muted">
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
        name:'DeleteData',
        data(){
            return{
                lists:[]
            }
        },
        mounted(){
            this.fetchData();
        },
        methods:{
            async fetchData(){
                await axios.get('https://69e7504d68208c1debe8a892.mockapi.io/api/p1/Employees')
                .then((res)=>{this.lists=res.data})
                .catch((err)=>{console.log(err)})
            },
            async deleteData(item){
                const ans=confirm("Do you want to delete?");
                if(!ans) return;

                await axios.delete(`https://69e7504d68208c1debe8a892.mockapi.io/api/p1/Employees/${item.id}`)
                .then((res)=>{console.log(res);})
                .catch((err)=>{console.log(err)});
                this.fetchData()

                this.$emit('data-added');
            }
        }
    }
</script>

<style>
</style>
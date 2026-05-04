<template>
    <div id="update" class="container mt-4">
        <div class="card shadow">
            
            <div class="card-header bg-warning text-dark">
                <h5 class="mb-0">
                    <i class="bi bi-pencil-square me-2"></i>Update Employee
                </h5>
            </div>

            <div class="card-body p-0">
                <div class="table-responsive-md">
                    <table class="table table-striped table-hover mb-0">
                    <thead class="table-dark">
                            <tr>
                                <th>ID</th>
                                <th>Name</th>
                                <th>Designation</th>
                                <th>Salary</th>
                                <th class="text-center">Edit</th>
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
                                        class="btn btn-warning btn-sm"
                                        @click="editItem(list)">
                                        <i class="bi bi-pencil-fill"></i>
                                    </button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <div class="card-body border-top" v-if="isData.availability">
                <form @submit.prevent="editData">
                    
                    <div class="row">
                        <div class="col-md-4 mb-3">
                            <label class="form-label">Name</label>
                            <input type="text" class="form-control" v-model="isData.name">
                        </div>

                        <div class="col-md-4 mb-3">
                            <label class="form-label">Designation</label>
                            <input type="text" class="form-control" v-model="isData.desig">
                        </div>

                        <div class="col-md-4 mb-3">
                            <label class="form-label">Salary</label>
                            <input type="number" class="form-control" v-model="isData.salary">
                        </div>
                    </div>

                    <div class="d-flex justify-content-end gap-2">
                        <button 
                            type="button" 
                            class="btn btn-secondary"
                            @click="CancelReq">
                            <i class="bi bi-x-circle me-1"></i>Cancel
                        </button>

                        <button type="submit" class="btn btn-warning">
                            <i class="bi bi-check-circle me-1"></i>Update
                        </button>
                    </div>

                </form>
            </div>

        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default{
    name:'UpdateData',
    data(){
        return{
            lists:[],
            isData:{
                id:null,
                name:'',
                desig:'',
                salary:'',
                availability:false
            }
        }
    }, 
    mounted(){
        this.fetchData();
    },
    methods:{
        CancelReq(){
            this.isData.name='';
            this.isData.desig='';
            this.isData.salary=null;
            this.isData.availability=false;
        },
        async fetchData(){
            await axios.get('https://69e7504d68208c1debe8a892.mockapi.io/api/p1/Employees')
            .then((res)=>{
                this.lists=res.data;
            })
            .catch(err=>{console.log(err)});
        },
        editItem(list){
            this.isData.id=list.id;
            this.isData.name=list.Name;
            this.isData.desig=list.Designation;
            this.isData.salary=list.Salary;
            this.isData.availability=true;
        },
        async editData(e){
            e.preventDefault();
            let id=this.isData.id;
            let name=this.isData.name;
            let Designation=this.isData.desig;
            let salary=this.isData.salary;
            await axios.put(`https://69e7504d68208c1debe8a892.mockapi.io/api/p1/Employees/${id}`,{
                Name:name,
                Designation:Designation,
                Salary:salary
            })
            .then((res)=>{console.log(res);alert("Data updated successfully")})
            .catch((err)=>{console.log(err)})

            this.isData.name='';
            this.isData.desig='';
            this.isData.salary=null;
            this.isData.availability=false;

            this.fetchData();
            this.$emit('data-added');
        }
    }
}
</script>

<style>
.card {
    border-radius: 12px;
}

.table td, .table th {
    vertical-align: middle;
}
</style>
<template>
    <div id="post" class="container mt-4">
        <div class="card shadow">
            <div class="card-header bg-success text-white">
                <h5 class="mb-0">
                    <i class="bi bi-person-plus-fill me-2"></i>Add Employee
                </h5>
            </div>

            <div class="card-body">
                <form @submit.prevent="postData">
                    
                    <div class="mb-3">
                        <label class="form-label">Name</label>
                        <input type="text" class="form-control" v-model="name" placeholder="Enter name">
                    </div>

                    <div class="mb-3">
                        <label class="form-label">Designation</label>
                        <input type="text" class="form-control" v-model="desig" placeholder="Enter designation">
                    </div>

                    <div class="mb-3">
                        <label class="form-label">Salary</label>
                        <input type="number" class="form-control" v-model="salary" placeholder="Enter salary">
                    </div>

                    <button type="submit" class="btn btn-success w-100">
                        <i class="bi bi-send-fill me-1"></i>Submit
                    </button>
                </form>

                <!-- Message -->
                <div v-if="Msg" class="alert mt-3" :class="Msg.includes('Error')?'alert-danger': 'alert-success'">
                    {{ Msg }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default{
    name:'PostData',
    data(){
        return{
            name:'',
            desig:'',
            salary:null,
            Msg:''
        }
    },
    methods:{
        postData(event){
            event.preventDefault();
            let name=this.name;
            let designation=this.desig;
            let salary=this.salary;
            if(!this.name || !this.desig || !this.salary){
                this.Msg='Error : all values must be filled';
                setTimeout(()=>{
                    this.Msg='';
                },2000);
                return;
            }
            axios.post('https://69e7504d68208c1debe8a892.mockapi.io/api/p1/Employees',{
                Name:name,
                Designation:designation,
                Salary:salary
            })
            .then((res)=>{
                res;
                this.Msg='Post added successfully';
                setTimeout(()=>{
                    this.Msg='';
                },2000);
                this.$emit('data-added');
            })
            .catch(err=>{
                console.log(err);
                this.Msg='Post was not added';
                setTimeout(()=>{
                    this.Msg='';
                },2000);
            })
            this.name='';
            this.desig='';
            this.salary='';
        }
    }
}
</script>

<style>
    .card {
        border-radius: 10px;
    }

    input:focus {
        box-shadow: none !important;
        border-color: #198754;
    }
</style>
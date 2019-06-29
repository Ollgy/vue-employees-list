<template lang="pug">
    
    .employees
        .search            
            input(type="text" 
                    placeholder="Поиск"
                    v-model="searchInput"
                    @input="filterEmployee(searchInput)"
                    ).search-input
            i(class="fa fa-search search-icon" aria-hidden="true")
        .button-block
            button(type="button"
                    @click="openModal=true").button Добавить
            button(type="button" @click="editEmployee").button Редактировать
            button(type="button" @click="removeEmployee").button Удалить
        transition(name="fade")
            modalInput(v-if="openModal" 
                        @addEmployee="addEmployee" 
                        @close="openModal=false" 
                        :isEdit="edit" 
                        :editId="editId"
                        :visibileByFilter="visibileByFilter" 
                        :employee='employees[editId]')
        employeeList(:employees="employees"
            @removeEmployee="removeEmployee"
            @checkEmployee = "checkEmployee"
            @checkActive = "checkActive")
  
</template>

<script>

import employeeList from './employeeList.vue'
import modalInput from './modalInput.vue'

export default {

    components:{    
        employeeList,
        modalInput
    },

    data(){
        return{
            employees: [],
            openModal: false,
            editId: -1,
            edit: false,
            visibileByFilter: true,
            searchInput: '',          
        }
    },

    methods:{
        addEmployee(employee){
            if(!this.edit){
                this.employees.push(employee)
            } else{
                this.employees = this.employees.map(item => item.id === this.editId ? employee : item);
                this.edit = false;
                this.editId = -1;
                this.openModal=false;                
            }
        },
        checkEmployee(employeeItem){
            this.employees = this.employees.map(item => item.id === employeeItem.id ? employeeItem : item);
        },
        checkActive(employeeItem){
            this.employees.forEach(function(item){
                item.id === employeeItem.id
                    ? item.active= true
                    : item.active= false 
            })
        },
        removeEmployee(){
            this.employees = this.employees.filter(item => item.checked !== true || item.active === true)
        },
        editEmployee(){
            if(this.employees.some(item => item.active === true)){
                this.openModal = true;
                this.edit = true;
                this.editId = this.employees.find(item => item.active !== false).id;
            }             
        },
        filterEmployee(text){
            this.employees.forEach(function(item){
                !item.surname.indexOf(text)
                    ? item.visibileByFilter = true
                    : item.visibileByFilter = false 
            })
           
        }
    }   

}
</script>

<style lang="scss" src='styles/employees.scss' scoped>

</style>

<template lang="pug">
    .modal-input
        header.header 
            i(class="fas fa-edit") 
            .header-title Панель редактирования
        .edit-block
            .photo-block
                img.preview(:src="employee.img")
                
                select(v-model = "employee.img").input
                    option(label="Снимок 1") /src/assets/photo/d_001.png
                    option(label="Снимок 2") /src/assets/photo/d_002.png
                    option(label="Снимок 3") /src/assets/photo/d_003.png
            .person-block
                input(
                type="text" 
                placeholder="Имя"
                v-model = "employee.name"
                ).input

                input(
                type="text" 
                placeholder="Фамилия"
                v-model = "employee.surname"
                ).input

                input(
                type="date" 
                placeholder="Дата рождения"
                v-model = "employee.date"
                @change = "calcAge(employee.date)"
                ).input

                input(
                type="text" 
                placeholder="Возраст"
                v-model = "employee.age"
                disabled
                ).input

                select(v-model = "employee.position").input
                    option техник
                    option бухгалтер
                    option программист

                label.chb-label
                    input(
                        type="checkbox" 
                        v-model = "employee.remote"
                        ).chb-input
                    .chb-custom 
                    span Удаленная работа

            .address-block         
                input(
                type="text" 
                placeholder="Город"
                v-model = "employee.city"
                ).input

                input(
                type="text" 
                placeholder="Улица"
                v-model = "employee.street"
                ).input

                input(
                type="text" 
                placeholder="Дом"
                v-model = "employee.building"
                ).input

                input(
                type="text" 
                placeholder="Квартира"
                v-model = "employee.flat"
                ).input

        .button-block   
            button(type="button" @click="closeModal").button Закрыть
            button(type="button" @click="addEmployee(isEdit, editId)").button Сохранить 
    
</template>


<script>

let uniqId = -1;

export default {

    props:{
        isEdit: Boolean,
        editId: Number,
        employee:{
            type: Object,
            default:() => {
                return {
                    active: false,
                    id: 0,
                    img: '/src/assets/photo/d_001.png',
                    name: '',
                    surname: '',
                    date: '',
                    age: '',
                    position: 'техник',
                    remote: false,
                    city: '', 
                    street: '',
                    building: '',
                    flat: '',                
                    checked: false,
                    visibileByFilter: true
                } 
            }
        }
    },    
    methods:{
        addEmployee(isEdit, editId){
            if(!isEdit){
                uniqId++;  
                this.employee.id = uniqId;
            } else  {
                this.employee.id = editId;
            } 
            this.employee.checked = false;
           
                            
            this.$emit("addEmployee", {...this.employee});
                   
            this.employee.name="";
            this.employee.surname="";
            this.employee.date="";
            this.employee.age="";
            this.employee.position="техник";
            this.employee.remote=false;
            this.employee.city="";
            this.employee.street="";
            this.employee.building="";
            this.employee.flat="";
                        
        },
        closeModal(){
            this.$emit("close");
        },
        calcAge(birthDate){
            birthDate = new Date(birthDate);
                var now = new Date(),
                age = now.getFullYear() - birthDate.getFullYear();
                if(age!=NaN){
                    this.employee.age = now.setFullYear(2000) < birthDate.setFullYear(2000) ? age - 1 : age;
                }else this.employee.age = ''

        }
    }

}
</script>

<style lang="scss" src="styles/modalInput.scss" scoped>

</style>

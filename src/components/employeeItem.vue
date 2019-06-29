<template lang="pug">
    .employee-item(v-if="employee.visibileByFilter")
        input.radio(type="radio"
                name="isActive"
                :class="{active:employee.active}"
                :value="employee.id"
                @change="checkActive")
        .employee-info
            label.label(:class="{checked:employee.checked}")
                .column.column--photo
                    img.photo(:src="employee.img")
                .column.column--name {{employee.name}}
                .column.column--surname {{employee.surname}}
                .column.column--date {{employee.date}}
                .column.column--age {{employee.age}}
                .column.column--position {{employee.position}}
                .column.column--remote
                    input(
                    type="checkbox"
                    :checked= "employee.remote"
                    disabled               
                    ).input
                .column.column--address г. {{employee.city}}, ул. {{employee.street}}, д. {{employee.building}}, кв.{{employee.flat}}
        input(
            type="checkbox"
            @change="checkEmployee"
            v-model="employee.checked"                
            ).input
  
</template>

<script>
export default {
    props: {
        employee: Object,      
    },
    methods: {
        removeEmployee(){
            this.$emit('removeEmployee', this.employee.id)
        },
        checkEmployee(e){
            const employeeItem = {
                ...this.employee,
                checked: e.target.checked
            }
            this.$emit('checkEmployee', employeeItem)
        },
        checkActive(){
            const employeeItem = this.employee;            
            this.$emit('checkActive', employeeItem)
        }
    }

}
</script>

<style lang="scss" src='styles/employeeItem.scss' scoped>

</style>

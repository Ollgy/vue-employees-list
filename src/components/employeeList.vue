<template lang="pug">
    .employee-list
        .content
            ul.list
                .list-header
                    -
                        var columns=[{title:'Фото', key:'photo'},
                                       {title:'Имя', key:'name'},
                                       {title:'Фамилия', key:'surname'},
                                       {title:'Дата Рождения', key:'date'},
                                       {title:'Возраст', key:'age'},
                                       {title:'Должность', key:'position'},
                                       {title:'Удаленная работа', key:'remote'},
                                       {title:'Адрес проживания', key:'address'}]
                    each column in columns
                        li(class=`column column--${column.key}`)= column.title
                li.item(v-for="employee in employees")
                    employee-item(
                        :employee="employee"                        
                        @removeEmployee="removeEmployee"
                        @checkEmployee = "checkEmployee"
                        @checkActive = "checkActive"
                    )       
  
</template>

<script>
import employeeItem from './employeeItem.vue'

export default {

    components:{
        employeeItem
    },
    props:{
        employees: Array
    },
    methods:{
        removeEmployee(employeeId){
            this.$emit('removeEmployee', employeeId)
        },
        checkEmployee(employeeItem){
            this.$emit('checkEmployee', employeeItem)
        },
        checkActive(employeeItem){
            this.$emit('checkActive', employeeItem)
        }
    }

}
</script>

<style lang="scss" src='styles/employeeList.scss' scoped>

</style>

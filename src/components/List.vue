<template>
    <div>
         <li :class="['list-group-item d-flex justify-content-between align-items-center created',{'deleted':list.isDelete}]" @dblclick="list.isEdit = true">
            <input v-if="list.isEdit" type="text" @keyup.enter="list.isEdit = false " v-model="list.message" class="form-control form-control-lg mr-2">
                <div v-else class="custom-control custom-checkbox">
                    <input type="checkbox" v-model="list.isDone" class="custom-control-input" :id="'customCheck1'+list.id">
                        <label :class="['custom-control-label',{'done':list.isDone}]" :for="'customCheck1'+list.id">{{ list.message }}</label>
                    </div>
                    <i class="fas fa-trash-alt text-danger" @click="[list.isDelete=true,del(list.id)]"></i>
        </li>
    </div>
</template>

<script>
    export default {
      name : "List",
      props:{
          list:{
              type: Object,
              required:true,
          }
      } ,
      methods: {
          del(x) {
             this.$emit("del",x) 
          }
      }, 
    }
</script>

<style lang="scss" scoped>

</style>
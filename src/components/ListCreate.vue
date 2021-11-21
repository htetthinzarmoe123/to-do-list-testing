<template>
    <div>
        <div class="form row mb-3">
                    <div class="col-10">
                        <div class="mb-3">
                          <input type="text" class="form-control form-control-lg" @keyup.enter="createList()" @keyup="showError=false" placeholder="Say something!" v-model="newMessage">
                        </div>
                    </div>
                    <div class="col-2">
                        <button class="btn btn-primary btn-lg w-100" @click="createList()">
                            <i class="fas fa-plus-circle"></i>
                        </button>
                    </div>
                    <div class="col-12">
                        <small v-if="showError" class="text-danger font-weight-bold">{{errorMessage}}</small>
                    </div>
                </div>
    </div>
</template>

<script>
    export default {
        name : "ListCreate",
        data() {
            return {
                newMessage: "",
                showError : false,
                errorMessage : ""
            }
        },
        methods: {
            createList() {
                if(this.newMessage.length){
                    this.showError = false;
                     this.$emit("createList",this.newMessage)
                               this.newMessage = "";
                }else{
                    this.showError = true;
                    this.errorMessage = "Say something!";
                }
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>
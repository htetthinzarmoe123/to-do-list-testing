<template>
  <div>
     <div class="container">
      <div class="row justify-content-center">
        <div class="col-12 col-md-4">
            <div class="my-5">
              <Title title="Vue Todo App"></Title>
                <div class="form row mb-3">
                    <div class="col-10">
                        <div class="mb-3">
                          <input type="text" class="form-control form-control-lg" @keyup.enter="create()" placeholder="Say something!" v-model="newMessage">
                        </div>
                    </div>
                    <div class="col-2">
                        <button class="btn btn-primary btn-lg w-100" @click="create()">
                            <i class="fas fa-plus-circle"></i>
                        </button>
                    </div>
                </div>
                    <div class="d-flex justify-content-center">
                        <p class="mb-0 font-weight-bold ">Job List{{lists.length > 1?"s" : ""}}</p>

                        <p v-if="lists.length > 0 && doneTotal === lists.length" class="badge bg-success m-auto">
                            All Done <i class="fas fa-check-circle"> </i>
                        </p>

                        <p v-else class="badge bg-primary m-auto">
                            Done {{ doneTotal }}
                        </p>
                    </div>
                    <ul class="list-group">
                       <li v-if="lists.length === 0" class="list-group-item text-center">
                         This is no job
                       </li>
                       <List v-for="list in lists" :key="list.id" :list="list" @del="del"></List>
                    </ul>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Title from "./components/Title";
  import List from "./components/List";
  export default {
    name : "App",
    components: {Title,List},
    data() {
      return {
         currentId : 0,
            newMessage : "",
            lists : []
      }
    },
      computed : {
            doneTotal(){
                return this.lists.filter(el => el.isDone === true).length
            }
        },
       methods : {
           create(){
               this.currentId++
               this.lists.push({
                    id: this.currentId,
                    message : this.newMessage,
                    isDone : false,
                    isEdit : false,
                    isDelete : false,
               });
               this.newMessage = "";
           },
           del(x){
            setTimeout(()=>this.lists= this.lists.filter(el=>el.id !== x),600)
           }    
       }
  }
</script>

<style>
  .done{
            text-decoration: line-through !important;
            animation: shakeX 0.5s;
        }
        .created{
            animation: fadeInDown 0.5s;
        }
        .deleted{
            animation: shakeX 0.5s;
        }
</style>
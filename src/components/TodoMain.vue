<template>

 <div class="page">
    <header><h1>Vue Fire todo1</h1></header>
    <main>
      <div class="todos">
        <div class="write" v-if="writeState === 'add'">
          
          <input ref="writeArea" type="text" v-model = "addItemText" @keyup.enter="addItem"/>
          <button class="btn add" @click="addItem">Add</button>
        </div>
        <div class="write" v-else> <!--수정-->
          <input ref="writeArea" type="text" v-model = "editItemText" @keyup.enter="editSave"/>
          <button class="btn add" @click="editSave">Save</button>
        </div>
   
        
        <ul class="list">
            <li v-for="(todo,i) in todos" :key="todo.text"> 
                <i
                  @click="checkItem(i)"

                  :class="[todo.state === 'yet' ? 'far': 'fas', 'fa-check-square']"></i>

                  <!-- :class="[todo.state === 'yet' ? 'far': 'fas', 'fa-check-square']"></i> -->

             
            <span>
              {{ todo.text }}

              <b>
                <a href="" @click.prevent="editShow(i)">Edit</a>
                <a href="" @click.prevent="del(i)">Del</a>
              </b>
            </span>
          </li>
        </ul>
      </div>
    </main>
    </div>

</template>

<script>
export default {
    data() {
        return {
          writeState:'add',
          addItemText: '',
          crrEditItem: '',
          editItemText: '',
            todos:[
                {text: '공부하기', state: 'yet'}, //yet일때 far
                {text: '운동하기', state: 'done'}, // fas되야함
                {text: '글쓰기', state: 'done'},
            ]
            }  
    },
    methods: {
      addItem(){
        if(this.addItemText === '') return;
        let value = this.addItemText;
         
        this.todos.push({
            text: value, state: 'yet'
          })
        this.addItemText='';
    
        },
      checkItem(index){
        if(this.todos[index].state === 'yet')
          this.todos[index].state = 'done'
        else if(this.todos[index].state === 'done')
          this.todos[index].state = 'yet'

      },
      editShow(index){
        this.crrEditItem = index; //번호기록
        this.writeState = 'edit';
        this.editItemText = this.todos[index].text

      },
      editSave(){ //몇번을 수정할것인지
        this.todos[this.crrEditItem].text = this.editItemText;
        this.writeState='add'
 
      },
      del(index){
        this.todos.splice(index,1);
      


      }
        
        

      },

      mounted() {
        this.$refs.writeArea.focus();
      }
    }

</script>

<style>

</style>
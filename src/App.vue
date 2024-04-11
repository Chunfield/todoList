<template>
  <div class="container">
    <div class="box">
      <Header @add-data="handleAddData"></Header>
      <InputBox @input-updated ="inputData"></InputBox>
      <div class="todoItems"  v-for="(tag,index) in tags" :key="index">
        <!-- <div @click="deleteItems(index)">{{ tag.text }}</div> -->
        <qwe @click="deleteItems(index)" :tag="tag"></qwe>
        <!-- <TodoItems @notcompleted="notCompleted" @iscompleted="isComlpeted" @sendnum="deleteItems" :mydata="index" :tag="tag"></TodoItems> -->
      </div>
      <div>{{ done }}</div>
    </div>
  </div>
 

</template>

<script>
import Header from './components/Header/index.vue';
import InputBox from './components/InputBox/index.vue';
import TodoItems from './components/TodoItems/index.vue';
import qwe from './components/qwe.vue';
export default{
  components:{
    Header,
    InputBox,
    TodoItems,
    qwe,
  },
  data(){
    return{
      tags:[],
      done:0,
      inputCreated:'',
      complete:false,
    }
  },
  created(){
    const savedTags = localStorage.getItem('tags');  
    if (savedTags) {  
      try {  
        this.tags = JSON.parse(savedTags);  
      } catch (error) {  
        console.error('Error parsing tags from local storage:', error);   
        this.tags = [];  
      }
    }  
  },
  mounted(){
    this.clearLocalStorage();

  },
  methods:{
    deleteItems(data){
      // const afterDelete =this.tags.splice(data,1)
      // console.log(afterDelete)
      // this.filterDone()
      // this.tags.push({text: 'text' + data, complex: false});
      // const d = this.tags.splice(0,1);

      this.tags.splice(data,1);

     
    },
    isComlpeted(data){
      this.tags[data].complete=true;
      console.log(this.tags[data].complete)
      this.filterDone()
    },
    notCompleted(data){
      this.tags[data].complete=false;
      console.log(this.tags[data].complete)
      this.filterDone()
    },
    filterDone() {  
        this.done=0;
      for(let i=0;i<this.tags.length;i++){
        if(this.tags[i].complete==true){
          this.done++
        }
      }  
    },  
    handleAddData(){
      this.tags.push({text:'', complete: false });
      this.inputCreated='';
      this.saveTodos();  
    },
    inputData(data){
      console.log(data)
      this.inputCreated = data
      this.tags.push({
        text:data,complete:false
      });
      this.saveTodos();
    },
    saveTodos(){
      localStorage.setItem('tags', JSON.stringify(this.tags));
    },
    clearLocalStorage() {  
      localStorage.clear();  
    
    }  
  },
  beforeDestroy() {  
      this.saveTodos();
    
    },  

}

</script>
<style>
body{
  margin: 0;
  padding: 0;
}
.created{
  width: 200px;
  height: 200px;
}
.container{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.box{
  
  width: 800px;
  border-radius: 8px;
  background-color:#337ecc;
}

</style>
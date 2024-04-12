<template>
  <div class="container">
    <div class="box">
      <Header @add-data="handleAddData"></Header>
      <InputBox @input-updated ="inputData"></InputBox>
      <div class="todoItems"  v-for="(tag,index) in fliterComplete" :key="index">
        <TodoItems @notcompleted="notCompleted" @iscompleted="isComlpeted" @sendnum="deleteItems" :mydata="index" :tag="tag"></TodoItems>
      </div>
      <div class="footer">
        <div>{{ doneCount }}</div>
        <div>{{ tags.length-doneCount }}</div>
      </div>
      <button @click="ifShowcompelet">Complete</button>
      <button @click="ifShowall">All</button>
    </div>
  </div>
 

</template>

<script>
import Header from './components/Header/index.vue';
import InputBox from './components/InputBox/index.vue';
import TodoItems from './components/TodoItems/index.vue';
export default{
  components:{
    Header,
    InputBox,
    TodoItems,
  },
  data(){
    return{
      tags:[],
      done:0,
      notDone:0,
      inputCreated:'',
      complete:false,
      showCompelet:false,
      showAll:false,
      showNotcompelet:'',
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
    ifShowcompelet(){
      this.showCompelet=true;
      this.showAll=false;
    },
    ifShowall(){
      this.showAll=true;
      this.showCompelet=false
    },
    deleteItems(data){
        this.tags.splice(data,1);
    },
    isComlpeted(data){
      this.tags[data].complete=true;
      console.log(this.tags[data].complete)
    },
    notCompleted(data){
      this.tags[data].complete=false;
      console.log(this.tags[data].complete)
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
  computed: {  
  doneCount() {  
    return this.tags.filter(item => item.complete==true).length
  },
   fliterComplete(){
    if(this.showCompelet){
      return this.tags.filter(item => item.complete==true)
    }
    else if(this.showAll){
      return this.tags
    }
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
.footer{
  display: flex;
}

</style>
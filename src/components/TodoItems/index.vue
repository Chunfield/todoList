<template >
    <div  class="todoItems">
       <ElCheckbox class="roundCheck" id="round" v-model="tag.complete" @click="sendnum"></ElCheckbox>
        <el-input class="todoInput" 
        style="width: 650px;height: 70%;margin-top: auto;
                margin-bottom: auto;
                margin-left: 24px;
                " v-model="tag.text" 
                :class="{ 'strikethrough': tag.complete }"
                :readonly="isWrite"/>
        <div class="content-right">
            <button class="deleteButton" @click="removeDiv"><el-icon style="font-size:32px;color: gray;"><CircleClose /></el-icon></button>
        </div>
    </div>
</template>
<script>
import { ElCheckbox } from 'element-plus';

export default{
    data(){
        return{
            isWrite:false,
        }
    },
    props:{
        mydata:'',
        tag: {
            default: ''  
            },  
         
    },
    
    computed: {  
    isWrite() {  
       
      return this.tag.text.trim() !== '';  
    }
        },
    methods:{
        removeDiv() {  
            this.$emit('sendnum',this.mydata);
            
    },
        sendnum(){
           if(this.tag.complete==true){
            this.$emit('iscompleted',this.mydata);
           }
           else{
            this.$emit('notcompleted',this.mydata);
           }
          
        }  
    },
   
}
</script>
<style>
.todoItems{
    display: flex;
    width: 100%;
    background-color: #a0cfff;
    
    height: 50px;
}
.roundCheck .el-checkbox__inner{
    border-radius: 50%;
    width: 26px !important;
    height: 26px !important; 
    background-color: #fff;   
    border: 1px solid #ccc;  
    cursor: pointer;
    margin-left: 25px;
    margin-top: 25px;
}

.el-checkbox__inner:after{
    height: 14px !important;
    width: 6px !important;
    left: 8px !important;
}

.strikethrough {  
  text-decoration: line-through;  
}  

.deleteButton{
    display: flex;
    margin-top: 8px;
    background: none;
    border: none;
    cursor: pointer;
    border-radius: 50%;
    height: 32px;
    width: 32px;
}
.content-left{
    display: flex;
    margin-left: 20px;
    align-self: center;
    width: 20px; 
    height: 20px;  
    border-radius: 50%; 
    cursor: pointer;
    border: 2px solid black;
  background-color: transparent; 
}
</style>

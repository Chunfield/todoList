<template>
    <div class="inputBox">
        <!-- <input 
        class="create-input"
        type="text"  
        v-model="inputValue"
        placeholder="What needs to be done?"
      /> -->
      <el-input 
            v-model="inputValue"
            style="width: 650px;height: 80%;;font-size: 20px;"
            placeholder="What needs to be done?"
            clearable
            @keyup.enter="sendValue" 
            />
    </div>

</template>
<script>
export default{
    data(){
        return{
            inputValue: '',
        }
    },
    methods:{
        sendValue(){
            this.$emit('input-updated', this.inputValue);
            this.inputValue = '';
        }
    },
}
</script>
<style>
.inputBox{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 60px;
    
}
.el-input__clear {  
  font-size: 20px !important;  
}
/* .create-input{
    width: 80%;
    height: 40px;
    } */

</style>
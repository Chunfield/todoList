<template>
    <div class="headerbar">
        <div class="bar-title">TodoList</div>
        <div class="bar-button">
            <!-- <button class="create" @click="clickAdd">添加</button> -->
            <el-button type="success" class="create" size="medium" @click="clickAdd">添加</el-button>
            <!-- <button class="select"></button> -->
        </div>
    </div>
</template>
<script>
export default{
    
    methods:{
        clickAdd(){
            console.log(1)
            this.$emit('add-data', { id: Date.now(), content: '' });
        },
    }
}
</script>
<style>
.headerbar{
    display: flex;
    justify-content: space-between;
    width: 100%;
    height: 80px;
    /* background-color: rgb(239, 111, 111);  */
}
.bar-title{
    display: flex;
    align-items: center;
    margin-left: 10px;
    font-size: 32px;
}
.bar-button{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 200px;
    
}
.create{

    margin-right: 20px;
    width: 70px;
}
.select{
    width: 60px;
    height: 40px;
    border-radius: 8px;
    border: none;
    background-color: rgb(249, 0, 0);
}
</style>
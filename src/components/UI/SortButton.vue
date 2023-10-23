<template>
    <button class="btns">
        <slot></slot>
    </button>

</template>

<script>
export default {
    name: 'SortButton',
   
}
   
</script>

<style scoped>
 .btns {
  height: 25px;
  width: 15%;
  outline: none;
  background-color: aliceblue;
  border-radius: 10px;
  border: 2px solid darkslategrey;
  box-shadow: 5px 5px 5px #999;
 } 

 

 .active-sort {
    box-shadow: 0 0 10px 5px darkslategrey;
    background-color: white;
    height: 35px ;
 }

 .confirm-active {
  color: white;
  background-color:  darkslategrey !important;
  box-shadow: 5px 5px 5px #999 !important;
  
}
</style>
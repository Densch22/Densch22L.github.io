<template> 
<!--Set Background based on if Published-->
 <div :class="book.published ? 'green' : 'red' ">
           {{ book.title }}
   </div>
</template>

<script>

//Send data to Parent boxForm
export default {
  name: 'inOne',

  //From Parent boxForm
  props:{
    book: Array
  }
};

</script>

<style scoped>
  /* green or red background */
.green{
    background: rgb(0, 75, 0);
}
.red{
    background: rgb(175, 0, 0);
}

 /* format for each grid value */
div{
  padding: 20px;
  font-weight: bold;
  color: white;
  border-radius: 8px;
  min-height: 100px;
  text-align: center;
}
</style>
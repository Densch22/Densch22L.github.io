<template>

<div class="boxForm"> 

    <!--Send each book in the array to child inOne-->
    <div v-for="book of books" :key="book.id">
        
      <!--Call Child inOne Component-->
         <inOne :book="book" /> 
    </div>
    
</div>

</template>

<script>

//Import Child inOne
import inOne from './inOne.vue';

// Send data to Parent App
export default {
  name: 'boxForm',

  //From Parent APP
  props:{
    books: Array
  },

  //To Child inOne
  components:{
    inOne
  }
};

</script>

<style scoped>

   /* grid format to handle dynamic imput amounts*/
.boxForm{
   display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 0.5rem;
    grid-template-areas:repeat(3, 1fr);
}

 /* small screens */
@media (max-width: 620px) {
  .boxForm {
    grid-template-columns: 1fr; 
  }}

</style>
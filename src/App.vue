<template>
   
   <Header />
   
  <div class="container">

    <Courses>
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="#">Home</a></li>
        <li class="breadcrumb-item active" aria-current="page">liste des cours</li>
      </ol>
       <template v-slot:button-right>
         <button class="btn btn-sm btn-success">Ajouter Cours </button>
       </template>
    </Courses>

  </div> 

  <Footer 
     url="Ensemble pour comprendre Vue js" 
     title="BAGHROSSE Rachid app" 
     text="preseverer pour avoir une attestation "
     />

</template>

<script>

import Header from './components/Header';
import Courses from './components/Courses';
import Footer from './components/Footer';
export default {
  name: 'App',
  components: {
    Header,
    Courses,
    Footer
  },
  data() {
    return {
    }
  },
  methods: {
    handleClick() {
      console.log(this.$refs.book.value)
      this.$refs.book.classList.add('active');
      this.$refs.book.focus();
    }
  }
}
</script>

<style>
  .container {
    margin-top: 60px;
  }

</style>

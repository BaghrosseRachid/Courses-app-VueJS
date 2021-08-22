<template lang="">
   
   <form @submit.prevent="newCourse">

      <div class="form-group">
         <label for="Title">Titre</label>
         <input v-model="title" id="Title" type="text" class="form-control">
      </div>
   
      <div class="form-group">
         <label for="Image">url de l'Image </label>
         <input v-model="image" id="Image" type="text" class="form-control">
      </div>
   
      <div class="form-group">
         <label for="category">Catégorie</label>
         <select v-model="category" id="category" class="form-control">
            <option :value="myCategory.id" v-for="myCategory in categories">
               {{ myCategory.name }}
            </option>
         </select>
      </div>
   
      <div class="form-check form-check-inline my-3">
         <label class="form-check-label">
            <input v-model="typeOfPayment" class="form-check-input" type="radio" name="typeOfPayment" value="free"> Gratuit
         </label>
   
         <label class="form-check-label ml-3">
            <input v-model="typeOfPayment" class="form-check-input" type="radio" name="typeOfPayment" value="paying"> payant
         </label>
      </div>
   
   
      <div class="my-3">
         <h5>Types</h5>
         <div class="form-check" v-for="tag in tags">
           <label class="form-check-label">
             <input type="checkbox" class="form-check-input" :value="tag" v-model="myTags">
             {{ tag }}
           </label>
         </div>
      </div>
   
      <button type="submit" class="btn btn-block btn-warning">Ajouter cours</button>
   </form>

</template>

<script>
export default {
    data() {
       return {
          title: 'Titre du cours',
          image: 'image url',
          categories: [
             { id: 1, name: 'Frontend' },
             { id: 2, name: 'Backend' },
             { id: 3, name: 'Mobile' },
          ],
          category: 3,
          typeOfPayment: 'paying',
          tags: ['Framework', 'Frontend', 'Backend', 'Javascript'],
          myTags: []
       }
    },
    methods: {
      newCourse() {
         let title = this.title;
         let image = this.image;

         if(title == "" || image == "") {
            return;
         }

         const course = {
            title,
            image,
            category: this.categories.find(category => category.id == this.category).name,
            tags: this.myTags
         }

         this.$emit('add', course)
         this.$refs.title.value = "";
         this.$refs.image.value = "";
      }
    }
}
</script>

<style lang="">
    
</style>
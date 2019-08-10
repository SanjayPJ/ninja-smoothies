<template>
  <div class="add-smoothie card p-4 mt-3">
    <h4 class="pb-4 center-align">Add New Smoothie Recipe</h4>
   <form @submit.prevent="submitSmoothie">
      <div class="field title">
      <label for="title">Smoothie Title: </label>
      <input type="text" name="title" id="title" v-model="title">
    </div>
    <div class="chip-container py-3">
      <div class="chip" v-for="(ingredient, index) in ingredients" :key="index">
          {{ ingredient }}
          <i class="close material-icons" @click="chipClick(index)">close</i>
      </div>     
      </div>
    <div class="field add-ingredient">
      <label for="add-ingredient">Add An Ingredient: </label>
      <input type="text" name="add-ingredient" id="title" @keydown.tab="addIngredient" v-model="another">
    </div>
    <div class="field center-align">
      <button type="submit" class="btn pink mt-4 block">Add Smoothie</button>
    </div>
   </form>
  </div>
</template>

<script>
import db from '@/firebase/init'
import slugify from 'slugify'

export default {
  name: 'AddSmoothie',
  data(){
    return {
      title: null,
      another: null,
      ingredients: [],
    }
  }, 
  methods: {
    submitSmoothie(){
      if(this.title !== null && this.ingredients !== null){
        const slug = slugify(this.title, {
          replacement: '-',
          lower: true
        });
        db.collection('smoothies').add({
          title: this.title,
          ingredients: this.ingredients,
          slug: slug
        }).then(() => {
          this.$router.push({ name: "home" });
        })
      }
    },
    addIngredient(e){
      if(this.another !== null){
        this.ingredients.push(this.another); 
        this.another = null;
      }
      e.preventDefault();
    } ,
    chipClick(id){
      this.ingredients = this.ingredients.filter((ingredient, index) =>  index != id);
    }
  }
}
</script>

<style scoped>
.add-smoothie{
  max-width: 500px;
  margin: 0 auto;
}
.block{
  width: 100%;
}
</style>





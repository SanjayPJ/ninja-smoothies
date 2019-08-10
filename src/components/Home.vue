<template>
  <div class="container">
       <div class="row">
            <div class="col s4 mt-2" v-for="(smoothie, index) in smoothies" :key="index">
                <div class="card">
                    <div class="card-content">
                    <span class="card-title">{{ smoothie.title }}</span>
                    <div class="mt-3">
                        <div class="chip" v-for="(ingredient, index) in smoothie.ingredients" :key="index">
                            {{ ingredient }}
                            <i class="close material-icons">close</i>
                        </div>                        
                    </div>
                     <router-link :to="{ name: 'edit', params: { slug: smoothie.slug }}" class="btn-floating btn-large halfway-fab pink waves-effect waves-light">
                        <i class="material-icons">edit</i>
                    </router-link>
                     <a class="btn-floating mt-4 pink waves-effect waves-light" @click.prevent="deleteSmoothie(smoothie.id)">
                        <i class="material-icons">delete</i>
                    </a>
                    </div>
                </div>
            </div>
        </div>  
  </div>
</template>

<script>
import db from '@/firebase/init'

export default {
  name: 'Home',
  data(){
      return {
          smoothies: [],
      }
  },
  methods: {
      deleteSmoothie(id){
          db.collection('smoothies').doc(id).delete().then(() => {
              this.smoothies = this.smoothies.filter(smoothie => { return smoothie.id != id});
          })
      }
  },
  created(){
      db.collection('smoothies').get().then(snapshot => {
          snapshot.forEach(doc => {
              const smoothie = {
                  ...doc.data(),
                  id: doc.id,
              }
              this.smoothies.push(smoothie);
          });
      })
  }
}
</script>

<template>
  <div id="app">
      <HeaderComponent />
    <div class="container">
      <div v-if="isNewRecipe">
        <recipe-form @formSaved="setRecipeList"></recipe-form>
      </div>
      <div class="row">
        <div class="col">
            <button class="btn btn-success float-right"
            @click="isNewRecipe=!isNewRecipe"
            >Add+</button> 
        </div>
         </div>

          <div class="row pt-4">
          <div class="col">
             Search : <input type="text" class="form-controll" v-model="searchTitle">
          </div>
          </div>
        <!-- Content here -->
         <div class="row pt-4">
          <div class="col-sm-12 col-md-3" v-for = "recipe in filterList" :key="recipe.id" >   
            <recipe-card
        @recipetedDelete="deleteRecipe"
        :key ="recipe.id" :recipe=recipe>
        </recipe-card>
          </div>
          </div>  
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HeaderComponent from './components/Header.vue'
import RecipeCard from './components/RecipeCard.vue'
import RecipeForm from './components/RecipeForm.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    HeaderComponent,
    RecipeCard,
    RecipeForm
  },
  data () {
    return {
      isNewRecipe: false,
      recipes: [{
        id: '1',
        title: 'Deadpool',
        description: 'SuperHero Dark',
        image: 'http://www.moviesbook.it/wp-content/uploads/2015/03/deadpoollogo.jpg'
      }],
      searchTitle :''
    }
  },
  computed :{
    filterList(){
      console.log("COMPUTED")
      return this.recipes.filter(recipe=>{
        // return recipe.title === this.searchTitle
        return recipe.title.toLowerCase().indexOf(this.searchTitle.toLowerCase())>-1 //ค่าว่าง TRUE
      })
    }
  },
  methods: {
    setRecipeList(recipe) {
      this.recipes.push(recipe)  
              this.isNewRecipe = false
                },
                deleteRecipe(id){
                  const index = this.recipes.findIndex((value) => value.id === id)
                  this.recipes.splice(index,1)
                  alert('Delete')
                }
  },
  mounted(){
    console.log("MOUNT")
    if(localStorage.getItem('recipes')){
      this.recipes = JSON.parse(localStorage.getItem('recipes'))
      // console.log(this.recipes  )
      // alert(localStorage.getItem('recipes'))
    }
  },
  watch:{   //ดูค่าที่เปลี่ยน 
    recipes:{
      handler(){  //watch ข้างในด้วย
        localStorage.setItem('recipes', JSON.stringify(this.recipes))
      },
      deep:true //ดูหลาย Level Object ข้างในด้วย
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

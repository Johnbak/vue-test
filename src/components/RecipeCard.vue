<template>
    <div>
       <div class="card" style="width: 18rem;">
  <img class="card-img-top" :src="recipe.image" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">{{recipe.title}}</h5>
    <p class="card-text">{{recipe.description}}</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
    <button 
    @click="sendDelete" class="btn btn-danger">Delete</button>
    <button class="btn btn-info">???</button>
  </div>
</div>
    </div>
</template>

<script>
export default {
  props: {
    recipe: {
      type: Object,
      required: true
    }
  }
,methods: {
  sendDelete() {
    this.$emit('recipetedDelete', this.recipe.id)
  }
},
}
</script>

<style scoped>

</style>
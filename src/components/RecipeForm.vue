<template>
  <div>
    <form @submit.prevent ="save"> <!-- not reload : save is function--> 
      <div class="form-group">
        <label for="">Title</label>
        <input type="text" class="form-control" id="" placeholder="Example input"
        v-model="recipe.title">
      </div>
      <div class="form-group">
        <label for="">Description</label>
        <input type="text" class="form-control" id="formGroupExampleInput2" placeholder="Another input"
        v-model="recipe.description">
      </div>
      <div class="form-group">
        <label for="">Image</label>
        <input type="text" class="form-control" id="formGroupExampleInput2" placeholder="Another input"
        v-model="recipe.image">
      </div>
      <button class="btn btn-success"> Save</button>  <!-- @click="save"-->
       <button class="btn btn-danger">Cancel</button>
       {{recipe}}
    </form>
  </div>
</template>

<script>
export default {
  data() {
      return {
        recipe: {
          id:'',
          title:'',
          description:'',
          image:''
        }
      }
    },
    methods: {
      save() {
        this.recipe.id = Math.random()
        this.$emit('formSaved', this.recipe)
      }
    },
}
</script>

<style scoped>

</style>
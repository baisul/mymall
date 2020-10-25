<template>
  <div class="wrapper">
    <ul class="content">
      <li>分类列表1</li>
      <li>分类列表2</li>
      <li>分类列表3</li>
      <li>分类列表4</li>
    </ul>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
    export default {
        name: "Category",
      data() {
          return{
            scroll: null
          }
      },
      /*created() {
         this.scroll =  new BScroll('.wrapper',{

          })
      }*/
      mounted() {
        this.scroll = new BScroll('.wrapper',{

        })
      }
    }
</script>

<style scoped>
  .wrapper{
    height: 150px;
    background-color: red;

    /*overflow: hidden;
    overflow-y: scroll;*/
  }
</style>

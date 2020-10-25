<template>
  <div class="tab-controll">
    <div v-for="(item,index) in titles"
         class="tab-controll-item" :class="{active: index === currentIndex}"
        @click="changeItem(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
    export default {
      name: "TabControll",
      props: {
        titles: {
          type: Array,
          default() {
            return []
          }
        }
      },
      data(){
        return{
          currentIndex: 0
        }
      },
      methods: {
        changeItem (index){
          this.currentIndex = index;
          //发射事件，告诉父组件，父组件要接收
          this.$emit("tabClick",index)
        }
      }
    }
</script>

<style scoped>
  .tab-controll{
    display: flex;
    text-align: center;
    font-size: 15px;
    height: 40px;
    line-height: 40px;
    background-color: #fff;
  }
  .tab-controll-item{
    flex: 1;
  }
  .tab-controll-item span{
    padding: 5px;
  }
  .active{
    color: #ff5777;
  }
  .active span{
    border-bottom: 3px solid #ff8198;
  }
</style>

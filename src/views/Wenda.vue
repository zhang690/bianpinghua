<template>
  <div>
    <div class="father">
      <div>1</div>
      <div>2</div>
      <div>3</div>
      <div class="pre">4</div>
      <div class="active">5</div>
      <div class="next">6</div>
      <div>7</div>
      <div>8</div>
      <div>9</div>
      <div>10</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
  methods: {},
  // mounted() {
  //   this.$axios.get(
  //       'https://qu.xinli001.com/lingxi/fun/getFunQuestionsOptions?channelId=513&id=1768&userAwaitTestScaleId=0&appCode=1'
  //     ).then(res=>{
  //       console.log(res)
  //       this.src = res.data.data.introPicture
  //     })
  // },
};
</script>
<style lang="less">
  .father {
    position: relative;
    
  }
  .father div:nth-of-type(n){
    position: absolute;
    top:0;
    background-color: green;
    left: 0;
    width:335px;
    height:500px;
  }
  .father .active {
      right:50%;
      transform: translateX(50%);
    }
</style>

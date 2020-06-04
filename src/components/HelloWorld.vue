<template>
  <div>
    <div
      v-for="(item, index) in findData"
      :key="index"
      :class="[
        {
          first: item.first,
          second: item.second,
          third: item.third,
          hideAnimation: item.level == 3 && item.child == true,
          showAnimation: item.level == 3 && item.child == false,
        },
      ]"
      @click="change(item)"
    >
      {{ item.title }}
    </div>

    <button @click="isShow">按钮</button>
    <div :class="[box]" ref="box"></div>
  </div>
</template>

<script>
import falseData from '../../public/test';
export default {
  name: 'HelloWorld',
  data() {
    return {
      findData: [],
      box: 'box1',
    };
  },
  mounted() {
    console.log(falseData);
    this.flat(falseData);
    console.log(this.findData);
  },
  methods: {
    isShow() {
      this.box = this.box == 'box1' ? 'box2' : 'box1';
      this.$router.push('/Wenda')
      
    },
    // 点击事件
    change(obj) {
      console.log(obj.id);
      if (obj.flagArr.length < 2) {
        return;
      }
      if (obj.level == 3) {
        return;
      }
      this.findData.forEach((item) => {
        if (item.flagArr.length > 2) {
          // item.flagArr.forEach((i) => {
          //   if (i == obj.id) {
          //     item.child = !item.child;
          //   }
          // });
          if (item.flagArr.includes(obj.id)) {
            item.child = !item.child;
          }
        }
      });
    },
    // 扁平化
    flat(data, arr = []) {
      data.forEach((item) => {
        let obj = {};
        obj.title = item.title;
        obj.level = item.level;
        obj.id = item.id;
        obj.child = item.child;
        let flagArr = [...arr];
        if (item.level == 1) {
          obj.first = true;
        } else if (item.level == 2) {
          obj.second = true;
        } else {
          obj.third = true;
        }
        this.findData.push(obj);
        flagArr.push(item.id);
        if (item.list) {
          this.flat(item.list, flagArr);
        }
        obj.flagArr = flagArr;
      });
    },
  },
};
</script>
<style lang="less">
.box1 {
  width: 100%;
  height: 20px;
  background-color: gray;
}
.box2 {
  width: 100%;
  height: 20px;
  background-color: red;
}
.first {
  height: 40px;
  font-size: 22px;
  line-height: 40px;
  padding-left: 10px;
  background-color: gray;
}
.second {
  height: 30px;
  font-size: 20px;
  line-height: 30px;
  padding-left: 20px;
  background-color: #ffe4e1;
}
.third {
  height: 30px;
  font-size: 16px;
  line-height: 30px;
  padding-left: 30px;
  background-color: #fff;
  overflow: hidden;
  box-sizing: border-box;
}
.showAnimation {
  animation: letShow 0.3s forwards;
}
.hideAnimation {
  animation: letHide 0.3s forwards;
}
@keyframes letHide {
  0% {
    width: 100%;
    height: 30px;
  }
  100% {
    width: 0;
    height: 0;
  }
}
@keyframes letShow {
  0% {
    width: 0;
    height: 0;
  }
  100% {
    width: 100%;
    height: 30px;
  }
}
</style>

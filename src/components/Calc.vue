<template>
  <div class="calc">
    <div class="input">
      <input v-model.number="kouchang" :disabled="calcWhich===0">
      <input v-model.number="toufen" :disabled="calcWhich===1">
      <input v-model.number="kouhao" :disabled="calcWhich===2">
    </div>
    <div class="formula">
      <span @click="calcWhich=0">筘长</span> =
      <span @click="calcWhich=1">头份</span> ÷
      <span @click="calcWhich=2">筘号</span>
      ÷ 4 x 2 x 2.54
    </div>
    <div class="calcing" :style="{transform: `translateX(${76*calcWhich}px)`}"></div>
    <p class="tips">使用方法:点击想要计算的项目，输入其他两个</p>
  </div>
</template>

<script>
export default {
  name: 'Calc',
  data: () => ({
    kouchang: undefined,
    toufen: undefined,
    kouhao: undefined,
    calcWhich: 0
  }),
  watch: {
    kouchang() {
      this.calc();
    },
    toufen() {
      this.calc();
    },
    kouhao() {
      this.calc();
    }
  },
  methods: {
    calc() {
      switch (this.calcWhich) {
        case 0:
          if (!(this.toufen && this.kouhao)) return;
          this.kouchang = this.toufen / this.kouhao / 4 * 2 * 2.54;
          break;
        case 1:
          if (!(this.kouchang && this.kouhao)) return;
          this.toufen = this.kouchang / 2.54 / 2 * 4 * this.kouhao;
          break;
        case 2:
          if (!(this.toufen && this.kouchang)) return;
          this.kouhao = this.toufen / (this.kouchang / 2 / 2.54 * 4);
          break;
      }
    }
  }
};
</script>

<style scoped lang="scss">

.calc {
  font-size: 24px;
  width: fit-content;
  margin: 0 auto;

  .input {
    display: flex;

    input {
      width: 48px;
      display: inline-block;
      border: 2px solid gray;
      border-radius: 4px;
      padding: 8px;
      margin: 16px 0;
      transition: 0.3s;

      &:disabled {
        border-color: transparent;
        background-color: orangered;
        color: white;
        width: 72px;
        transform: translateY(-120%) translateX(-12px);
        margin-right: -24px;
      }
    }
  }

  .formula {
    width: fit-content;

    span {
      font-weight: bolder;
    }
  }

  .calcing {
    width: 0;
    height: 0;
    border: 10px solid transparent;
    border-bottom-color: orangered;
    transition: 0.3s;
    margin-left: 14px;
  }

  .tips {
    font-size: 14px;
    text-align: left;
  }

}


</style>
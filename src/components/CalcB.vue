<template>
  <div class="calcB">
    <div class="input">
      <input v-model.number="ratioPingsha" class="input-a">:
      <input v-model.number="ratioZhujiesha" class="input-b">
      <input v-model.number="zongjing" class="input-c">
    </div>
    <div class="formula">
      <span>平纱 <span :class="{active:showRes}" class="result">{{ resPingsha }}</span> </span> +
      <span>竹节纱布 <span :class="{active:showRes}" class="result result-2">{{ resZhujiesha }}</span> </span> =
      <span>总经</span>
    </div>
    <p class="tips">使用方法:总经上方输入框输入值，平纱和竹节纱上方输入比例后，下方现实结果</p>
  </div>
</template>

<script>
export default {
  name: "CalcB",
  data: () => ({
    ratioPingsha: undefined,
    ratioZhujiesha: undefined,
    zongjing: undefined,
    resPingsha: undefined,
    resZhujiesha: undefined,
  }),
  computed: {
    showRes() {
      return this.ratioPingsha && this.ratioZhujiesha && this.zongjing
    }
  },
  watch: {
    ratioPingsha() {
      this.calc()
    },
    ratioZhujiesha() {
      this.calc()
    },
    zongjing() {
      this.calc()
    },
  },
  methods: {
    calc() {
      if (!(this.ratioPingsha && this.ratioZhujiesha && this.zongjing)) return
      this.resPingsha = this.zongjing / (this.ratioPingsha + this.ratioZhujiesha) * this.ratioPingsha
      this.resZhujiesha = this.zongjing / (this.ratioPingsha + this.ratioZhujiesha) * this.ratioZhujiesha
    }
  }
}
</script>

<style lang="scss" scoped>
.calcB {
  font-size: 24px;
  text-align: left;
}

.input {
  input {
    display: inline-block;
    border: 2px solid gray;
    border-radius: 4px;
    padding: 8px;
    margin-bottom: 16px;
  }

  &-a {
    width: 28px;
    margin-right: 10px;
  }

  &-b {
    width: 28px;
    margin-left: 4px;
  }

  &-c {
    width: 48px;
    margin-left: 70px;
  }
}

.formula {
  > span {
    font-weight: bolder;
    position: relative;

    .result {
      position: absolute;
      left: 0;
      transition: 0.3s;
      opacity: 0;

      &.active {
        opacity: 1;
        transform: translateY(230%);
      }

      &-2.active {
        transform: translateY(320%);
      }
    }
  }
}

.tips {
  font-size: 14px;
  text-align: left;
  margin-top: 0;
}
</style>
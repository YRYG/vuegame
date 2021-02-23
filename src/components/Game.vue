<template>
  <div>
    <div class="game-group">
      <div class="game-item" @click="setOption(index)" v-for="(item,index) in options" :key="index">
        <span>{{item}}</span>
      </div>
    </div>
    <h2>
      {{stop ? 'Winner' : 'Next player'}}:
      <span>{{value}}</span>
    </h2>
    <ul>
      <li>
        <span>1.</span>
        <span class="text" @click="reset()">Go to game start</span>
      </li>
      <li v-for="(item,index) in record" :key="index">
        <span>{{index+2}}.</span>
        <span class="text" @click="changeRecord(index)">Go to move # {{ index+1 }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: ["", "", "", "", "", "", "", "", ""],
      answer: [
        "1,2,3",
        "4,5,6",
        "7,8,9",
        "1,4,7",
        "2,5,8",
        "3,6,9",
        "1,5,9",
        "3,5,7"
      ],
      record: [],
      value: "X",
      stop: false
    };
  },
  methods: {
    reset() {
      this.options = ["", "", "", "", "", "", "", "", ""];
      this.record = [];
      this.value = "X";
      this.stop = false;
    },
    getOptions() {
      console.log(this.options);
    },
    setOption(index) {
      if (this.options[index] === "" && !this.stop) {
        var arr2 = [...this.options];
        arr2[index] = this.value;
        this.options = arr2;
        this.record.push({ arr: this.options, value: this.value });
        this.value = this.value == "X" ? "O" : "X";
      }
    },
    changeRecord(index) {
      this.options = this.record[index].arr;
      this.value = this.record[index].value == "X" ? "O" : "X";
      this.record = this.record.slice(0, index + 1);
      this.stop = false;
    }
  },
  watch: {
    options: {
      deep: true,
      handler(n, o) {
        const that = this;
        for (let i = 0; i < that.answer.length; i++) {
          let arr = that.answer[i].split(",");
          const n1 = parseInt(arr[0]) - 1;
          const n2 = parseInt(arr[1]) - 1;
          const n3 = parseInt(arr[2]) - 1;
          let code1 = n[n1];
          let code2 = n[n2];
          let code3 = n[n3];

          if (code1 == "" && code2 == "" && code3 == "") continue;

          if (code1 == code2 && code1 == code3) {
            this.stop = true;
            this.value = this.value == "X" ? "O" : "X";
          }
        }
      }
    }
  }
};

// SKILL IMPROVEMENT
</script>

<style scoped lang="scss">
.game-group {
  width: 600px;

  &::after {
    content: "";
    display: block;
    clear: both;
    opacity: 0;
    visibility: hidden;
    height: 0;
  }
}

.game-item {
  width: 200px;
  height: 200px;
  border: 1px solid gray;
  position: relative;
  box-sizing: border-box;
  float: left;
  text-align: center;

  input {
    display: none;
  }

  span {
    display: block;
    width: 100%;
    font-size: 180px;
    font-weight: bold;
    height: 100%;
  }
}

li {
  list-style: none;

  .text {
    border: 1px solid gray;
    border-radius: 10px;
    padding: 2px 10px;
    line-height: 30px;
    cursor: pointer;
  }
}
</style>
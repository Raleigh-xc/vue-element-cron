<template>
  <div class="vue-element-cron">
    <el-input v-if="showValue" :value="valueArr.join(' ')" readonly> </el-input>

    <el-tabs v-model="activeTab" stretch>
      <el-tab-pane v-if="useSeconds" label="秒" name="Second">
        <span slot="label"><i class="el-icon-date"></i> 秒</span>
        <Second @change="hanleValueChange" />
      </el-tab-pane>
      <el-tab-pane label="分" name="Minute">
        <span slot="label"><i class="el-icon-date"></i> 分</span>
        <Minute @change="hanleValueChange" />
      </el-tab-pane>
      <el-tab-pane label="时" name="Hour">
        <span slot="label"><i class="el-icon-date"></i> 时</span>
        <Hour @change="hanleValueChange" />
      </el-tab-pane>
      <el-tab-pane label="日" name="Date">
        <span slot="label"><i class="el-icon-date"></i> 日</span>
        <MDay @change="hanleValueChange" />
      </el-tab-pane>
      <el-tab-pane label="月" name="Month">
        <span slot="label"><i class="el-icon-date"></i> 月</span>
        <Month @change="hanleValueChange" />
      </el-tab-pane>
      <el-tab-pane label="周" name="Day">
        <span slot="label"><i class="el-icon-date"></i> 周</span>
        <WDay @change="hanleValueChange" />
      </el-tab-pane>
      <el-tab-pane v-if="useYears" label="年" name="Year">
        <span slot="label"><i class="el-icon-date"></i> 年</span>
        <Year @change="hanleValueChange" />
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
// import cron from "cron-validate";
import Second from "./widgets/Second";
import Minute from "./widgets/Minute";
import Hour from "./widgets/Hour";
import MDay from "./widgets/MDay";
import Month from "./widgets/Month";
import WDay from "./widgets/WDay";
import Year from "./widgets/Year";

const DEFAULT_CRON = "* * * * ?";

export default {
  name: "Cron",
  components: {
    Second,
    Minute,
    Hour,
    MDay,
    Month,
    WDay,
    Year,
  },

  props: {
    showValue: {
      type: Boolean,
      default: true,
    },
    useSeconds: {
      type: Boolean,
      default: true,
    },
    useYears: {
      type: Boolean,
      default: true,
    }
  },

  data() {
    return {
      activeTab: "Second",
      valueArr: [],
    };
  },

  created() {
    const { useSeconds, useYears } = this;
    let cron = DEFAULT_CRON;
    cron = useSeconds ? "* " + cron : cron;
    cron = useYears ? cron + " *" : cron;
    this.valueArr = cron.split(" ");
  },

  // watch: {
  //   valueArr(value) {
  //     this.$emit("change", value.join(" "));
  //   },
  // },

  methods: {
    setCron() {},

    getCron() {
      return this.valueArr.join(" ");
    },

    hanleValueChange(data) {
      const { index, value } = data;
      this.$set(this.valueArr, index, value);
      // console.log(
      //   cron(this.getCron(), {
      //     override: {
      //       useSeconds: true,
      //       useYears: true,
      //       useBlankDay: true,
      //       useLastDayOfMonth: true,
      //       useLastDayOfWeek: true,
      //       useNearestWeekday: true,
      //       useNthWeekdayOfMonth: true,
      //     },
      //   })
      // );
    },
  },
};
</script>

<style>
.vue-element-cron .el-input__inner {
  text-align: center;
}

.vue-element-cron .el-radio-group > div:not(:last-child) {
  margin-bottom: 10px;
}

.vue-element-cron .el-input-number {
  width: 100px;
}

.vue-element-cron .el-select {
  width: 300px;
}

.vue-element-cron .el-select.single {
  width: 100px;
}

.vue-element-cron .text {
  font-size: 12px;
}

.vue-element-cron .show-value {
  font-size: 14px;
  font-weight: bold;
}
.vue-element-cron .show-value::after {
  content: "";
  display: block;
  margin-top: 10px;
}

.vue-element-cron .ml10 {
  margin-left: 10px;
}

.vue-element-cron .mr10 {
  margin-right: 10px;
}
</style>
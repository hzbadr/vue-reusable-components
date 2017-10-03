<template>
  <div>
    <select @change="(event) => { dateRangeChanged(event.target.value) }">
      <option v-for="(option, value) in rangeTypeOptions" :value="value" :key="value">{{ option }}></option>
    </select>
  </div>  
</template>

<script>
export default {
  data () {
    return {
      rangeTypeOptions: {
        yesterday: 'Yesterday',
        today: 'Today',
        thisweek: 'This Week',
        lastweek: 'Last Week',
        thismonth: 'This Month',
        lastmonth: 'Last Month',
        last3months: 'Last 3 Months',
        last6months: 'Last 6 Months'
      }
    }
  },

  methods: {
    calculateRangeForType(rangeType){
      // TODO
    },
    dateRangeChanged(rangeType){
      var dateRange = this.calculateRangeForType(rangeType)
      this.$emit('input', dateRange)
    }
  }
}
</script>

<style scoped>

</style>

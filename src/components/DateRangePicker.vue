<template>
  <div>
    <select @change="(event) => { dateRangeChanged(event.target.value) }" v-model="selectedRangeType">
      <option v-for="(option, value) in rangeTypeOptions" :value="value" :key="value">{{ option }}</option>
    </select>
    <div v-if="selectedRangeType == 'custom'">
      <label> From: <date-picker v-model="fromPickedDate" fromat="MM/dd/yyyy"></date-picker></label>
      <label> To: <date-picker v-model="toPickedDate" fromat="MM/dd/yyyy"></date-picker></label>
    </div>  
  </div>  
</template>

<script>
import moment from 'moment'
import DatePicker from 'vuejs-datepicker'

export default {
  components: {
    'date-picker': DatePicker
  },
  data () {
    return {
      fromPickedDate: null,
      toPickedDate: null,
      selectedRangeType: null,
      rangeTypeOptions: {
        yesterday: 'Yesterday',
        today: 'Today',
        thisweek: 'This Week',
        lastweek: 'Last Week',
        thismonth: 'This Month',
        lastmonth: 'Last Month',
        last3months: 'Last 3 Months',
        last6months: 'Last 6 Months',
        custom: 'Custom'
      }
    }
  },

  methods: {
    calculateRangeForType(rangeType){
      switch(rangeType){
        case 'yesterday':
          return {
            from: moment().subtract(1, 'day').startOf('day').toDate(),
            to: moment().subtract(1, 'day').endOf('day').toDate()
          }
        case 'today':
          return {
            from: moment().startOf('day').toDate(),
            to: moment().endOf('day').toDate()
          }
        case 'thisweek':
          return {
            from: moment().startOf('week').toDate(),
            to: moment().endOf('week').toDate()
          }
        case 'lastweek':
          return {
            from: moment().subtract(1, 'week').startOf('week').toDate(),
            to: moment().subtract(1, 'week').endOf('week').toDate()
          }
        case 'thismonth':
          return {
            from: moment().startOf('month').toDate(),
            to: moment().endOf('month').toDate()
          }
        case 'lastmonth':
          return {
            from: moment().subtract(1, 'month').startOf('month').toDate(),
            to: moment().subtract(1, 'month').endOf('month').toDate()
          }
        case 'last3months':
          return {
            from: moment().subtract(3, 'month').startOf('month').toDate(),
            to: moment().endOf('month').toDate()
          }
          
        case 'last6months':
          return {
            from: moment().subtract(6, 'month').startOf('month').toDate(),
            to: moment().endOf('month').toDate()
          }
        default:
          return null
      }
    },
    dateRangeChanged(rangeType){
      if(this.selectedRangeType == 'custom'){
        if(this.fromPickedDate == null || this.toPickedDate == null){
          return
        }else{
          let dateRange = {
            from: moment(this.fromPickedDate).startOf('day').toDate(),
            to: moment(this.toPickedDate).endOf('day').toDate()
          }
          this.$emit('input', dateRange)
        }
      }else{
          let dateRange = this.calculateRangeForType(rangeType)
          this.$emit('input', dateRange)
      }
    }
  }
}
</script>

<style scoped>
.date-range-picker{
  padding: 5px;
}
</style>

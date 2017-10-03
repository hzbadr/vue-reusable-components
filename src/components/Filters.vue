<template>
  <div class="filter">
    <div class="filter">
      <label for="component-dropdown">Component-based dropdown: </label>
      <dropdown id="component-dropdown" :options="fruitOptions" v-model="selectedFruit"></dropdown>
    </div>

    <div class="filter">
      <label for="autocomplete-dropdown">Autocomplete dropdown: </label>
      <autocomplete-dropdown id="autocomplete-dropdown" 
                             :options="fruitOptions"
                             v-model="selectedFruit" 
                             placeholder="Enter a fruit name"></autocomplete-dropdown>
    </div>

    <div class="result">
      Selected: <strong>{{ selectedFruit}}</strong>
    </div>
  </div>
</template>

<script>
import Dropdown from '@/components/Dropdown'
import AutocompleteDropdown from '@/components/AutocompleteDropdown'

export default {
  components: {
    'dropdown': Dropdown,
    'autocomplete-dropdown': AutocompleteDropdown
  },
  data() {
    return {
      selectedFruit: '',
      fruitOptions: {
        'Apple': 'Apple',
        'Banana': 'Banana',
        'Blueberry': 'Blueberry',
        'Kiwi': 'Kiwi',
        'Pear': 'Pear',
        'Pineapple': 'Pineapple',
        'Watermelon': 'Watermelon'
      }
    }
  }
}
</script>

<style scoped>
.filters {
  width: 800px;
  margin: 0 auto;
}

.filter {
  text-align: left;
}

.result {
  margin: 30px 0;
  text-align: left;
}

label {
  display: block;
}
</style>
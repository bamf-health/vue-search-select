# vue-search-select

A Vue.js search select component.

+ Dependency only vue 2.x & lodash
+ Design css use from <https://github.com/Semantic-Org>

## Version 2.x

### New

+ Support Vue.js 2.x
+ Five Select Component
  + BasicSelect
    + simple search select
  + ListSelect
    + Can pass to Component custom list and customize display text
    + Wrap BasicSelect component
  + MultiSelect
    + search select for multiple select
  + MultiListSelect
    + ListSelect for MultiSelect
  + ModelSelect
    + similar BasicSelect
    + value set through v-model
    + value can be string or object
      + If you pass string, onInput set by string
  + ModelListSelect
    + ListSelect for ModelSelect

### Updated 2.3.8-alpha.0 - 2017/05/02

+ FEATURE : ModelSelect Component

### Updated 2.3.7 - 2017/04/27

+ FEATURE : Add key listener #17
+ FIX : prevent close options when clicks on scrollbar #25

### Updated 2.3.6

+ Add "placeholder" prop

### Updated 2.3.4

+ MultiSelect's search is case insensitive (BasicSelect also)
+ MultiSelect and MultiListSelect emit last selected item.(pr#19)

### Updated 2.3.0

+ Now vue-search-select use events beyond props

# Demo

<http://moreta.github.io/vue-search-select/>

# Usage

## Install

```bash
npm install --save vue-search-select
```

or by yarn

```bash
yarn add vue-search-select
```

## BasicSelect Component Example

See More Samples : src/components/sample

```html
<template>
  <basic-select :options="options"
                :selected-option="item"
                placeholder="select item"
                @select="onSelect">
  </basic-select>
</template>

<script>
  import { BasicSelect } from 'vue-search-select'

  export default {
    data () {
      return {
        options: [
          { value: '1', text: 'aa' + ' - ' + '1' },
          { value: '2', text: 'ab' + ' - ' + '2' },
          { value: '3', text: 'bc' + ' - ' + '3' },
          { value: '4', text: 'cd' + ' - ' + '4' },
          { value: '5', text: 'de' + ' - ' + '5' },
          { value: '6', text: 'ef' + ' - ' + '6' },
          { value: '10', text: 'ef' + ' - ' + '10' },
          { value: '11', text: 'ef' + ' - ' + '11' },
          { value: '12', text: 'ef' + ' - ' + '12' },
          { value: '13', text: 'down case' + ' - ' + 'testcase' },
          { value: '14', text: 'camel case' + ' - ' + 'testCase' },
          { value: '15', text: 'Capitalize case' + ' - ' + 'Testcase' }
        ],
        searchText: '', // If value is falsy, reset searchText & searchItem
        item: {
          value: '',
          text: ''
        }
      }
    },
    methods: {
      onSelect (item) {
        this.item = item
      },
      reset () {
        this.item = {}
      },
      selectOption () {
        // select option from parent component
        this.item = this.options[0]
      }
    },
    components: {
      BasicSelect
    }
  }
</script>
```

## MultiSelect Component Example

```html
<template>
        <multi-select :options="options"
                       :selected-options="items"
                       placeholder="select item"
                       @select="onSelect">
        </multi-select>
</template>

<script>
  import _ from 'lodash'
  import { MultiSelect } from 'vue-search-select'

  export default {
    data () {
      return {
        options: [
          { value: '1', text: 'aa' + ' - ' + '1' },
          { value: '2', text: 'ab' + ' - ' + '2' },
          { value: '3', text: 'bc' + ' - ' + '3' },
          { value: '4', text: 'cd' + ' - ' + '4' },
          { value: '5', text: 'de' + ' - ' + '5' },
          { value: '6', text: 'ef' + ' - ' + '6' },
          { value: '7', text: 'ef' + ' - ' + '7' },
          { value: '8', text: 'ef' + ' - ' + '8' },
          { value: '9', text: 'ef' + ' - ' + '9' },
          { value: '10', text: 'ef' + ' - ' + '10' },
          { value: '11', text: 'ef' + ' - ' + '11' },
          { value: '12', text: 'ef' + ' - ' + '12' },
          { value: '13', text: 'down case' + ' - ' + 'testcase' },
          { value: '14', text: 'camel case' + ' - ' + 'testCase' },
          { value: '15', text: 'Capitalize case' + ' - ' + 'Testcase' }
        ],
        searchText: '', // If value is falsy, reset searchText & searchItem
        items: [],
        lastSelectItem: {}
      }
    },
    methods: {
      onSelect (items, lastSelectItem) {
        this.items = items
        this.lastSelectItem = lastSelectItem
      },
      // deselect option
      reset () {
        this.items = [] // reset
      },
      // select option from parent component
      selectOption () {
        this.items = _.unionWith(this.items, [this.options[0]], _.isEqual)
      }
    },
    components: {
      MultiSelect
    }
  }
</script>
```

# Props


| Compoent        | Name            | Type     | Defailt                 | Description                |
| --------------- | --------------- | -------- | ----------------------- | -------------------------- |
| BasicSelect     | options         | Array    |                         | option list                |
|                 | selectedOption  | Object   | { value: '', text: '' } | default option             |
|                 | isError         | Boolean  | false                   | error style                |
|                 | placeholder     | String   | ''                      |                            |
| ListSelect      | list            | Array    |                         | option list                |
|                 | optionValue     | String   |                         | value key                  |
|                 | optionText      | String   |                         | text key                   |
|                 | customText      | Function |                         | custome text function      |
|                 | selectedItem    | Object   |                         | default option(raw object) |
|                 | isError         | Boolean  | false                   | error style                |
|                 | placeholder     | String   | ''                      |                            |
| MultiSelect     | options         | Array    |                         | option list                |
|                 | selectedOptions | Array    |                         | default option list        |
|                 | isError         | Boolean  | false                   | error style                |
|                 | placeholder     | String   | ''                      |                            |
| MultiListSelect | list            | Array    |                         | option list                |
|                 | optionValue     | String   |                         | value key                  |
|                 | optionText      | String   |                         | text key                   |
|                 | customText      | Function |                         | custome text function      |
|                 | selectedItems   | Array    |                         | default option(raw object) |
|                 | isError         | String   | false                   | error style                |
|                 | placeholder     | String   | ''                      |                            |
| ModelSelect     | options         | Array    |                         | option list                |
|                 | isError         | Boolean  | false                   | error style                |
|                 | placeholder     | String   | ''                      |                            |
| ModelListSelect | list            | Array    |                         | option list                |
|                 | optionValue     | String   |                         | value key                  |
|                 | optionText      | String   |                         | text key                   |
|                 | customText      | Function |                         | custome text function      |
|                 | isError         | Boolean  | false                   | error style                |
|                 | placeholder     | String   | ''                      |                            |


# Run examples

```bash
# install dependencies
yarn install

# serve with hot reload at localhost:9090
npm run dev
```


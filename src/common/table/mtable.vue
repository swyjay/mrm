<template>
<table class="mtable">
  <thead>
    <tr>
      <th v-for="column in columns" @click="sortBy(column.key)" :class="{active: sort.key == column.key}">
        {{column.title}}
        <span class="arrow" :class="sortOrders[column.key] > 0 ? 'asc' : 'dsc'">
        </span>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="entry in data">
      <td v-for="column in columns" :class="column.textAlign">
        {{entry[column.key]}}
      </td>
    </tr>
  </tbody>
</table>
</template>

<script>
export default {
  props: {
    data: Array,
    columns: Array,
    sort:{
      default:function (){
        return {}
      }
    }
  },
  data(){
    let vm = this;
    var sortOrders ={};
    for (var item of this.columns) {
      sortOrders[item.key] = 0;
      if(vm.sort.key == item.key){
        if(vm.sort.order  == "asc"){
          sortOrders[item.key] = 1;
        }else if(vm.sort.order  == "desc"){
          sortOrders[item.key] = -1;
        }
      }
    }
    return {
      sortOrders
    }
  },
  created:function (){
    this.sortBy(this.sort.key)
  },
  methods: {
    sortBy: function (key) {
      let vm = this;
      vm.sortOrders[key] = vm.sortOrders[key]==0 ? 1: vm.sortOrders[key] * -1
      vm.data.sort(function(a,b){
        if(typeof a[key] == "string" && typeof b[key] == "string"){
          if(vm.sortOrders[key] > 0){
            return a[key].localeCompare(b[key]);
          }else{
            return a[key].localeCompare(b[key]) * -1;
          }
        }else{
          if(vm.sortOrders[key] > 0){
            return a[key] < b[key] ? -1 : 1;
          }else{
            return a[key] > b[key] ? -1 : 1;
          }
        }

      })
    }
  }
}
</script>

<style lang='stylus' scoped>
.mtable
  border-radius 3px
  background-color #ffffff
  width 100%
  th
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    -user-select: none;
    border-bottom #dddddd 2px solid
    font-weight bold
    text-align center
  th, td
    min-width: 100px;
    padding: 15px 10px;
  th.active
    color: #333333;
  th.active .arrow
    opacity: 1;
  tbody
    tr:nth-child(odd)
      background:#f9f9f9
    td
      border-top #dddddd 1px solid
    td.left
      text-align left
    td.center
      text-align center
    td.right
      text-align right
  .arrow
    display: inline-block;
    width: 0;
    height: 0;
    margin-left: 5px;
    opacity: 0.66;
  .arrow.asc
    border-left: 6px solid transparent;
    border-right: 6px solid transparent;
    border-bottom: 8px solid #ccc;
  .arrow.dsc
    border-left: 6px solid transparent;
    border-right: 6px solid transparent;
    border-top: 8px solid #ccc;

</style>

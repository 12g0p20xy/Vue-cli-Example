<template>

  <div class="count">

    <ul class="item-list">
      <li v-for="item in items">
        <p>
          {{ item.name + ": " + item.value }}
          <span><i :style="{ width: percent(item) }">{{ percent(item) }}</i></span>
        </p>
        <div class="btn-group">
          <button class="btn btn-default" @click="plus(item)">+</button>
          <button class="btn btn-default" @click="minus(item)">-</button>
        </div>
      </li>
    </ul>
    <h4>总数：{{ total }}</h4>

    <hr>

    <div class="input-group">
      <label for="">Name:</label>
      <input type="text" class="form-control" placeholder="name" v-model="o.name">
    </div>
    <div class="input-group">
      <label for="">Value:</label>
      <input type="text" class="form-control" placeholder="value" v-model.number="o.value">
    </div>
    <button class="btn btn-success" @click="add()"><i class="glyphicon glyphicon-plus"></i> 添加新项目</button>

  </div>

</template>

<script>
export default {
  data () {
    return {
      items: [
        {name: 'Jack', value: 80},
        {name: 'Marry', value: 60},
        {name: 'Sam', value: 100}
      ],
      o: {}
    }
  },
  computed: {
    total () {
      let total = 0
      for (let i = 0; i < this.items.length; i++) {
        total += this.items[i].value
      }
      return total
    }
  },
  methods: {
    percent (item) {
      return Math.round((item.value / this.total) * 100) + '%'
    },
    plus (item) {
      item.value += 10
      return item.value
    },
    minus (item) {
      (item.value >= 10) ? item.value -= 10 : item.value = 0
      return item.value
    },
    add () {
      let newObj = {}
      if (this.o.name && this.o.value) {
        newObj.name = this.o.name
        newObj.value = this.o.value
        this.items.push(newObj)
        this.o.name = ''
        this.o.value = ''
      }
      else{
        alert('请完整填写！')
      }
      
    }
  }
}
</script>

<style lang="less" scoped>
  .item-list {
    padding: 0;
    font-size: 16px;
    li{
      margin-bottom: 1em;
      list-style: none;
      color: darken(yellow, 20%);
      span{
        display: inline-block;
        width: 100%;
        max-width: 480px;
        background: #f2f2f2;
        i{
          display: inline-block;
          background: yellowgreen;
          color: #fff;
          -webkit-transition: width .3s ease-out;
          transition: width .3s ease-out;
        }
      }
    }
  }
  .btn-success{
    margin-top: 1em;
  }
</style>

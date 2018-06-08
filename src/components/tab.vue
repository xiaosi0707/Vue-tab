<template>
  <div class="tab">
    <nav>
      <a href="javascript:;" v-for="(item, key, index) in tabData" :class="{'active': index === selectedIndex}" @click="selectTab(index)">{{ key }}</a>
    </nav>
    <section>
      <div v-for="(item, key, index) in tabData" v-if="index === selectedIndex">
        <dl v-for="(child, key, index) in item">
          <dt>片名：{{ child.name }}</dt>
          <dd>时长：{{ child.time }}</dd>
        </dl>
      </div>
    </section>
  </div>
</template>

<script>
import Axios from 'axios'
export default {
  data() {
    return {
      tabData:{},
      selectedIndex: 0
    }
  },
  created() {
    Axios.get('/static/data.json').then((res) => {
      let { mapList } = res.data;
      this.tabData = mapList;
    })
  },
  methods: {
    selectTab(index) {
      this.selectedIndex = index;
    }
  }
}
</script>

<style scoped>
  .tab nav a {
    display: inline-block;
    width: 49.1%;
    height: 36px;
    line-height: 36px;
    text-align: center;
    background: ghostwhite;
    color: white;
    text-decoration: none;
    color: black;
  }
  .tab nav a.active {
    background: white;
  }
  .tab {
    margin: 0 auto;
    width: 360px;
    border: 1px #ccc solid;
  }

  .tab section {
    margin-top: 24px;
  }

  .tab section dl {
    text-align: left;
    text-indent: 24px;
    margin: 12px;
    padding-bottom: 12px;
    border-bottom: 1px #ccc dotted;
  }

  .tab section dl:last-child {
    border: 0;
  }
</style>

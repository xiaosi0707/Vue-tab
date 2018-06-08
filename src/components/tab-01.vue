<template>
  <div class="tab">
    <nav>
      <a href="javascript:;" :class="{'active': index == selectedIndex}" v-for="(item, key, index) in tabData" @click="selectTab(key, index)">{{ key }}</a>
    </nav>
    <section>
      <dl v-for="(item, index) in filterTabData">
        <dt>片名：{{ item.name }}</dt>
        <dd>时长：{{ item.time }}</dd>
      </dl>
    </section>
  </div>
</template>

<script>
import Axios from 'axios'
    export default {
        data() {
          return {
            tabData: {},
            selectedVal: '',
            selectedIndex: 0
          }
        },
        computed: {
          filterTabData() {
            return this.tabData[this.selectedVal]
          }
        },
        created() {
          Axios.get('/static/data.json').then((res) => {
            let { mapList } = res.data;
            this.tabData = mapList;
            this.selectedVal = Object.keys(mapList)[0]
          })
        },
        methods: {
            selectTab(val, index) {
              this.selectedIndex = index;
              this.selectedVal = val
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

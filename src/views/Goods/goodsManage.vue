<template>
  <div class="tab-container">

    <el-tabs v-model="activeName" style="margin-top:15px;">
      <el-tab-pane v-for="item in tabMapOptions" :key="item.key" :label="item.label" :name="item.key">
        <keep-alive>
          <tab-pane v-if="activeName==item.key" :type="item.key" @create="showCreatedTimes"/>
        </keep-alive>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>
<script>
  import tabPane from './components/TabPane'

  export default {
    name: 'Tab',
    components: { tabPane },
    data() {
      return {
        tabMapOptions: [
          { label: '出售中商品', key: 'SALING' },
          { label: '待上架商品', key: 'READY' },
          { label: '已售罄商品', key: 'OUT' },
          { label: '库存警戒', key: 'ALARM' }
        ],
        activeName: 'SALING',
        createdTimes: 0
      }
    },
    watch: {
      activeName(val) {
        this.$router.push(`${this.$route.path}?tab=${val}`)
      }
    },
    created() {
      // init the default  selected tab
      const tab = this.$route.query.tab
      if (tab) {
        this.activeName = tab
      }
    },
    methods: {
      showCreatedTimes() {
        this.createdTimes = this.createdTimes + 1
      }
    }
  }
</script>

<style scoped>
  .tab-container {
    margin: 30px;
  }
</style>

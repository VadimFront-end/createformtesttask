<template>
  <div
      :style="showList ? border: ''"
      class="select-component"
      @click="showList=!showList"
  >{{itemC}}
    <div class="selectList" v-show="showList">
      <div
          v-for="(item,index) in list"
          :key="index" @click="changeThis(item)"
          class="options"
          :style="{color: itemC.indexOf(item)!==-1 ? '#E35757': ''}"
      >{{item}}
        <div v-show="itemC.indexOf(item)!==-1">X</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "tm-select-component",
  props: {
    list: {
      type: Array,
      default() {
        return []
      }
    },
    multiSelect: {
      type: Boolean,
      default() {
        return false;
      }
    }
  },
  data() {
    return {
      itemC: '',
      showList: false
    }
  },
  methods: {
    changeThis(item) {
      if(this.multiSelect) {
        if(this.itemC.indexOf(item)!==-1) {
          let tmp=this.itemC.split('');
          tmp.splice(this.itemC.indexOf(item), item.length);
          this.itemC=tmp.join('');
        }
        else this.itemC = this.itemC + ' ' + item;
        this.$emit('getItem', this.itemC);
      }
      else {
        if(this.itemC === item) this.itemC = '';
        else this.itemC = item;
        this.$emit('getItem', this.itemC);
      }
    }
  },
  computed: {
    border() {
      return {
        borderRadius: '3px 3px 0px 0px'
      }
    }
  }
}
</script>

<style>

.select-component {
  height: 40px;
  cursor: pointer;
  background: #333361;
  border-radius: 3px;
  position: relative;
  color: #B0B0F4;
  padding: 10px;
}
.selectList {
  border-radius: 0 0 3px 3px;
  position: absolute;
  top: 100%;
  z-index: 2;
  left: 0;
  width: 100%;
  color: #B0B0F4;
  background: #333361;
}
.options {
  display: flex;
  justify-content: space-between;
  border-top: 1px solid #53538D;
  padding: 10px;
}
</style>

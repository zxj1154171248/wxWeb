<template>
  <div id="ChangeName">
    <Header :showBack="true">
      <span slot="title">修改自我介绍</span>
    </Header>
    <section class="content-box">
      <div class="change-box">
        <cube-textarea :placeholder="placeholder" :maxlength="maxlength" :autofocus="autofocus" v-model="value"></cube-textarea>
      </div>
      <cube-button @click="changeSelf">保存</cube-button>
    </section>
  </div>
</template>

<script>
  import Header from '../common/Header.vue'
  import { Button, Input, Textarea } from 'cube-ui'
  export default {
    name: 'selfIntroduction',
    components: {
      Header,
      Button,
      Input,
      Textarea
    },
    data () {
      return {
        value: '',
        placeholder: '请输入',
        maxlength: 150,
        autofocus: true
      }
    },
    /**
     * 生命周期函数--在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用
     */
    beforeCreate: function () {
    },
    /**
     * 生命周期函数--在实例创建完成后被立即调用
     */
    created: function () {
    },
    /**
     * 生命周期函数--在挂载开始之前被调用：相关的 render 函数首次被调用
     */
    beforeMount: function () {
    },
    /**
     * 生命周期函数--el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子
     */
    mounted: function () {
    },
    /**
     * 生命周期函数--数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前
     */
    beforeUpdate: function () {
    },
    /**
     * 生命周期函数--由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子
     */
    updated: function () {
    },
    /**
     * 生命周期函数--keep-alive 组件激活时调用
     */
    activated: function () {
      this.value = this.$store.editSelf.introduction
    },
    /**
     * 组件内方法
     */
    methods: {
      changeSelf: function () {
        let _this = this
        // 非空校验
        if (!this.value) {
          _this.$createToast({
            time: 2000,
            txt: '自我介绍不能为空',
            type: 'warn'
          }).show()
          return
        }
        // 提交数据
        this.$store.dispatch('editSelf', {introduction: this.value}).then(function (res) {
          if (res.code == 0) {
            _this.$createToast({
              time: 2000,
              txt: '修改成功',
              type: 'correct'
            }).show()
            _this.$router.push('/personalMine')
          } else {
            _this.$createToast({
              time: 2000,
              txt: res.msg,
              type: 'error'
            }).show()
          }
        })
      }
    },
    /**
     * 计算属性
     */
    computed: {
    }
  }
</script>

<style scoped>
  #ChangeName {padding-top: 45px;}
  .content-box{padding: 10px;}
  .change-box {margin-bottom: 20px;}
</style>

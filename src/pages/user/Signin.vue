<template>
  <div class="container">
    <mu-card>
      <mu-card-text>
        <mu-text-field label="用户名\手机号" labelFloat v-model="name"/>
        <mu-text-field label="密码" type="password" labelFloat v-model="password"/>
      </mu-card-text>
      <mu-card-actions>
        <mu-raised-button :disabled="!canSave" @click="save" label="登录" class="demo-raised-button" secondary/>
        <mu-flat-button label="注册"/>
      </mu-card-actions>
    </mu-card>
  </div>
</template>

<script>
  import ArticleServ from '@/services/ArticleServ'
  export default {
    name: 'Signin',
    data () {
      return {
        name: '',
        password: ''
      }
    },
    computed: {
      canSave () {
        return this.name && this.password
      }
    },
    async mounted () {
    },
    methods: {
      async save () {
        const params = {
          title: this.title,
          content: this.content,
          tags: this.tags
        }
        const res = await ArticleServ.add(params)
        if (res.result === 'ok') {
          this.$parent.showToast({message: '保存成功'})
          this.$router.back()
        }
      }
    }
  }
</script>

<style scoped>
  .mu-text-field {
    width:100%;
  }

</style>

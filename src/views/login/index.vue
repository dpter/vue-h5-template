<template>
  <div class="login">
    <h2>登录</h2>
    <nut-form ref="ruleForm" :model-value="formData">
      <nut-form-item label="用户名" required prop="name" :rules="[{ required: true, message: '请输入用户名' }]">
        <nut-input v-model="formData.name" placeholder="请输入用户名" type="text" />
      </nut-form-item>
      <nut-form-item label="密码" required prop="pwd" :rules="[{ required: true, message: '请输入密码' }]">
        <nut-input v-model="formData.pwd" placeholder="请输入密码" type="password" />
      </nut-form-item>
      <nut-button block type="info" @click="submit"> 登录 </nut-button>
    </nut-form>
  </div>
</template>

<script lang="ts" setup name="LoginPage">
  import router from '@/router';
  import { reactive, ref } from 'vue';
  import { useUserStore } from '@/store/modules/user';

  const userStore = useUserStore();
  const formData = reactive({
    name: '',
    pwd: '',
  });
  const ruleForm = ref<any>(null);
  const submit = () => {
    ruleForm.value.validate().then(async ({ valid, errors }: any) => {
      if (valid) {
        const userInfo = await userStore.login();
        console.log(userInfo);
        if (userInfo) {
          router.push({ path: '/home' });
        }
      } else {
        console.log('error submit!!', errors);
      }
    });
  };
</script>

<style scoped lang="scss">
  .login {
    padding: 20px;

    h2 {
      letter-spacing: 10px;
      text-align: center;
    }

    .nut-form-item {
      margin-bottom: 20px;
      border-radius: 20px;
      background: #f2f3f5;

      input {
        background: transparent;
      }
    }
  }
</style>

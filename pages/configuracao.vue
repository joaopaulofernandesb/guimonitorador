<template>
  <a-layout id="components-layout-demo-fixed-sider">
    <a-layout-sider
      :trigger="null"
      collapsible
      v-model="collapsed"
      :style="{ overflow: 'auto', height: '100vh', position: 'fixed', left: 0 }"
    >
      <div class="logo"></div>
      <a-menu theme="dark" mode="inline">
        <a-menu-item>
          <router-link to="/" style="color:#fff;">
            <a-icon type="home" />Home
          </router-link>
        </a-menu-item>
        <a-menu-item>
          <router-link to="/configuracao" style="color:#fff;">
            <a-icon type="setting" />Ajuste
          </router-link>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout :style="{ marginLeft: '200px' }">
      <a-layout-header :style="{ background: '#fff', padding: 0 }">
        <div style="margin-right:19px; float: right">
          <a-button type="primary" shape="circle" icon="plus" ghost @click="showDrawer" />
        </div>
      </a-layout-header>

      <a-layout-content :style="{ margin: '24px 16px 0', overflow: 'initial' }">
        <div :style="{ padding: '24px', background: '#fff', textAlign: 'center' }">
          <div style="padding: 20px;"></div>
        </div>

        <a-drawer
          title="Criar Novo Monitor"
          :width="720"
          @close="onClose"
          :visible="visible"
          :wrapStyle="{height: 'calc(100% - 108px)',overflow: 'auto',paddingBottom: '108px'}"
        >
          <a-form :form="form" layout="vertical" hideRequiredMark>
            <a-row :gutter="16">
              <a-col :span="12">
                <a-form-item label="Name">
                  <a-input
                    v-decorator="['name', {
                  rules: [{ required: true, message: 'Please enter user name' }]
                }]"
                    placeholder="Nome do site que vai monitorar"
                  />
                </a-form-item>
              </a-col>
              <a-col :span="12">
                <a-form-item label="Url">
                  <a-input
                    v-decorator="['url', {
                  rules: [{ required: true, message: 'please enter url' }]
                }]"
                    style="width: 100%"
                    addonBefore="http://"
                    addonAfter=".com.br"
                    placeholder="Informe a URL"
                  />
                </a-form-item>
              </a-col>
            </a-row>
          </a-form>
          <div
            :style="{
          position: 'absolute',
          left: 0,
          bottom: 0,
          width: '100%',
          borderTop: '1px solid #e9e9e9',
          padding: '10px 16px',
          background: '#fff',
          textAlign: 'right',
        }"
          >
            <a-button :style="{marginRight: '8px'}" @click="onClose">Cancel</a-button>
            <a-button @click="onClose" type="primary">Submit</a-button>
          </div>
        </a-drawer>
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>
<script>
export default {
  data() {
    return {
      collapsed: false,
      dadoss: 8,
      status: false,
      form: this.$form.createForm(this),
      visible: false
    }
  },

  methods: {
    showConfirm() {
      this.status = true
      this.$confirm({
        title: 'Atenção !',
        content: 'Deseja Ativar o Monitoramento ?',
        onOk() {
          return new Promise((resolve, reject) => {
            setTimeout(Math.random() > 0.5 ? resolve : reject, 1000)
          }).catch(() => console.log('Oops errors!'))
        },
        onCancel() {}
      })
    },
    showDrawer() {
      this.visible = true
    },
    onClose() {
      this.visible = false
    }
  }
}
</script>
<style>
#components-layout-demo-fixed-sider .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px;
}
</style>
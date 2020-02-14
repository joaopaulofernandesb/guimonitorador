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
          <div style="padding: 30px">
            <a-row :gutter="16">
              <a-col :span="6">
                <a-card hoverable style="margin:24px 16px 0; overflow:initial; border-radius:12px;">
                  <a-statistic
                    title="Feedback"
                    :value="11.28"
                    :precision="2"
                    suffix="%"
                    :valueStyle="{color: '#3f8600'}"
                    style="margin-right: 50px"
                  >
                    <template v-slot:prefix>
                      <a-icon type="arrow-up" />
                    </template>
                  </a-statistic>
                </a-card>
              </a-col>
              <a-col :span="6">
                <a-card hoverable style="margin:24px 16px 0; overflow:initial; border-radius:12px;">
                  <a-statistic
                    title="Idle"
                    :value="9.3"
                    :precision="2"
                    suffix="%"
                    valueClass="demo-class"
                    :valueStyle="{ color: '#cf1322' }"
                  >
                    <template v-slot:prefix>
                      <a-icon type="arrow-down" />
                    </template>
                  </a-statistic>
                </a-card>
              </a-col>
              <a-col :span="6">
                <a-card hoverable style="margin:24px 16px 0; overflow:initial; border-radius:12px;">
                  <a-statistic
                    title="Idle"
                    :value="9.3"
                    :precision="2"
                    suffix="%"
                    valueClass="demo-class"
                    :valueStyle="{ color: '#cf1322' }"
                  >
                    <template v-slot:prefix>
                      <a-icon type="arrow-down" />
                    </template>
                  </a-statistic>
                </a-card>
              </a-col>
              <a-col :span="6">
                <a-card hoverable style="margin:24px 16px 0; overflow:initial; border-radius:12px;">
                  <a-statistic
                    title="Idle"
                    :value="9.3"
                    :precision="2"
                    suffix="%"
                    valueClass="demo-class"
                    :valueStyle="{ color: '#cf1322' }"
                  >
                    <template v-slot:prefix>
                      <a-icon type="arrow-down" />
                    </template>
                  </a-statistic>
                </a-card>
              </a-col>
            </a-row>
          </div>
          <div style="padding: 20px;">
            <div v-if="dadoss === 0">
              <img src="../img/vazio.png" alt />
            </div>
            <div v-else>
              <a-row type="flex" justify="center">
                <a-col :span="6" v-for="dados in dadoss" :key="dados.id">
                  <a-card
                    hoverable
                    style="margin:24px 16px 0; overflow:initial; border-radius:12px;"
                  >
                    <!-- <img
                    alt="example"
                    src="https://gw.alipayobjects.com/zos/rmsportal/JiqGstEfoWAOHiTxclqi.png"
                    slot="cover"
                    style="border-radius:12px;"
                    />-->
                    <template class="ant-card-actions" slot="actions">
                      <a-button type="link" @click="showModal">
                        <a-icon type="setting" />
                      </a-button>

                      <a-button type="link" @click="() => openNotificationWithIcon('warning')">
                        <a-icon type="edit" />
                      </a-button>

                      <div v-if="status == true">
                        <a-button type="link" @click="showConfirm">
                          <a-icon type="close" style="color:red" />
                        </a-button>
                      </div>
                      <div v-else>
                        <a-button type="link" @click="showConfirm">
                          <a-icon type="sync" style="color:green" />
                        </a-button>
                      </div>
                    </template>
                    <a-card-meta title="Monitorando a eSocial" />
                    <div v-if="status == true">
                      <a-icon type="sync" spin style="color:green;" />
                    </div>
                    <div v-else>
                      <a-icon type="stop" style="color:red;" />
                    </div>
                  </a-card>
                  <br />
                </a-col>
              </a-row>
            </div>
          </div>
        </div>

        <a-modal v-model="visiblemodal" title="Logs" onOk="handleOk">
          <template slot="footer">
            <a-button type="success" key="back" @click="handleCancel">Sair</a-button>
            <!-- <a-button key="submit" type="primary" :loading="loading" @click="handleOk">Submit</a-button> -->
          </template>
          <div v-if="status == true">
            <a-timeline pending="Monitorando..." :reverse="true">
              <a-timeline-item>Create a services site 2015-09-01</a-timeline-item>
              <a-timeline-item>Solve initial network problems 2015-09-01</a-timeline-item>
              <a-timeline-item>Technical testing 2015-09-01</a-timeline-item>
            </a-timeline>
          </div>
          <div v-else>
            <a-timeline>
              <a-timeline-item color="red">
                <a-icon slot="dot" type="close-circle" style="font-size: 16px;" />Monitorametno parado
              </a-timeline-item>
            </a-timeline>
          </div>
        </a-modal>

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
                <a-form-item label="URL">
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
      dadoss: 0,
      status: false,
      form: this.$form.createForm(this),
      visible: false,
      loading: false,
      visiblemodal: false,
      loadingmodal: false
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
        onCancel() {
          this.status = false
        }
      })
    },
    showDrawer() {
      this.visible = true
    },
    onClose() {
      this.visible = false
    },

    showModal() {
      this.visiblemodal = true
    },
    handleOk(e) {
      this.loadingmodal = true
      setTimeout(() => {
        this.visiblemodal = false
        this.loadingmodal = false
      }, 3000)
    },
    handleCancel(e) {
      this.visiblemodal = false
    },
    openNotificationWithIcon(type) {
      this.$notification[type]({
        message: 'Desculpe !',
        description: 'Esta opção não está disponivel no momento'
      })
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
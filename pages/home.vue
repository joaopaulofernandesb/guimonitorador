<template>
  <a-layout id="components-layout-demo-custom-trigger">
    <a-layout-sider
      :trigger="null"
      collapsible
      v-model="collapsed"
      :style="{ left: 0, position: 'relative'  }"
    >
      <div class="logo" />
      <a-menu theme="dark" mode="inline">
        <a-menu-item>
          <router-link to="/" style="color:#fff;">
            <a-icon type="home" />Home
          </router-link>
        </a-menu-item>
        <a-menu-item key="2" to="/home">
          <a-icon type="setting" />
          <span class="nav-text">nav 2</span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout>
      <a-layout-header style="background: #fff; padding: 0">
        <a-icon
          class="trigger"
          :type="collapsed ? 'menu-unfold' : 'menu-fold'"
          @click="()=> collapsed = !collapsed"
        />
      </a-layout-header>
      <a-layout-content
        :style="{ margin: '24px 16px', padding: '24px', background: '#fff', minHeight: '280px' }"
      >
        <div :style="{ padding: '24px', background: '#fff', textAlign: 'center' }">
          <div style="padding: 20px;">
            <a-row :gutter="130">
              <a-col :span="6" v-for="dados in dadoss" :key="dados.id">
                <a-card hoverable style="width: 300px">
                  <img
                    alt="example"
                    src="https://gw.alipayobjects.com/zos/rmsportal/JiqGstEfoWAOHiTxclqi.png"
                    slot="cover"
                  />
                  <template class="ant-card-actions" slot="actions">
                    <a-icon type="setting" to="/home" />
                    <a-icon type="edit" />
                    <a-icon type="ellipsis" />
                  </template>
                  <a-card-meta title="Card title" description="This is the description">
                    <a-avatar
                      slot="avatar"
                      src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png"
                    />
                  </a-card-meta>
                </a-card>
                <br />
              </a-col>
            </a-row>
          </div>
        </div>
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>
<script>
export default {
  data() {
    return {
      collapsed: false,
      dadoss: 10
    }
  }
}
</script>
<style>
#components-layout-demo-custom-trigger .trigger {
  font-size: 18px;
  line-height: 64px;
  padding: 0 24px;
  cursor: pointer;
  transition: color 0.3s;
}

#components-layout-demo-custom-trigger .trigger:hover {
  color: #1890ff;
}

#components-layout-demo-custom-trigger .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px;
}
</style>
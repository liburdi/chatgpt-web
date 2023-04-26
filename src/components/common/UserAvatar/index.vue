<script setup lang='ts'>
import { computed, ref } from 'vue'
import { NAvatar, useMessage } from 'naive-ui'
import type { UserInfo } from '@/store/modules/user/helper'
import { useUserStore } from '@/store'
import defaultAvatar from '@/assets/avatar.jpg'
import { isString } from '@/utils/is'
import { t } from '@/locales'

const userStore = useUserStore()
const ms = useMessage()
const open = ref<boolean>(false)
const token = ref<string>('')

const userInfo = computed(() => userStore.userInfo)

// const count = ref(userInfo.value.count ?? 0)

const description = ref(userInfo.value.description ?? '')

function setToken() {
  open.value = true
}

function handleSetToken() {
  if (token.value === 'usA3lAH') {
    ms.success(t('设置成功'))
    window.location.reload()
  }
  else {
    ms.error(t('无效token'))
  }
  open.value = false
}

function updateUserInfo(options: Partial<UserInfo>) {
  userStore.updateUserInfo(options)
  ms.success(t('common.success'))
}
</script>

<template>
  <div class="flex items-center overflow-hidden">
    <div class="w-10 h-10 overflow-hidden rounded-full shrink-0">
      <template v-if="isString(userInfo.avatar) && userInfo.avatar.length > 0">
        <NAvatar
          size="large"
          round
          :src="userInfo.avatar"
          :fallback-src="defaultAvatar"
        />
      </template>
      <template v-else>
        <NAvatar size="large" round :src="defaultAvatar" />
      </template>
    </div>
    <div class="flex-1 min-w-0 ml-2">
      <h2 class="overflow-hidden font-bold text-md text-ellipsis whitespace-nowrap">
        {{ userInfo.name ?? '游客' }}
      </h2>
      <p class="overflow-hidden text-xs text-gray-500 text-ellipsis whitespace-nowrap">
        <button @click="setToken">
          {{ userInfo.description ?? '设置' }}
        </button>
      </p>
    </div>
  </div>
  <Teleport to="body">
    <div v-if="open" class="dialog">
      <div style="position:flex;">
        <el-input
          v-model:value="description"
          class="w-50 m-2"
          size="small"
          placeholder="设置token开始智能之旅～"
        />

        <el-button type="success" size="small" @click="updateUserInfo({ description })">
          设
        </el-button>
        <el-button type="warning" size="small" @click="handleSetToken">
          免费试用20次
        </el-button>
        <el-button type="danger" size="small" @click="handleSetToken">
          9.9元购买
        </el-button>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
#tokenButton{

}
.flex{
  position:flex;
}
.dialog {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  max-width: 80%;
  padding: 20px;
  border-radius: 5px;
  background-color: #18a058;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
}
</style>

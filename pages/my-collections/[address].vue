<script setup lang="ts">
import _ from 'lodash'
defineProps<IView>()
interface IView {
  tokenData: any
}
const tokenData = {
  name: 'Soulship Org',
  address: '0x9d95e67f1B30610f58Fd6D4588A11f851F2818d9',
  utility: 'Gaming',
  total_minted: 50,
  total_burned: 8,
  balance: 2,
  logo_url: 'https://avatars.githubusercontent.com/u/38809367?s=280&v=4s',
}
const tabs = ['Overview', 'Mint']
const showModal = $ref<boolean>(false)
const activeTab = ref('Overview')
const params = {
  receiver: '',
  baseUri: '',
}
</script>

<template>
  <NuxtLayout name="dashboard">
    <div class="font-poppins text-center w-full h-full px-8">
      <Suspense>
        <div class="py-8 px-8">
          <div class="collection-title">
            <div class="text-gray-400 font-semibold">
              Manage My SBT Collection
            </div>
          </div>
          <div class="flex justify-start items-center py-8">
            <div class="w-[20%] flex justify-start items-center">
              <div class="flex justify-start items-center w-36 h-36 rounded-lg bg-secondary overflow-hidden">
                <img :src="tokenData.logo_url" alt="logo">
              </div>
            </div>
            <div class="w-[75%] text-left">
              <div class="w-full flex justify-between items-center py-3 gap-4 text-sm text-gray-400">
                <div class="w-[30%] font-bold">
                  Collection Name
                </div>
                <div class="w-[5%]">
                  :
                </div>
                <div class="w-[65%] font-light">
                  {{ tokenData.name }}
                </div>
              </div>
              <div class="w-full flex justify-between items-center py-3 gap-4 text-sm font-bold text-gray-400">
                <div class="w-[30%] font-bold">
                  Utility
                </div>
                <div class="w-[5%]">
                  :
                </div>
                <div class="w-[65%] font-light">
                  {{ tokenData.utility }}
                </div>
              </div>
              <div class="w-full flex justify-between items-center py-3 gap-4 text-sm font-bold text-gray-400">
                <div class="w-[30%] font-bold">
                  Address
                </div>
                <div class="w-[5%]">
                  :
                </div>
                <div class="w-[65%] font-light">
                  {{ tokenData.address }}
                </div>
              </div>
            </div>
          </div>
          <div class="mt-16">
            <div class="tabs text-sm">
              <a
                v-for="(tab, idx) in tabs" :key="idx" class="tab w-36 text-gray-400 tab-lifted px-4 h-10"
                :class="(activeTab === tab) ? 'tab-active tab-active-color' : ''"
                @click="activeTab = tab"
              >
                {{ tab }}
              </a>
            </div>
            <div v-if="activeTab === tabs[0]" class="mt-12 w-full flex justify-around items-enter">
              <BasicCard>
                <template #title>
                  Your Balance
                </template>
                <template #value>
                  {{ tokenData.balance }}
                </template>
              </BasicCard>
              <BasicCard>
                <template #title>
                  Total Minted
                </template>
                <template #value>
                  {{ tokenData.total_minted }}
                </template>
              </BasicCard>
              <BasicCard>
                <template #title>
                  Total Burned
                </template>
                <template #value>
                  {{ tokenData.total_burned }}
                </template>
              </BasicCard>
            </div>
            <div v-if="activeTab === tabs[1]">
              <div class="flex justify-start items-center text-left py-6 px-24 gap-12">
                <div class="text-sm w-64 font-bold text-gray-400">
                  Receiver
                </div>
                <FormTextInput v-model="params.receiver" placeholder="Enter Receiver" />
              </div>
              <div class="flex justify-start items-center text-left py-6 px-24 gap-12">
                <div class="text-sm w-64 font-bold text-gray-400">
                  Base URI
                </div>
                <FormTextInput v-model="params.baseUri" class="w-[150px]" placeholder="Enter URI" />
              </div>
            </div>
          </div>
        </div>
      </Suspense>
    </div>
    <Modal v-if="showModal" type="SUCCESS" @click:close="showModal = $event" />
  </NuxtLayout>
</template>

<style lang="postcss" scoped>
 .collection-title {
  @apply flex justify-between items-center mb-4;
 }
 .tab-active-color {
  @apply bg-primary text-white;
 }
</style>
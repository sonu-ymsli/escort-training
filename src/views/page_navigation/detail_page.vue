<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

onMounted(() => {
  console.log('Mounted : Detail page');
});

onUnmounted(() => {
  console.log('UnMounted: Detail page');
});

defineOptions({
  name: 'detail_page',
});

const form = ref();

const formData = reactive({
});
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueText id="viy2Text_9b5RvG" ref="viy2Text_9b5RvG" :style="{ width: '100%', display: 'inline-block' }">
      Hello
    </VueText>
  </VueForm>
</template>

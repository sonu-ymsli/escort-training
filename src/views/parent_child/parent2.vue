<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

import childSubPage2Page from '/src/views/parent_child/child2.vue';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

const selectedNameValue = ref('defaultName');

defineOptions({
  name: 'parent2',
});

const form = ref();
const fullName = ref();
const childSubPage2 = ref();

const formData = reactive({
  fullName: '',
});

function handlePustEvent() {
  formData.fullName = '';
}

function capturSelectedName(event) {
  console.log('value', event);
  selectedNameValue.value = event;
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Full name"

      prop="fullName"
    >
      <VueInput

        id="fullName"

        ref="fullName"

        v-model="formData.fullName"
        data-type="string"

        placeholder="Full name..."
      />
    </VueFormItem>

    <VueText id="selectedName" ref="selectedName" :style="{ width: '100%', display: 'inline-block' }">
      Selected name
    </VueText>
    <VueText id="sname" ref="sname" :style="{ width: '100%', display: 'inline-block' }" v-html="selectedNameValue" />
    <childSubPage2Page

      id="childSubPage2"
      ref="childSubPage2"
      :full-name="formData.fullName"

      @push-event="handlePustEvent"
      @emit-selected-name="capturSelectedName"
    />
  </VueForm>
</template>

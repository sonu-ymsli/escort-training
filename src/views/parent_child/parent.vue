<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

import childSubpagePage from '/src/views/parent_child/child.vue';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'parent',
});

const form = ref();
const parentInput = ref();
const childSubpage = ref();

const formData = reactive({
  parentInput: '',
});

function handleEventFromChild(event) {
  console.log(event);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Parent input"

      prop="parentInput"
    >
      <VueInput

        id="parentInput"

        ref="parentInput"
        v-model="formData.parentInput"

        data-type="string"
      />
    </VueFormItem>

    <childSubpagePage

      id="childSubpage" ref="childSubpage"
      const
      val2="hello"
      p1="val1"
      :p2="formData.parentInput"

      p3="val3"
      @data-to-parent="handleEventFromChild"
    />
  </VueForm>
</template>

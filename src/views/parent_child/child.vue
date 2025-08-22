<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const { p1, p2, p3 } = defineProps(['p1', 'p2', 'p3']);
const emits = defineEmits(['dataToParent']);
const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

console.log(p1, p2, p3);
defineOptions({
  name: 'child',
});

const form = ref();
const childInput = ref();
const childButton = ref();
const sendToParentBtn = ref();

const formData = reactive({
  childInput: '',
});

const childButtonClick = () => {
  console.log(p2);
};
const sendToParentBtnClick = () => {
  handleSendDataToParent();
};

function handleSendDataToParent() {
  emits('dataToParent', formData.childInput);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Child Input"

      prop="childInput"
    >
      <VueInput

        id="childInput"

        ref="childInput"
        v-model="formData.childInput"

        data-type="string"
      />
    </VueFormItem>

    <VueButton id="childButton" ref="childButton" icon-position="left" @click="childButtonClick">
      Child Button
    </VueButton>
    <VueButton id="sendToParentBtn" ref="sendToParentBtn" icon-position="left" @click="sendToParentBtnClick">
      Send data to parent
    </VueButton>
  </VueForm>
</template>

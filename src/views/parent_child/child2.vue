<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const props = defineProps(['fullName']);
const emit = defineEmits(['pushEvent', 'emitSelectedName']);
const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

console.log('props', props);
const nameListData = ref([]);

defineOptions({
  name: 'child2',
});

const form = ref();
const addBtn = ref();
const nameList = ref();

const formData = reactive({
  nameList: '',
});

const nameListProps = computed(() => {
    	return {
    label: 'fullName',
    value: 'fullName',

  };
});

const addBtnClick = () => {
  handleAdd();
};
const nameListChange = (val, option, oldVal, oldOption) => {
  console.log('selected name', val);
  emit('emitSelectedName', val);
}

;

function handleAdd() {
  console.log('handle add', props.fullName);
  nameListData.value.push({ fullName: props.fullName });
  console.log('Name List', nameListData);
  emit('pushEvent');
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueButton id="addBtn" ref="addBtn" icon-position="left" @click="addBtnClick">
      Add
    </VueButton>

    <VueFormItem

      label="Name List"

      prop="nameList"
    >
      <VueSelect

        id="nameList"
        ref="nameList"

        v-model="formData.nameList"

        :options="nameListData"

        :props="nameListProps"

        @change="nameListChange"
      />
    </VueFormItem>
  </VueForm>
</template>

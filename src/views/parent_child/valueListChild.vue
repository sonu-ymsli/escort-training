<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { useApi } from '@/composables/useApi';

const emit = defineEmits(['select']);
const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'valueListChild',
});

const form = ref();
const fullNameTable = ref();
const setBtn = ref();

const formData = reactive({
});

const fullNameTableEditConfig = reactive({
  trigger: 'click',

});

const fullNameTableMouseConfig = reactive({

  extension: true,

});

const fullNameTableRowConfig = reactive({
  isCurrent: true,
});

const pageDataSet_PTrg3Api = useApi({
  method: 'post',
  localData: [
    {
      firstName: 'Sonu',
      lastName: 'Singh',

    },
    {
      firstName: 'Aman',
      lastName: 'Dashore',

    },
    {
      firstName: 'Himanshu',
      lastName: 'Verma',

    },
  ],

});
const pageDataSet_PTrg3 = pageDataSet_PTrg3Api.data;
const fullNameDataApi = useApi({
  method: 'post',
  localData: [

    {
      firstName: 'Sonu',
      lastName: 'Singh',
    },
    {
      firstName: 'Aman',
      lastName: 'Singh',
    },
    {
      firstName: 'Himanshu',
      lastName: 'Singh',
    },
  ],

});
const fullNameData = fullNameDataApi.data;

const fullNameTableFirstNameEditRender = computed(() => {
  return {
    enabled: false,
  };
});

const fullNameTableLastNameEditRender = computed(() => {
  return {
    enabled: false,
  };
});

const setBtnClick = () => {
  setSelectedData();
};

function setSelectedData() {
  emit('select', fullNameTable.value.getCurrentRecord());
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueText id="viy2Text_PwOzL" ref="viy2Text_PwOzL" :style="{ width: '100%', display: 'inline-block' }">
      hello
    </VueText>

    <VueTable

      id="fullNameTable"
      ref="fullNameTable"

      :data="fullNameData"

      :edit-config="fullNameTableEditConfig"
      :mouse-config="fullNameTableMouseConfig"
      :row-config="fullNameTableRowConfig"
    >
      <VueInputColumn

        :edit-render="fullNameTableFirstNameEditRender"

        field="firstName"

        width="200px"

        title="First Name"
      />
      <VueInputColumn

        :edit-render="fullNameTableLastNameEditRender"

        field="lastName"

        width="200px"

        title="Last Name"
      />
    </VueTable>

    <VueButton id="setBtn" ref="setBtn" icon-position="left" @click="setBtnClick">
      Set
    </VueButton>
  </VueForm>
</template>

<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { useApi } from '@/composables/useApi';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'table_component',
});

const form = ref();
const empTable = ref();
const viy2Button_QrVbB = ref();
const viy2Button_QrU5S = ref();
const viy2Button_QrUK5 = ref();

const formData = reactive({
});

const empTableEditConfig = reactive({
  trigger: 'click',

});

const empTableMouseConfig = reactive({

  extension: true,

});

const empTableRowConfig = reactive({
  isCurrent: true,
});

const empDataApi = useApi({
  method: 'post',
  localData: [
    {
      empId: 101,
      firstName: 'Sonu',
      lastName: 'Singh',
      gender: 'Male',
      dob: '10-01-2002',
      age: 25,

    },
    {
      empId: 102,
      firstName: 'Aman',
      lastName: 'Singh',
      gender: 'Male',
      dob: '10-01-2002',
      age: 25,

    },
  ],

});
const empData = empDataApi.data;

const empTableEmpCodeEditRender = computed(() => {
  return {
    enabled: false,
  };
});

const empTableFirstNameEditRender = computed(() => {
  return {
    enabled: true,
    attrs: {

      textAlign: 'center',

    },
  };
});

const empTableLastNameEditRender = computed(() => {
  return {
    enabled: true,
  };
});

const empTableGenderEditRender = computed(() => {
  return {
    enabled: true,
    defaultValue: 'Male',
    attrs: {

      activeValue: 'Male',
      inactiveValue: 'Female',

    },
  };
});

const empTableDobEditRender = computed(() => {
  return {
    enabled: true,
  };
});

const empTableAgeEditRender = computed(() => {
  return {
    enabled: true,
  };
});

const viy2Button_QrVbBClick = () => {
  handleAdd();
}

;
const viy2Button_QrU5SClick = () => {
  empTable.value.remove(empTable.value.getCurrentRecord());
};
const viy2Button_QrUK5Click = () => {
  console.log(empTable.value.getTableData());
};

function handleAdd() {
  empTable.value.insertAt({}, -1);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueTable

      id="empTable"

      ref="empTable"
      :show-footer="true"

      :data="empData"

      :edit-config="empTableEditConfig"
      :mouse-config="empTableMouseConfig"
      :row-config="empTableRowConfig"
    >
      <VueIndexColumn

        align="center"

        width="50px"

        min-width="50px"

        header-align="center"

        title="S.No."
      />

      <VueInputColumn

        :edit-render="empTableEmpCodeEditRender"

        field="empCode"

        width="200px"

        title="Employee Code"
      />
      <VueInputColumn

        :edit-render="empTableFirstNameEditRender"

        field="firstName"

        align="center"

        :title="t('label.firstName')"

        min-width="150px"

        header-align="center"
      />
      <VueInputColumn

        :edit-render="empTableLastNameEditRender"

        field="lastName"

        width="200px"

        :title="t('label.lastName')"
      />

      <VueSwitchColumn

        :edit-render="empTableGenderEditRender"

        field="gender"

        width="200px"

        :title="t('label.gender')"
      />
      <VueDateTimeColumn

        :edit-render="empTableDobEditRender"

        field="dob"

        width="200px"

        :title="t('label.dob')"
      />
      <VueNumberColumn

        :edit-render="empTableAgeEditRender"

        field="age"

        width="200px"

        :title="t('label.age')"
      />
    </VueTable>

    <VueButton id="viy2Button_QrVbB" ref="viy2Button_QrVbB" icon-position="left" @click="viy2Button_QrVbBClick">
      Add
    </VueButton>
    <VueButton id="viy2Button_QrU5S" ref="viy2Button_QrU5S" icon-position="left" @click="viy2Button_QrU5SClick">
      Delete
    </VueButton>
    <VueButton id="viy2Button_QrUK5" ref="viy2Button_QrUK5" icon-position="left" @click="viy2Button_QrUK5Click">
      Save
    </VueButton>
  </VueForm>
</template>

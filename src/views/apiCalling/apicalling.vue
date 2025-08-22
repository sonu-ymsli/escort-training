<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { useApi } from '@/composables/useApi';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'apicalling',
});

const form = ref();
const apidata = ref();
const fetchdatabtn = ref();

const formData = reactive({
  apidata: [],
});

const apidataProps = computed(() => {
    	return {
    label: 'traineeId',
    value: 'name',

  };
});

const apiDataSetApi = useApi({
  url: 'http://localhost:8085/trainee',
  method: 'get',

}, {
  manual: true,
});
const apiDataSet = apiDataSetApi.data;

const fetchdatabtnClick = () => {
  loadData();
}

;

function loadData() {
  apiDataSetApi.runAsync();
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Api Data"

      prop="apidata"
    >
      <VueSelect

        id="apidata"

        ref="apidata"

        v-model="formData.apidata"
        placeholder="API DATA"

        :multiple="true"

        :options="apiDataSet"

        :props="apidataProps"
      />
    </VueFormItem>

    <VueButton id="fetchdatabtn" ref="fetchdatabtn" icon-position="left" @click="fetchdatabtnClick">
      Fetch data
    </VueButton>
  </VueForm>
</template>

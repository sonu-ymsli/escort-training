<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { useApi } from '@/composables/useApi';

import { CONST_SYSTEM_DATE_FORMAT, CONST_SYSTEM_DATE_VALUE_FORMAT } from '@/constants';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'first_page',
});

const form = ref();
const firstName = ref();
const lastName = ref();
const dob = ref();
const age = ref();
const gender = ref();
const hobbies = ref();
const joiningDate = ref();
const yoe = ref();
const descriptor = ref();
const submittbn = ref();

const formData = reactive({
  fname: '', lname: '', dob: '', age: 0, gender: '', hobbies: [], jDate: '', yoe: '', descriptor: '',
});

const yoeProps = computed(() => {
    	return {
    label: 'name',
    value: 'value',

  };
});

const hobbiesDataApi = useApi({
  method: 'post',
  localData: [
    { value: '1', label: 'Baseball' },
    { value: '2', label: 'Cricket' },
    { value: '3', label: 'Badminton' },
  ],

});
const hobbiesData = hobbiesDataApi.data;
const yoeDropdownApi = useApi({
  method: 'post',
  localData: [
    { name: '<= 1year', value: 1 },
    { name: '>1 year and <5 years', value: 2 },
    { name: '>=5 yeats', value: 3 },

  ],

});
const yoeDropdown = yoeDropdownApi.data;
const genderDataApi = useApi({
  method: 'post',
  localData: [
    { value: 'M', label: 'Male' },
    { value: 'F', label: 'Female' },

  ],

});
const genderData = genderDataApi.data;

const firstNameBlur = (event) => {
  console.log('Input field blurred');
}

;
const firstNameInput = (value) => {
  console.log(value);
}

;
const firstNameChange = (value) => {
  console.log(value);
};

const submittbnClick = () => {
  printFormData();
  console.log('Form Submitted');
}

;

function printFormData() {
  console.log('Form data printed');
  console.log(formData.fname);
  console.log(formData.lname);
  console.log(formData.dob);
  console.log(formData.gender);
  console.log(formData.hobbies);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      :label="t('label.firstName')"

      prop="fname"
    >
      <VueInput

        id="firstName"

        ref="firstName"

        v-model="formData.fname"

        data-type="string"

        placeholder="Enter your name"
        type="text"

        text-align="right"

        @blur="firstNameBlur"

        @input="firstNameInput"

        @change="firstNameChange"
      />
    </VueFormItem>

    <VueFormItem

      :label="t('label.lastName')"

      prop="lname"
    >
      <VueInput

        id="lastName"

        ref="lastName"

        v-model="formData.lname"

        data-type="string"

        :autofocus="false"

        placeholder="Enter last name....."
        type="text"

        text-align="left"
      />
    </VueFormItem>

    <VueFormItem

      label="D.O.B"

      prop="dob"
    >
      <VueDatePicker

        id="dob"

        ref="dob"
        v-model="formData.dob"

        placeholder="Enter DOB"

        :format="CONST_SYSTEM_DATE_FORMAT.ymd"

        :value-format="CONST_SYSTEM_DATE_VALUE_FORMAT.ymd"
      />
    </VueFormItem>

    <VueFormItem

      label="Age"

      prop="age"

      size="default"
    >
      <VueInputNumber

        id="age"

        ref="age"

        v-model="formData.age"

        suffix="Years"

        :min="5"

        :max="60"

        size="default"
        :controls="true"

        controls-position="right"
      >
        <template #suffix>
          Years
        </template>
      </VueInputNumber>
    </VueFormItem>

    <VueFormItem

      :label="t('label.gender')"

      prop="gender"
    >
      <VueRadioGroup

        id="gender"

        ref="gender"
        v-model="formData.gender"

        direction="horizontal"

        split-size="default"
      >
        <VueRadio
          v-for="option in genderData"
          :key="option.value"
          :label="option.value"
          :name="option.name"
          :disabled="option.disabled"
        >
          {{ option.label }}
        </VueRadio>
      </VueRadioGroup>
    </VueFormItem>

    <VueFormItem

      label="Hobbies"

      prop="hobbies"
    >
      <VueCheckboxGroup

        id="hobbies"
        ref="hobbies"

        v-model="formData.hobbies"

        split-size="default"
      >
        <VueCheckbox
          v-for="option in hobbiesData"
          :key="option.value"
          :label="option.value"
          :name="option.name"
          :disabled="option.disabled"
        >
          {{ option.label }}
        </VueCheckbox>
      </VueCheckboxGroup>
    </VueFormItem>

    <VueFormItem

      label="Date of Joining"

      prop="jDate"
    >
      <VueDatePicker

        id="joiningDate"

        ref="joiningDate"

        v-model="formData.jDate"
        placeholder="Date of Joining"

        type="datetime"

        :format="CONST_SYSTEM_DATE_FORMAT.ymd"

        :value-format="CONST_SYSTEM_DATE_VALUE_FORMAT.ymd"
      />
    </VueFormItem>

    <VueFormItem

      label="Y.O.E"

      prop="yoe"
    >
      <VueSelect

        id="yoe"

        ref="yoe"
        v-model="formData.yoe"

        placeholder="Year of Experience"

        :options="yoeDropdown"

        :props="yoeProps"
      />
    </VueFormItem>

    <VueFormItem

      label="Description"

      prop="descriptor"
    >
      <VueInput
        id="descriptor"

        ref="descriptor"

        v-model="formData.descriptor"

        type="textarea"

        resize="none"
        :rows="5"

        :maxlength="10"
      />
    </VueFormItem>

    <VueButton id="submittbn" ref="submittbn" icon-position="left" color="#108DED" :round="true" @click="submittbnClick">
      Submit
    </VueButton>
  </VueForm>
</template>

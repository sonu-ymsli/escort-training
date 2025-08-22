<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

const router = useRouter();

onMounted(() => {
  console.log('header Component Mounted');
});

onUnmounted(() => {
  console.log('Unmounted : Header page');
});

defineOptions({
  name: 'header_page',
});

const form = ref();
const route = ref();
const openNonActiveTag = ref();
const closeCurrentTabBtn = ref();
const closeAndGoToSpecifiedTab = ref();
const refreshBtn = ref();
const openDetailOnSameTagBtn = ref();
const viy2InputBox_USooU = ref();

const formData = reactive({
  datafieldviy2InputBox_USooU: '',
});

const routeClick = () => {
  router.push('detail_page');
};
const openNonActiveTagClick = () => {
  handleOpenNonActiveTagClick();
};
const closeCurrentTabBtnClick = () => {
  closeCurrentTab();
};
const closeAndGoToSpecifiedTabClick = () => {
  closeCurrentTabWithSpecifiedTab();
};
const refreshBtnClick = () => {
  console.log('hello');
  refreshCurrentTab();
};
const openDetailOnSameTagBtnClick = () => {
  openDetailOnSameTag();
};

function handleOpenNonActiveTagClick() {
  useMultiTags().openTag(
    {
      name: 'detail_page',
    },
  );
}

function closeCurrentTab() {
  useMultiTags().closeTag();
}

function closeCurrentTabWithSpecifiedTab() {
  useMultiTags().closeTag(
    'detail_page',
  );
}

function refreshCurrentTab() {
  useMultiTags().refreshCurrent();
}

function openDetailOnSameTag() {
  useMultiTags().updateTag({
    name: 'detail_page',
  });
  router.push('detail_page');
  useMultiTags().removeTagCache({ name: 'header_page' }); // removes the cahces of header_page
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueButton id="route" ref="route" icon-position="left" @click="routeClick">
      Button
    </VueButton>
    <VueButton id="openNonActiveTag" ref="openNonActiveTag" icon-position="left" @click="openNonActiveTagClick">
      Open Non Active Tag
    </VueButton>
    <VueButton id="closeCurrentTabBtn" ref="closeCurrentTabBtn" icon-position="left" @click="closeCurrentTabBtnClick">
      Close current Tab
    </VueButton>
    <VueButton id="closeAndGoToSpecifiedTab" ref="closeAndGoToSpecifiedTab" icon-position="left" @click="closeAndGoToSpecifiedTabClick">
      Close this tab, goto detail page *
    </VueButton>
    <VueButton id="refreshBtn" ref="refreshBtn" icon-position="left" @click="refreshBtnClick">
      Refresh me!
    </VueButton>
    <VueButton id="openDetailOnSameTagBtn" ref="openDetailOnSameTagBtn" icon-position="left" @click="openDetailOnSameTagBtnClick">
      Open Detail on same tag
    </VueButton>

    <VueFormItem

      prop="datafieldviy2InputBox_USooU"
    >
      <VueInput

        id="viy2InputBox_USooU"

        ref="viy2InputBox_USooU"
        v-model="formData.datafieldviy2InputBox_USooU"

        data-type="string"
      />
    </VueFormItem>
  </VueForm>
</template>

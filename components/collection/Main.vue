<template>
    <!--Add Builder-->
  <div>
    <CollectionAdd @addBuilderData="addBuilderData"></CollectionAdd>
  </div>
    <!--Builderdata List-->
  <div>
    <CollectionList
      :builderData="builderData"
      @builderPrefillData="editData"
      :key="editRender"
    ></CollectionList>
  </div>
      <!--Edit Builder-->
  <CollectionEdit
    v-if="show"
    :builderData="builderData.data._rawValue"
    :editBuilderData="builderPrefill"
    @updateBuilder="editBuilderData"
  ></CollectionEdit>
</template>
<script setup lang="ts">
// Get builder using getcall
const builderData = await useAuthLazyFetch(
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  {}
);
const show = ref(false);
const builderPrefill = ref({});

const editRender = ref(0);
const rawValue = ref(builderData.data._rawValue);

// Add builder
const addBuilderData = async (data: Object) => {
  const body = {
    body: JSON.stringify(data),
  };
  // post call for adding builder
  useAuthLazyFetchPost(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/",
    body
  );
  rawValue.value.unshift(data);
};
// Prefilling in edit builder sidebar
const editData = (data: object) => {
  show.value = true;
  builderPrefill.value = data;
  editRender.value++;
};

// Update builder data after editing
const editBuilderData = async (data: Object) => {
  const putOptions = {
    body: JSON.stringify(data),
  };
  await useAuthLazyFetchPut(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/${data.uid}`,
    putOptions
  );
};
</script>

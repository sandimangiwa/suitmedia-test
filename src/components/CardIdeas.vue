<template>
  <div
    class="card h-100 border-0 shadow"
    style="border-radius: 12px; overflow: hidden"
  >
    <div class="bg-light">
      <b-img-lazy
        v-bind="mainProps"
        :src="
          item.medium_image && item.medium_image.length > 0
            ? item.medium_image[0].url
            : '../assets/logo.png'
        "
        :alt="item.title"
      />
    </div>
    <div class="card-body">
      <h6 class="card-subtitle mb-2 text-muted">{{ item.published_at }}</h6>
      <h5 class="card-title font-weight-bolder text-overflow-ellipsis-3">
        {{ item.title }}
      </h5>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      mainProps: {
        center: true,
        fluidGroud: true,
        blank: true,
        blankColor: "#bbb",
        height: "200vh",
        // width: "300vw",
      },
    };
  },
};
</script>
<style>
.text-overflow-ellipsis-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  text-align: left;
}
</style>

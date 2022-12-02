<template>
  <div>
    <section class="banner mb-5" style="padding-top: 4.5em">
      <div>
        <div
          class="container text-center text-white"
          style="padding-top: 7em; padding-bottom: -4em"
        >
          <h1 class="display-6">Ideas</h1>
          <p class="lead">Where all our great things begin</p>
        </div>
        <svg
          style="margin-top: -3.8em"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 1440 320"
        >
          <path
            fill="white"
            fill-opacity="1"
            d="M0,320L1440,160L1440,320L0,320Z"
          ></path>
        </svg>
      </div>
    </section>
    <div class="container">
      <div class="row mb-4">
        <div class="col-sm-12 col-md-4">
          <div>
            <label class="d-inline-flex align-items-center">
              Showing {{ params.current_page }} - {{ params.per_page }} of
              {{ totalRow }}
            </label>
          </div>
        </div>
        <!-- Search -->
        <div class="col-sm-12 col-md-8">
          <div
            class="dataTables_length text-md-right"
            id="tickets-table_length"
          >
            <label class="d-inline-flex align-items-center text-nowrap">
              Show per page:&nbsp;
              <b-form-select
                v-model="params.per_page"
                plain
                class="rounded-pill"
                :options="pageOptions"
              ></b-form-select>
            </label>
            &nbsp;
            <label class="d-inline-flex align-items-center text-nowrap">
              Sort by:&nbsp;
              <b-form-select
                v-model="params.sort"
                plain
                class="rounded-pill"
                :options="sortOptions"
              ></b-form-select>
            </label>
          </div>
        </div>
      </div>
      <div class="row">
        <div
          class="col-12 col-md-3 mb-5"
          v-for="item in listIdeas"
          :key="item.id"
        >
          <card-ideas :item="item" />
        </div>
      </div>
      <div class="overflow-auto">
        <div class="my-5">
          <b-pagination
            align="center"
            v-model="params.current_page"
            :total-rows="totalRow"
            :per-page="params.per_page"
            pills
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CardIdeas from "@/components/CardIdeas.vue";
import axios from "axios";
export default {
  name: "HomeView",
  components: {
    CardIdeas,
  },
  data() {
    return {
      listIdeas: [],
      params: {
        current_page: 1,
        per_page: 10,
        sort: "published_at",
      },
      totalRow: 1,
      pageOptions: [10, 20, 50],
      sortOptions: [
        { value: "published_at", text: "Newest" },
        { value: "-published_at", text: "Oldest" },
      ],
    };
  },
  mounted() {
    this.getIdeas();
  },
  watch: {
    params: {
      handler(val) {
        if (val) {
          this.$router.replace({
            ...this.$router.currentRoute,
            query: val,
          });
          this.getIdeas();
        }
      },
      deep: true,
    },
  },
  methods: {
    getIdeas() {
      const params = {
        "page[number]":
          this.$route.query.current_page || this.params.current_page,
        "page[size]": this.$route.query.per_page || this.params.per_page,
        sort: this.$route.query.sort || this.params.sort,
        append: ["small_image", "medium_image"],
      };

      axios
        .get("https://suitmedia-backend.suitdev.com/api/ideas", {
          params: params,
        })
        .then((response) => {
          this.totalRow = response.data.meta.total;
          this.listIdeas = response.data.data;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally(() => (this.loading = false));
    },
  },
};
</script>
<style>
.banner {
  background-image: url("../assets/bg.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  background-attachment: fixed;
}
.b-pagination-pills .page-item .page-link {
  border-radius: 12px !important;
  line-height: 1.5 !important;
  border-color: white;
}
.page-link {
  color: black;
  font-weight: 600;
}
.page-item.active .page-link {
  background-color: #ff6404;
}
.page-link:hover {
  background-color: #ff640417;
  color: #ff6404;
}
</style>

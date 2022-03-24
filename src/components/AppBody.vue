<template>
  <div class="container body-container">
    <div class="container-lg">
      <div class="row justify-content-md-center">
        <div v-for="content in contents" :key="content.id" class="col">
          <div class="card mb-5" style="width: 15rem">
            <img
              :src="content.imageLink"
              class="card-img-top"
              alt="can't load image"
              onerror="this.onerror=null; this.src='https://sciendo.com/product-not-found.png'"
            />

            <div class="card-body">
              <h5 class="card-title">{{ content.title }}</h5>
              <p class="card-text">
                {{ content.abstract }}
              </p>
              <button
                type="button"
                class="btn btn-primary"
                data-bs-toggle="modal"
                data-bs-target="#exampleModal"
              >
                See Details
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">...</div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { createApp } from "vue";
import App from "../App.vue";
import axios from "axios";
import VueAxios from "vue-axios";
createApp(App).use(VueAxios, axios);

export default {
  name: "AppBody",
  data() {
    return {
      contents: null,
    };
  },
  mounted() {
    let config = {
      headers: {
        "Access-Control-Allow-Origin": "*",
      },
    };
    axios
      .get(`http://localhost:8080/books`, {
        config,
        withCredentials: true,
      })
      .then((res) => {
        this.contents = res.data;
      });
  },
};
</script>

<style>
.body-container {
  padding: 100px 0px;
}

p.card-text {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
}
</style>
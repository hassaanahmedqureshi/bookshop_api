<template>
  <div class="container body-container">
    <!-- List of books in cards -->
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
                data-bs-target=".bd-example-modal-lg"
                v-on:click="getBookData(content.id)"
              >
                See Details
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal for showing a specific BookDetail -->
    <div
      class="modal fade bd-example-modal-lg"
      id="bookdetails"
      tabindex="-1"
      aria-labelledby="bookdetailsLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-lg">
        <div class="modal-content" v-if="bookDetails !== null">
          <div class="modal-header">
            <h5 class="modal-title" id="bookdetailsLabel">
              {{ this.bookDetails.title }}
            </h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <div class="container">
              <div
                class="bookImage mb-5"
                style="width: 100%; height: 400px; overflow: hidden"
              >
                <img
                  style="height: 100%"
                  :src="this.bookDetails.imageLink"
                  alt="can't load image"
                  onerror="this.onerror=null; this.src='https://sciendo.com/product-not-found.png'"
                />
              </div>

              <div class="row">
                <div class="col-sm-2">
                  <p class="text-start fw-bold">Author:</p>
                </div>
                <div class="col-sm-10">
                  <p class="text-start">{{ this.bookDetails.author }}</p>
                </div>
              </div>

              <div class="row">
                <div class="col-sm-2">
                  <p class="text-start fw-bold">Country:</p>
                </div>
                <div class="col-sm-10">
                  <p class="text-start">{{ this.bookDetails.country }}</p>
                </div>
              </div>

              <div class="row">
                <div class="col-sm-2">
                  <p class="text-start fw-bold">Language:</p>
                </div>
                <div class="col-sm-10">
                  <p class="text-start">{{ this.bookDetails.language }}</p>
                </div>
              </div>

              <div class="row">
                <div class="col-sm-2">
                  <p class="text-start fw-bold">Pages:</p>
                </div>
                <div class="col-sm-10">
                  <p class="text-start">{{ this.bookDetails.pages }}</p>
                </div>
              </div>

              <div class="row">
                <div class="col-sm-2">
                  <p class="text-start fw-bold">Year:</p>
                </div>
                <div class="col-sm-10">
                  <p class="text-start">{{ this.bookDetails.year }}</p>
                </div>
              </div>

              <div class="row">
                <div class="col-sm-2">
                  <p class="text-start fw-bold">Description:</p>
                </div>
                <div class="col-sm-10">
                  <p class="text-start">{{ this.bookDetails.abstract }}</p>
                </div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
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
      bookDetails: null,
    };
  },
  methods: {
    getBookData(bookId) {
      axios
        .get(`http://localhost:8080/books/${bookId}`, {
          withCredentials: true,
        })
        .then((res) => {
          this.bookDetails = res.data;
          console.log(this.bookDetails.title);
        });
    },
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
<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Http</h1>
        <div class="form-group">
          <label for>Username</label>
          <input type="text" class="form-control" v-model="user.username" />
        </div>
        <div class="form-group">
          <label for>Email</label>
          <input type="text" class="form-control" v-model="user.email" />
        </div>
        <button class="btn btn-primary" @click="submit">Submit</button>
        <hr />
        <input type="text" class="form-control" v-model="node" />
        <br />
        <br />
        <button class="btn btn-primary" @click="getData">Get data</button>
        <hr />
        <ul class="list-group">
          <li
            class="list-group-item"
            v-for="u in users"
            :key="u.id"
          >{{ u.username }} - {{ u.email }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        username: "",
        email: ""
      },
      users: [],
      resource: {},
      node: "data"
    };
  },
  methods: {
    submit() {
      // this.$http.post("data.json", this.user).then(
      //   response => {
      //     console.log(response);
      //   },
      //   error => {
      //     console.log(error);
      //   }
      // );

      // this.resource.save({}, this.user);
      this.resource.saveAlt(this.user);
    },

    getData() {
      // this.$http
      //   .get("data.json")
      //   .then(response => {
      //     return response.json();
      //   })
      //   .then(data => {
      //     const resultArray = [];
      //     for (const key in data) {
      //       resultArray.push(data[key]);
      //     }
      //     this.users = resultArray;
      //   });
      this.resource
        .getData({ node: this.node })
        .then(response => {
          return response.json();
        })
        .then(data => {
          const resultArray = [];
          for (const key in data) {
            resultArray.push(data[key]);
          }
          this.users = resultArray;
        });
    }
  },
  created() {
    const customActions = {
      saveAlt: { method: "POST", url: "alternative.json" },
      getData: { method: "GET" }
    };

    this.resource = this.$resource("{node}.json", {}, customActions);
  }
};
</script>

<style>
</style>

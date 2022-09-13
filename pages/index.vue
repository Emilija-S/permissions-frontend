<template>
  <main>
    <section class="bg-light">
      <div class="container d-flex flex-column align-items-center py-5">
        <h1 class="fw-bold mb-5 text-center">USER-PERMISSION RELATION</h1>
        <div class="row d-flex justify-content-center mt-5">
          <div class="col-10 col-lg-8">
            <form
              id="user-permission-form"
              role="form"
              class="ui form"
              @submit.prevent="sendUserPermissions"
            >
              <div class="row">
                <select class="form-select col col-6 mt-3 mb-5"
                        id="permission_id"
                        name="permission_id"
                        v-model="form.permission_id"
                >
                  <option selected>Select the permission</option>
                  <option v-for="permission in permissions" :value="permission.id">{{ permission.name }}</option>
                </select>
                <select class="form-select col col-6 mt-3 mb-5"
                        id="user_id"
                        name="user_id"
                        v-model="form.user_id"
                >
                  <option selected>Select the user</option>
                  <option v-for="user in users" :value="user.id">{{ user.name }}</option>
                </select>
                <div class="d-flex justify-content-end">
                  <button @click="sendUserPermissions" type="submit"
                          class="ui button btn btn-outline-dark rounded-pill px-4 ">
                    SUBMIT
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      form: {
        permission_id: "",
        user_id: "",
      },
      users: [],
      permissions: [],
    };
  },
  created() {
    this.$axios.get('/api/all-users')
      .then((response) => {
        this.users = JSON.parse(JSON.stringify(response.data));
      })
      .catch((error) => {
        console.log(error);
      });
    this.$axios.get('/api/all-permissions')
      .then((response) => {
        this.permissions = JSON.parse(JSON.stringify(response.data));
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
      async sendUserPermissions() {
      try {
        await this.$axios.post('/api/user-permission', this.form);
      } catch (error) {
        console.log(error);
      } finally {
        console.log(this.form);
      }
    },
  }
}
</script>

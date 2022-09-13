<template>
  <main>
    <section class="bg-light">
      <div class="container d-flex flex-column align-items-center py-5">
        <h1 class="fw-bold mb-5 text-center">USER</h1>
        <div class="row d-flex justify-content-center mt-5">
          <div class="col-10 col-lg-8">
            <form
              id="member-form"
              role="form"
              class="ui form"
              @submit.prevent="sendUserPermissions"
            >
              <div class="row">
                <div class="col col-12 col-lg-6">
                  <label for="name">Name</label>
                  <input
                    data-bs-toggle="tooltip"
                    title="please fill out this field"
                    id="name"
                    name="name"
                    v-model="form.name"
                    type="text"
                    class="form-control bg-light border border-2 rounded-0 px-0 mb-5"
                  />
                </div>
                <div class="col col-12 col-lg-6">
                  <label for="email">Email</label>
                  <input
                    data-bs-toggle="tooltip"
                    title="please fill out this field"
                    id="email"
                    name="email"
                    v-model="form.email"
                    type="email"
                    class="form-control bg-light border border-2 rounded-0 px-0 mb-5"
                  />
                </div>
                <div class="col col-12">
                  <label for="password">Password</label>
                  <input
                    data-bs-toggle="tooltip"
                    title="please fill out this field"
                    id="password"
                    name="password"
                    v-model="form.password"
                    type="password"
                    class="form-control bg-light border border-2 rounded-0 px-0 mb-5"
                  />
                </div>
              </div>
              <select class="form-select form-select-sm col col-12 mt-3 mb-5"
                      multiple aria-label="multiple select example"
                      id="permissions"
                      name="permissions[]"
                      v-model="form.permissions"
              >
                <option value="1">READ</option>
                <option value="2">WRITE</option>
                <option value="3">EXECUTE</option>
              </select>
              <div class="d-flex justify-content-end">
                <button @click="sendUserPermissions" type="submit"
                        class="ui button btn btn-outline-dark rounded-pill px-4 ">
                  SUBMIT
                </button>
              </div>
            </form>
          </div>
        </div>
        <div class="my-5">
          {{ users }}
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
        name: "",
        email: "",
        password: "",
        permissions: [],
      },
      users: ""
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
  },
  methods: {
    async sendUserPermissions() {
      try {
        await this.$axios.post('/api/contact-form', this.form);
      } catch (error) {
        console.log(error);
      } finally {
      }
    },
  }
}
</script>

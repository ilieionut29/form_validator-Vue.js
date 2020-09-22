<template>
  <div>
    <form v-if="!isSubmitted">
      <div class="form-group ">
        <label for="fullName">Full name: </label>
        <input id="fullName" type="name" class="form-control" placeholder="First name & second name" v-model="formInputs.name" :fullName="formInputs.name">

        <label for="email-address">Email address:</label>
        <input id="email-address" type="email" class="form-control" placeholder="name@example.com" v-model.lazy="formInputs.email" :email="formInputs.email">

        <label for="password">Password:</label>
        <input id="password" type="password" class="form-control" v-model.lazy="formInputs.password" :password="formInputs.password">

        <label for="role">Selec your role</label>
        <select id="role" class="form-control" v-model.lazy="selectedRole">
          <option v-for="role in roles" v-bind:key="role" > {{role}} </option>
        </select>

        <fieldset class="form-group">
          <div class="row">
            <legend class="col-form-label col-sm-2 pt-0">Gender:</legend>
            <div class="col-sm-10">
              <div class="form-check">
                <input class="form-check-input" type="radio" name="gender" id="genderMale" value="Male" v-model.lazy="gender">
                <label class="form-check-label" for="genderMale">
                  Male
                </label>
              </div>

              <div class="form-check">
                <input class="form-check-input" type="radio" name="gender" id="genderFemeale" value="Femeale" v-model.lazy="gender">
                <label class="form-check-label" for="genderFemeale">
                  Female
                </label>
              </div>
            </div>
          </div>
        </fieldset>

        <label for="aboutMe">About me</label>
        <textarea class="form-control" id="aboutMe" rows="3" v-model.lazy="aboutMe"></textarea>
      </div>

      <div class="buttons">
        <button class="btn btn-success" @click.prevent="submit">Submit</button>
        <button class="btn btn-danger" @click="resetForm">Cancel</button>
      </div>
    </form>
    <div v-if="isSubmitted" id="submitedForm">
      Full name: {{formInputs.name}} <br>
      Email: {{formInputs.email}} <br>
      Password: {{formInputs.password}} <br>
      Role: {{selectedRole}} <br>
      Gender: {{gender}} <br>
      About me: {{aboutMe}} <br>
      <button class="btn btn-danger" @click="reloadPage">Reload Page</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formInputs: {
        name: "",
        email: "",
        password: ""
      },
      selectedRole: "UI/UX Designer",
      roles: ["Front End Developer", "Back End Developer", "UI/UX Designer"],
      gender: "",
      aboutMe: "",
      isSubmitted: false
    }
  },
  methods: {
    resetForm() {
      if(confirm("Do you really wana reset all the data?")) {
        this.formInputs.name = "";
        this.formInputs.email = "";
        this.formInputs.password = "";
        this.selectedRole = "";
        this.gender = "";
        this.aboutMe = "";
      }
    },
    submit() {
      if (this.formInputs.name == "" || 
          this.formInputs.email == "" || 
          this.formInputs.password == "" || 
          this.gender == "" ||
          this.aboutMe == "" ) {
        alert("Complete the form inputs!")
      } else {
        this.isSubmitted = true;
      }
    },
    reloadPage() {
      window.location.reload()
    }
  }
}

</script>

<style>
</style>

<template>
  <div>
    <b-navbar
      toggleable="lg"
      type="dark"
      variant="info"
      style="background: #28333a !important"
    >
      <b-navbar-brand href="#"
        ><img
          style="width: 6em"
          src="https://www.toronto.ca/wp-content/themes/cot/img/logo.svg"
      /></b-navbar-brand>

      <!-- <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#">Link</b-nav-item>
          <b-nav-item href="#" disabled>Smart Simple </b-nav-item>
        </b-navbar-nav>
 
      </b-collapse> -->
    </b-navbar>

    <b-form @submit="onSubmit" class="p-4">
      <h1 class="mt-4">TPH - SmartSimple Incident Report Form</h1>
      <p class="text-muted">
        This form will help pre-populate an email to the TPH SmartSimple IT
        support staff. <br />
        <span class="text-danger"
          >Please note that only emails sent using the format prepared by this
          form will be accepted.</span
        >
      </p>
      <div class="row">
        <b-form-group
          label="Summary/Title:"
          label-for="input-title"
          class="col-lg-6"
        >
          <b-form-input
            id="input-title"
            v-model="form.title"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="Type of change:"
          label-for="input-typeofchange"
          class="col-lg-6"
        >
          <b-form-select
            id="input-typeofchange"
            v-model="form.typeofchange"
            :options="typeofchange"
            required
          ></b-form-select>
        </b-form-group>
      </div>

      <b-form-group>
        <div class="row">
          <div class="col-6">
            <label for="input-date">Date of occurance</label>
            <b-form-datepicker
              id="input-date"
              v-model="form.date"
              class="mb-2"
              required
            ></b-form-datepicker>
          </div>
          <div class="col-6">
            <label for="input-time">Time of occurance (optional)</label>
            <b-input-group>
              <b-form-input
                id="input-time"
                v-model="form.time"
                type="text"
                placeholder="HH:mm:ss"
              ></b-form-input>
              <b-input-group-append>
                <b-form-timepicker
                  v-model="form.time"
                  button-only
                  right
                  show-seconds
                  locale="en"
                  aria-controls="example-input"
                ></b-form-timepicker>
              </b-input-group-append>
            </b-input-group>
          </div>
        </div>
      </b-form-group>

      <div class="row">
        <b-form-group
          label="Program:"
          label-for="radio-program"
          class="col-lg-6"
        >
          <b-form-radio-group
            id="radio-program"
            v-model="form.program"
            :options="programs"
            required
          ></b-form-radio-group>
        </b-form-group>

        <b-form-group
          label="Has your manager approved this change:"
          label-for="radio-managerApproval"
          class="col-lg-6"
        >
          <b-form-radio-group
            id="radio-managerApproval"
            v-model="form.managerApproval"
            :options="yesno"
            required
            name="radio-options"
          ></b-form-radio-group>
        </b-form-group>
      </div>

      <div class="row">
        <b-form-group
          label="Person we can contact:"
          label-for="input-contact"
          class="col-lg-6"
        >
          <b-form-input
            id="input-contact"
            v-model="form.contact"
            placeholder="firstname.lastname@toronto.ca"
            required
            type="email"
          ></b-form-input>
        </b-form-group>
        <b-form-group
          label="Affected User (optional):"
          label-for="input-affected"
          class="col-lg-6"
        >
          <b-form-input
            id="input-affected"
            v-model="form.affected"
            placeholder="firstname.lastname@toronto.ca"
            type="email"
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="Issue Description:"
          label-for="textarea-issue"
          class="col-lg-6"
        >
          <b-form-textarea
            id="textarea-issue"
            rows="3"
            max-rows="8"
            v-model="form.issue"
          ></b-form-textarea>
          <p class="text-muted">
            Where in the flow was this issue encountered? <br />
            Please give Clear step by step directions from the login screen.
          </p>
        </b-form-group>

        <b-form-group
          label="Expected Results:"
          label-for="textarea-Expected"
          class="col-lg-6"
          v-model="form.expected"
        >
          <b-form-textarea
            id="textarea-Expected"
            rows="3"
            max-rows="8"
            v-model="form.expected"
          ></b-form-textarea>
          <p class="text-muted">
            Please describe in as much detail as possible.
          </p>
        </b-form-group>
      </div>
      <div class="alert alert-warning">
        Screenshots & video links are encouraged to help facilitate better
        communication, you may include these in the email.
      </div>
      <b-button type="reset" variant="secondary" class="mr-3">Reset</b-button>
      <b-button type="submit" variant="success">Prefill my Email</b-button>
    </b-form>

    <div class="d-none" id="emailTemplate">
      Type of change:{{ form.typeofchange }}

      Date of occurance: {{ form.date }}

      Time of occurance: {{ form.time }}

      Program: {{ form.program }}

      Has your manager approved this change: {{ form.managerApproval }}

      Person we can contact: {{ form.contact }}

      Affected User: {{ form.affected }}

      Issue Description:
      {{ form.issue }}

      Expected Result:
      {{ form.expected }}
    </div>
  </div>
</template>

<style>
/* body {} */
</style>

<script>
export default {
  data() {
    return {
      name: "SmartSimple incident Reporting",
      form: {
        title: "",
        name: "",
        program: "",
        date: "",
        time: "",
        contact: "",
        affected: "",
        typeofchange: "",
        managerApproval: "",
        issue: "",
        expected: "",
      },
      programs: [
        { value: "TUHF", text: "TUHF" },
        { value: "SNP", text: "SNP" },
      ],
      typeofchange: [
        { value: "General", text: "General" },
        { value: "New functionality", text: "New functionality" },
        { value: "Data Change", text: "Data Change" },
      ],
      yesno: [
        { value: "Yes", text: "Yes" },
        { value: "No", text: "No" },
      ],
    };
  },
  methods: {
    onSubmit() {
      console.log("Toggle button clicked");
      window.location.href =
        "mailto:tphsmartsimple@toronto.ca?" +
        "subject=" +
        this.form.title +
        " - SmartSimple Incident Report&" +
        "body=" +
        encodeURIComponent(document.getElementById("emailTemplate").innerHTML);
    },
  },
};
</script>
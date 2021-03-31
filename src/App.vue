<template>
  <div>
    <h1>Toronto Public Health - SmartSimple Incident Report Form</h1>
    <b-form @submit="onSubmit">
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
            required
          ></b-form-input>
        </b-form-group>
      </div>

      <!-- 

Issue Description:

Screen print:
Where in the flow the issue was encountered:  
Please give directions from the login screen.
Clear step by step. 
Screenshots & video links are encouraged to help facilitate better communication

Note: sometimes contact person is not the actual person ( i.e Herb can raise the issue but it’s really someone else’s .. ) 


Expected Result:
Screenshots & video links are encouraged to help facilitate better communication -->
      <div class="alert alert-warning">Please geat</div>
      <b-button type="reset" variant="secondary" class="mr-3">Reset</b-button>
      <b-button type="submit" variant="success">Start Ticket</b-button>
    </b-form>
  </div>
</template>

<style>
body {
  padding: 1rem;
}
</style>

<script>
export default {
  data() {
    return {
      name: "BootstrapVue",
      form: {
        title: "",
        name: "",
        program: "",
        date: "",
        time: "",
        contact: "",
        affected: "",
        managerApproval: "",
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
  watch: {
    show(newVal) {
      console.log(`Alert is now ${newVal ? "visible" : "hidden"}`);
    },
  },
  methods: {
    onSubmit() {
      console.log("Toggle button clicked");
      window.location.href =
        "mailto:tphsmartsimple@toronto.ca?bcc=subhas.fagu@toronto.ca, andreea.gray@toronto.ca&"+
        "subject=SmartSimple Incident Report&"+
        "body="+
        "Hi%20Bob,%0d%0dI%20would%20like%20to%20RSVP%20to%20your%20party%20invitation.%20Here%20are%20my%20details:%0d%0dName:%20Eryka%20Adams%0dNumber%20of%20Guest:%0d";
    },
  },
};
</script>
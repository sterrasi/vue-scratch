<template>
<ValidationObserver ref="observer">
    <b-form slot-scope="{ validate }" @submit.prevent="validate().then(onSubmit)" @reset="resetForm">
      <ValidationProvider rules="required|email" name="Email">
        <b-form-group 
          slot-scope="{ valid, errors }"
          label="Email address:"
          label-for="exampleInput1"
          description="We'll never share your email with anyone else.">      
            <b-form-input
              type="email"
              v-model="email"
              :state="errors[0] ? false : (valid ? true : null)"
              placeholder="Enter email">
            </b-form-input>
            <b-form-invalid-feedback id="inputLiveFeedback">
              {{ errors[0] }}
            </b-form-invalid-feedback>
        </b-form-group>
      </ValidationProvider>

      <ValidationProvider rules="required" name="Password" vid="password">
        <b-form-group 
          slot-scope="{ valid, errors }"
          label="Password:"
          description="We'll never share your password with anyone else.">      
            <b-form-input
              type="password"
              v-model="password"
              :state="errors[0] ? false : (valid ? true : null)"
              placeholder="Enter password">
            </b-form-input>
            <b-form-invalid-feedback id="inputLiveFeedback">
              {{ errors[0] }}
            </b-form-invalid-feedback>
        </b-form-group>
      </ValidationProvider>

      <ValidationProvider rules="required|confirmed:password" name="Password confirmation">
        <b-form-group 
          slot-scope="{ valid, errors }"
          label="Confirm Password:"
          label-for="exampleInput1">
            <b-form-input
              type="password"
              v-model="confirmation"
              :state="errors[0] ? false : (valid ? true : null)"
              placeholder="Confirm Password">
            </b-form-input>
            <b-form-invalid-feedback id="inputLiveFeedback">
              {{ errors[0] }}
            </b-form-invalid-feedback>
        </b-form-group>
      </ValidationProvider>

      <ValidationProvider name="Subject" rules="required">
        <b-form-group id="exampleInputGroup3"
          slot-scope="{ valid, errors }"
          label="Subject:"
          label-for="exampleInput3">
          <b-form-select id="exampleInput3"
              :state="errors[0] ? false : (valid ? true : null)"
              v-model="subject">
            <option value="">None</option>
            <option value="S1">Subject 1</option>
            <option value="S2">Subject 2</option>
          </b-form-select>
            <b-form-invalid-feedback id="inputLiveFeedback">
              {{ errors[0] }}
            </b-form-invalid-feedback>
        </b-form-group>
      </ValidationProvider>
      <ValidationProvider name="Subject" rules="required|length:2">
        <b-form-group id="exampleGroup4" slot-scope="{ valid, errors }">
          <b-form-checkbox-group :state="errors[0] ? false : (valid ? true : null)" v-model="choices" id="exampleChecks">
            <b-form-checkbox value="Coffee">Coffe</b-form-checkbox>
            <b-form-checkbox value="Tea">Tea</b-form-checkbox>
            <b-form-checkbox value="Soda">Soda</b-form-checkbox>
          </b-form-checkbox-group>
          <b-form-invalid-feedback id="inputLiveFeedback">
            {{ errors[0] }}
          </b-form-invalid-feedback>
        </b-form-group>
      </ValidationProvider>
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
</ValidationObserver>
</template>

<script>
import { ValidationObserver, ValidationProvider } from 'vee-validate';

export default {
  name: "BootstrapForm",
  components: {
    ValidationObserver,
    ValidationProvider
  },
  data: () => ({
    email: '',
    password: '',
    confirmation: '',
    subject: '',
    choices: []
  }),
  methods: {
    onSubmit () {
      console.log('Form submitted yay!');
    },
    resetForm () {
      this.email = '';
      this.password = '';
      this.confirmation = '';
      this.subject = '';
      this.choices = [];
      requestAnimationFrame(() => {
        this.$refs.observer.reset();
      });
    }
  }
};
</script>

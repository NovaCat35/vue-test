<script setup lang="ts">
import { reactive } from "vue";
import {
  NysButton,
  NysCheckbox,
  NysCheckboxgroup,
  NysRadiobutton,
  NysRadiogroup,
  NysTextinput,
} from "@nysds/vue";
 
const model = reactive({
  firstName: "",
  agree: false,
  languages: [] as string[],
  contact: "",
});

function onLanguagesChange(e: any) {
  const { value, checked } = e.detail;
  if (checked) {
    if (!model.languages.includes(value)) {
      model.languages.push(value);
    }
  } else {
    model.languages = model.languages.filter((l) => l !== value);
  }
}
 
function onSubmit() {
  console.log(model);
}
</script>
 
<template>
  <form @submit.prevent="onSubmit">
    <NysTextinput v-model="model.firstName" label="First name" required />
    <NysCheckbox v-model="model.agree" label="I agree to the terms" />
    <NysCheckboxgroup label="Languages" name="contact1" @nys-change="onLanguagesChange">
      <NysCheckbox label="English" value="en" name="contact1" :checked="model.languages.includes('en')"/>
      <NysCheckbox label="Spanish" value="es" name="contact1" :checked="model.languages.includes('es')"/>
    </NysCheckboxgroup>
 
    <NysRadiogroup v-model="model.contact" label="Preferred contact" name="contact">
      <NysRadiobutton label="Email" name="contact" value="email" />
      <NysRadiobutton label="Phone" name="contact" value="phone" />
    </NysRadiogroup>
 
    <NysButton type="submit" label="Submit" />
  </form>
</template>
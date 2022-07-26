<template>
  <div>
    <h1>Create an Event</h1>
    <form @submit="submit">
      <BaseSelect
        label="Select a category"
        :options="categories"
        v-model="category"
        :error="errors.category"
      />

      <h3>Name & describe your event</h3>
      <BaseInput
        label="Title"
        type="text"
        v-model="title"
        :error="errors.title"
      />

      <BaseInput
        label="Description"
        type="text"
        v-model="description"
        :error="errors.description"
      />

      <h3>Where is your event?</h3>
      <BaseInput
        label="Location"
        type="text"
        v-model="location"
        :error="errors.location"
      />

      <h3>Are pets allowed?</h3>
      <BaseRadioGroup
        name="pets"
        :options="[
          { value: 1, label: 'Yes' },
          { value: 0, label: 'No' }
        ]"
        v-model="pets"
        :error="errors.pets"
      />

      <h3>Extras</h3>
      <div>
        <BaseCheckbox
          label="Catering"
          v-model="catering"
          :error="errors.catering"
        />
      </div>

      <div>
        <BaseCheckbox
          label="Live music"
          v-model="music"
          :error="errors.music"
        />
      </div>

      <div>
        <BaseButton type="submit" class="-fill-gradient">
          Submit
        </BaseButton>
      </div>
    </form>
  </div>
</template>

<script>
import { useForm, useField } from 'vee-validate'

export default {
  data () {
    return {
      categories: [
        'sustainability',
        'nature',
        'animal welfare',
        'housing',
        'education',
        'food',
        'community'
      ]
    }
  },
  setup () {
    // Validator
    const required = value => {
      const requiredMessage = 'This field is required'
      if (value === undefined || value === null) return requiredMessage
      if (!String(value).length) return requiredMessage

      return true
    }

    // Validator
    const minLength = (number, value) => {
      return String(value).length < number
        ? `Please type at least ${number} characters`
        : true
    }

    // Validator
    const anything = () => {
      return true
    }

    const validationSchema = {
      category: required,
      title: value => {
        const req = required(value)
        if (req !== true) return req

        const min = minLength(3, value)
        if (min !== true) return min

        return true
      },
      description: required,
      location: undefined,
      pets: anything,
      music: anything
    }

    const { handleSubmit, errors } = useForm({
      validationSchema,
      initialValues: {
        pets: 1,
        catering: false,
        music: false
      }
    })

    const { value: category } = useField('category')
    const { value: title } = useField('title')
    const { value: description } = useField('description')
    const { value: location } = useField('location')
    const { value: pets } = useField('pets')
    const { value: catering } = useField('catering')
    const { value: music } = useField('music')

    const submit = handleSubmit(values => {
      // the callback only happen if there is no errors
      console.log('submit', values)
    })

    return {
      category,
      title,
      description,
      location,
      pets,
      catering,
      music,
      submit,
      errors
    }
  }
}
</script>

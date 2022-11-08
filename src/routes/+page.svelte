<script>
    import { createForm } from "svelte-forms-lib";
    import * as yup from "yup";
  
    yup.setLocale({
      mixed: {
        default: "Có lỗi xảy ra",
        required: "Trường này không được để trống",
      },
      string: {
        min: ({ min }) => `Độ dài tối thiểu là ${min}`,
      },
    });
  
    const { form, errors, handleChange, handleSubmit } = createForm({
      initialValues: {
        length_name: "3",
        name: "",
        email: "",
        age: "",
        dob: "",
      },
      validationSchema: yup.object().shape({
        title: yup.string().oneOf(["Mr.", "Mrs.", "Mx."]).required(),
        length_name: yup.number().integer().required(),
        name: yup.string().min(yup.ref("length_name")).required(),
        email: yup.string().email().required(),
        age: yup.number().integer().min(18).max(30).required(),
        dob: yup
          .date()
          .min("2022-11-1", "Ngày nhỏ nhất là 1-11-2022")
          .max(new Date().toDateString(), "Không thể là ngày ở tương lai")
          .required(),
      }),
      onSubmit: (values) => {
        alert(JSON.stringify(values));
      },
    });
  </script>
  
  <form on:submit={handleSubmit}>
    <label for="title">title</label>
    <select
      id="title"
      name="title"
      on:change={handleChange}
      bind:value={$form.title}
    >
      <option />
      <option>Mr.</option>
      <option>Mrs.</option>
      <option>Mx.</option>
    </select>
    {#if $errors.title}
      <small>{$errors.title}</small>
    {/if}
  
    <label for="length_name">Length of Name</label>
    <input
      id="length_name"
      name="length_name"
      on:change={handleChange}
      on:blur={handleChange}
      bind:value={$form.length_name}
    />
    {#if $errors.length_name}
      <small>{$errors.length_name}</small>
    {/if}
  
    <label for="name">name</label>
    <input
      id="name"
      name="name"
      on:change={handleChange}
      on:blur={handleChange}
      bind:value={$form.name}
    />
    {#if $errors.name}
      <small>{$errors.name}</small>
    {/if}
  
    <label for="email">email</label>
    <input
      id="email"
      name="email"
      on:change={handleChange}
      on:blur={handleChange}
      bind:value={$form.email}
    />
    {#if $errors.email}
      <small>{$errors.email}</small>
    {/if}
  
    <label for="age">age</label>
    <input
      id="age"
      type="text"
      name="age"
      on:change={handleChange}
      on:blur={handleChange}
      bind:value={$form.age}
      placeholder="Age is between 18 and 30"
    />
    {#if $errors.age}
      <small>{$errors.age}</small>
    {/if}
  
    <label for="dob">date of birth</label>
    <input
      id="dob"
      type="date"
      name="dob"
      on:change={handleChange}
      on:blur={handleChange}
      bind:value={$form.dob}
    />
    {#if $errors.dob}
      <small>{$errors.dob}</small>
    {/if}
  
    <button type="submit">submit</button>
  </form>
  
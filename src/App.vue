<script>
export default {
  data() {
    return {
      experiences: [
        {id: 1, title: 'Starter Frontend Engineer', company: 'Qatros', duration: 'Aug 2022 - present', desc: 'Membuat aplikasi menggunakan framework Vue.js'},
        {id: 2, title: 'Frontend Engineer ', company: 'Ruangguru', duration: 'Feb 2022 - Jul 2022', desc: 'Membuat aplikasi menggunakan ReactJs'},
        {id: 3, title: 'Frontend Developer', company: 'Evomo', duration: 'Aug 2021 - Nov 2021', desc: 'Membuat aplikasi menggunakan framework Angular'},
      ] ,
      skills: [
        {title: 'ReactJs', percentage: 70},
        {title: 'Vue.js', percentage: 10},
        {title: 'HTML', percentage: 90},
        {title: 'CSS', percentage: 60},
      ],
      isOpen : false,
      selectedId: null,
      name: '',
      email: '',
      note: '',
      percentage: 0,
    }
  },
  methods: {
    handleClick(id) {
      if (id === this.selectedId) {
        this.selectedId = null
      } else {
        this.selectedId = id
      }
    },
    handleSubmit() {
      alert(`Thank you ${this.name}, we'll send you an email to ${this.email} regarding ${this.note}`)
    },
    handleForm() {
      this.$refs.form.reset()
    }
  }
}
</script>

<template>
  <div class="container">
    <h1>Resume</h1>
    <h2>Elroy Pedro Kameo</h2>
    <p>Hi! Saya adalah seorang Frontend Engineer Intern di Qatros</p>
    <div>
      <h2>Experiences</h2>
      <ol>
        <li class="skill" v-for="experience in experiences" :key="experience.id" @click="handleClick(experience.id)" >
          {{ experience.duration }} - {{ experience.title }} at {{ experience.company }}   
            <p v-if="experience.id === selectedId">{{ experience.desc }}</p>
        </li>
      </ol>
    </div>
    <div>
      <h2>Skills</h2>
      <ol>
        <li v-for="skill in skills" :key="skill.title">
          {{ skill.title }} - {{ skill.percentage }}%
          <div class="bar">
            <div class="percentage" :style="{'width': skill.percentage + '%'}"></div>
          </div>
        </li>
      </ol>
    </div>
    <div>
      <h2>Contact Me</h2>
      <form class="inputform" ref="form" action="submit" @submit.prevent="handleForm()">
        <div class="input-name">
          <label for="name">Name</label>
          <input v-model="name" type="text" required>
        </div>
        <div class="input-email">
          <label for="email">Email</label>
          <input v-model="email" type="email" required>
        </div>
        <div class="input-note">
          <label for="note">Note</label>
          <textarea v-model="note" name="note"></textarea>
        </div>
        <button class="btn-submit" @click="handleSubmit()">Submit</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
  .container {
    margin-left: 50%;
    width: 100%;
  }
  .bar {
    width: 100%;
    height: 20px;
    background-color: #ddd;
    border-radius: 20px;
  }
  .percentage {
    height: 100%;
    background-color: #4CAF50;
    border-radius: 20px;
  }
  .inputform {
    display: flex;
    flex-direction: column;
  }
  .input-name, .input-email, .input-note {
    display: flex;
    flex-direction: column;
  }
  input, textarea {
    padding: 5px;
  }
  .btn-submit {
    width: 100px;
    height: 30px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    margin: 20px 0 20px;
  }
  .skill {
    cursor: pointer;
  }
</style>

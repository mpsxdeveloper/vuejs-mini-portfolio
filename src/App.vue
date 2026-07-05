<template>  
  <div style="padding: 10px;">
    <h2 style="width: 100%; text-align: center;">Vue.js Mini Portfolio</h2>
    <div class="wrapper">
      <div class="inputs">
        <textarea id="text" v-model="text" placeholder="Enter your main text" rows="3"></textarea>
        <input type="text" v-model="objective" placeholder="Enter your career objective" />
        <input type="text" @keydown.enter="addJob" placeholder="Enter a job title and press Enter" />
        <input type="text" v-model="skillsTitle" placeholder="Skills section title (e.g. Skills, Talents, Abilities)" />
        <select @change="addSkill">
          <option value="">Select a skill</option>
          <option v-for="skill in skills" :key="skill.icon" :value="skill.icon">{{ skill.title }}</option>
        </select>
      </div>
      <div class="output">
        <div class="card">
          <div class="card-text">{{ text }}</div>
          <div>
            <h2 style="text-align: center;">{{ objective }}</h2>
            <div class="jobs">                
              <div v-for="job in jobs" :key="job">
                <div class="job">{{ job }}</div>
              </div>
            </div>
          </div>
          <div>
            <h2 style="text-align: center;">{{ skillsTitle}}</h2>
            <div class="skills">
              <div v-for="skill in mySkills" :key="skill.icon">
                <div style="margin-bottom: 15px;">
                  <i :class="'fa-brands ' + skill.icon"></i> <span class="skill">{{ skill.title }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>        
    </div>      
  </div>  
</template>

<script setup>

import { onMounted, ref } from 'vue'
const text = ref('')
const objective = ref('')
const skillsTitle = ref('')
const skills = ref([])
const mySkills = ref([])
const jobs = ref([])

function addSkill(e) {
  const skill = e.target.value
  if(skill !== '') {
    const options = e.target.options
    const selectedOption = options[options.selectedIndex]
    skills.value = skills.value.filter(s => s.icon !== skill)
    mySkills.value.push({title: selectedOption.innerHTML, icon: skill})      
  }   
}

function addJob(e) {
  const job = e.target.value
  if(job !== '' && e.key === 'Enter') {
    if(!jobs.value.includes(job)) {
      jobs.value.push(job)
      e.target.value = ''
    }
  }
}

onMounted(() => {
  skills.value.push({ title: 'HTML', icon: 'fa-html5'})
  skills.value.push({ title: 'CSS', icon: 'fa-css3-alt'})
  skills.value.push({ title: 'Bootstrap', icon: 'fa-bootstrap'})
  skills.value.push({ title: 'JavaScript', icon: 'fa-square-js'})
  skills.value.push({ title: 'PHP', icon: 'fa-php'})
  skills.value.push({ title: 'Laravel', icon: 'fa-laravel'})
  skills.value.push({ title: 'Vue.js', icon: 'fa-vuejs'})
  skills.value.push({ title: 'Node.js', icon: 'fa-node'})
  skills.value.push({ title: 'Unity', icon: 'fa-unity'})
})

</script>

<style scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css");
.wrapper {
  display: flex;
}
.inputs {
  width: 50%;
  display: flex;
  flex-direction: column;
}
textarea, input[type=text], select {
  resize: none;
  padding: 10px;
  margin: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
.output {
  width: 50%;
  display: flex;
  flex-direction: column;
}
.card {
  border: 1px solid #000;    
  height: auto;
  padding: 10px;
  margin: 10px;    
  word-wrap: break-word;
}
.card-text {
  padding: 10px;
}
.skills, .jobs {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  margin-top: 10px;
  padding: 5px;    
}
.skill {
  margin-right: 5px;
  margin-top: 5px;
  border-radius: 8px;
  padding: 5px;
  background-color: #2196F3;
}
.job {
  border: 1px solid #000;
  border-radius: 25%;
  padding: 10px;
  margin: 5px;
  background-color: #4CAF50;
}
</style>

<template>
  <div id="app">
    <nav class="navbar is-white topNav">
      <div class="container">
        <div class="navbar-brand">
          <h1>Activity Planner</h1>
        </div>
      </div>
    </nav>
    <nav class="navbar is-white">
      <div class="container">
        <div class="navbar-menu">
          <div class="navbar-start">
            <a class="navbar-item is-active" href="#">Newest</a>
            <a class="navbar-item" href="#">In Progress</a>
            <a class="navbar-item" href="#">Finished</a>
          </div>
        </div>
      </div>
    </nav>
    <section class="container">
      <div class="columns">
        <div class="column is-3">
          <a v-if="!isFormDisplayed" @click="isFormDisplayed = !isFormDisplayed" class="button is-primary is-block is-alt is-large" href="#">New Activity</a>
          <div v-if="isFormDisplayed" class="create-form">
            <h2>Create Activity</h2>
            <form>
              <div class="field">
                <label class="label">Title</label>
                <div class="control">
                  <input v-model="newActivity.title" class="input" type="text" placeholder="Read a Book">
                </div>
              </div>
              <div class="field">
                <label class="label">Notes</label>
                <div class="control">
                  <textarea v-model="newActivity.notes" class="textarea" placeholder="Write some notes here"></textarea>
                </div>
              </div>
              <div class="field is-grouped">
                <div class="control">
                  <button @click="createActivity" class="button is-link">Create Activity</button>
                </div>
                <div class="control">
                  <button @click="toggleFormDisplay" class="button is-text">Cancel</button>
                </div>
              </div>
            </form>
          </div>
        </div>

        <div class="column is-9">
          <div class="box content">
            <Activityitem
                    v-for="activity in activities"
                    :activity="activity"
                    :key="activity.id"></Activityitem>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
  import Activityitem from '@/components/Activityitem'
  import { activites } from '@/api/index'
  export default {
    name:'App',
    data() {
      return {
          message:'Hello Vue',
          titleMessage: 'Title Message Vue!!!!!',
          isTextDispalyed:true,
          isFormDisplayed:false,
          user: {
            name: 'Filip Jerga',
            id: '-Aj34jknvncx98812',
          },
          newActivity:{
            title:'',
            notes:''
          },
          activities: {},
          categories: {
            '1546969049': {text: 'books'},
            '1546969225': {text: 'movies'}
          },
      }
    },
    components:{
      Activityitem
    },
    beforeCreate() {
      console.log('before create')
    },
    created() {
      this.activities = activites()
    },
    beforeMount() {
      console.log('before mount')
    },
    mounted() {
      console.log('mounted')
    },
    beforeUpdate() {
      console.log('before update')
    },
    updated() {
      console.log('before updated')
    },
    beforeDestroy() {
      console.log('before destroy')
    },
    destroyed() {
      console.log('destroed')
    },
    methods: {
      createActivity() {
        this.activities.push({
          'test' : {
            id: new Date(),
            title:this.newActivity.title,
            notes:this.newActivity.notes
          }
        })
      },
      toggleFormDisplay () {
        this.isFormDisplayed = !this.isFormDisplayed;
      }
    }
  }
</script>
<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

html,body {
  font-family: 'Open Sans', serif;
  background: #F2F6FA;
}
footer {
  background-color: #F2F6FA !important;
}
.topNav {
  border-top: 5px solid #3498DB;
}
.topNav .container {
  border-bottom: 1px solid #E6EAEE;
}
.container .columns {
  margin: 3rem 0;
}
.navbar-menu .navbar-item {
  padding: 0 2rem;
}
aside.menu {
  padding-top: 3rem;
}
aside.menu .menu-list {
  line-height: 1.5;
}
aside.menu .menu-label {
  padding-left: 10px;
  font-weight: 700;
}
.button.is-primary.is-alt {
  background: #00c6ff;
  background: -webkit-linear-gradient(to bottom, #0072ff, #00c6ff);
  background: linear-gradient(to bottom, #0072ff, #00c6ff);
  font-weight: 700;
  font-size: 14px;
  height: 3rem;
  line-height: 2.8;
}
.media-left img {
  border-radius: 50%;
}
.media-content p {
  font-size: 14px;
  line-height: 2.3;
  font-weight: 700;
  color: #8F99A3;
}
article.post {
  margin: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #E6EAEE;
}
article.post:last-child {
  padding-bottom: 0;
  border-bottom: none;
}
.menu-list li{
  padding: 5px;
}

</style>

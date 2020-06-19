<template>
  <section class="section">
    <div class="columns is-desktop is-multiline">
      <div class="column is-8">
        <h1 class="title">Advent of Code 2019 Solutions</h1>
        <h2 class="subtitle">by Austin Barrett</h2>

        <p>
          <a href="https://adventofcode.com/" target="_blank" rel="noopener">Advent of Code</a> is an Advent calendar of
          small programming puzzles for a variety of skill sets and skill levels that can be solved in any programming
          language you like. People use them as a speed contest, interview prep, company training, university
          coursework, practice problems, or to challenge each other.
        </p>
        <br>
        <p>
          <span class="is-hidden-touch">To the right</span>
          <span class="is-hidden-desktop">Below</span>
          are my solutions for each day's challenge. Most solution can be used to validate your answers, but be sure to do the work your self (cheaters never prosper). I will update solutions as i sol
        </p>
      </div>

      <div class="column">
        <nav class="panel">
          <p class="panel-heading">
            Challenges
          </p>
          <div class="panel-block">
            <p class="control has-icons-left">
              <input class="input" type="text" placeholder="Search" v-model="linkSearch">
              <span class="icon is-left">
                <i class="mdi mdi-magnify" aria-hidden="true"></i>
              </span>
            </p>
          </div>
          <n-link class="panel-block is-active" v-for="link in links" :to="link.path">
            {{link.name | name}}
          </n-link>
        </nav>
      </div>
    </div>
  </section>
</template>

<script>

  export default {
    name: 'HomePage',
    data() {
      return {
        linkSearch: ''
      }
    },
    computed: {
      links() {
        let routes = this.$router.options.routes.filter(x => x.name !== 'index');
        return !!this.linkSearch ? routes.filter(x => x.name.toString().toLowerCase().includes(this.linkSearch.toLowerCase())) : routes
      }
    },
    filters: {
      name: (value) => {
        if (!value) return '';
        value = value.toString();
        return value.slice(0, 4) === 'day-' ? value.slice(4) : value
      }
    }
  }
</script>

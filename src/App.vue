<template>
  <div id="app">
    <h1>Vue Checklist Demo</h1>
    <!-- NOTE: this is a joke. Don't take content seriously. And don't judge the spelling/ language, aint no one got time for that shit -->
    <Checklist :theList="theList" title="Code Quality Checklist"/>

    <!-- Links for come context -->
    <footer class="more-links">
      <p>This is a quick demo, of a simple checklist component for Vue, with persistant memory</p>
      <p>The source code, can be found in this repo: <a href="https://github.com/Lissy93/vue-checklist">github.com/Lissy93/vue-checklist</a></p>
      <p>For a demo, of this used in action in a real use case, check out <a href="#">LINK-COMING-SOON</a></p>
      <p>Licensed under the <a href="https://gist.github.com/Lissy93/143d2ee01ccc5c052a17">MIT</a>, © <a href="https://aliciasykes.com">Alicia Sykes</a> 2019</p>
    </footer>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Checklist  from './components/Checklist.vue';

@Component({
  components: {
    Checklist,
  },
  data: () => {
        return  {
            theList: [
                { name: 'Lint', description: 'You need to lint your shit. That trailing white space on line 76 might well be the end of your maridge.', checked: false },
                { name: 'Test', description: 'It\'s all well and good writing code that works totally fine if the user enters Hello World. But if you don\'t test, and the user missed the \'d\' from world, the world may just implode', checked: false },
                { name: 'Type Checking', description: 'Lets face it, we\'re embarassed and ashamed to be JavaScript developers, so in a half-hearted effort to be just very slightly less uncool, use TypeScript/ Flow to implement data types', checked: false },
                { name: 'Documentation', description: 'Yeah, we\'ve all heard it said, clean code doesn\'t need comments. But truth is, it\'s 4 AM, you\'ve had a couple of pints and have been programming 19 hours strait, without out comments your not going to understand that code on Monday, let alont in a months time.', checked: false },
                { name: 'Use Standards', description: 'If you don\'t inforce common standards, the monkeys you employ because your on a budget, will invent their own crazy places to put curly braces, and your source code will end up looking like a pice of ASCII art', checked: false },
                { name: 'Give variables meaningful names', description: 'Naming your variables affter all your ex-boyfriends may seem like a `great idea at the time, but come to debugging it 6 weeks later, and you have no idea why the f*ck Darren is 6 and Frank is undefined', checked: false },
                { name: 'Have a .gitignore', description: 'It\'s near the worst thing ever, when you pull a repo, and the developer has left their .editor-config, you open if up in your IDE, and instead of youe sick dark theme, you get the origional authors gopping white theme, and your eye\'s are burning', checked: false },
            ],
        };
    },
})
export default class App extends Vue {}
</script>

<style lang="scss">
body {
  margin: 0;
  background: #ffff76;
}
h1 {
  color: #00bcd4;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  padding: 5em;
}

.inner-item .checkbox-container.checkbox-active .checkbox-group { 
  background-color: #00bcd4; 
  border-color: #00bcd4; 
}

.more-links {
  margin-top: 5em;
  p {
    text-align: center;
    a {
      color: #00bcd4;
      text-decoration: none;
      &:hover { text-decoration: underline;}
    }
  }
}
</style>

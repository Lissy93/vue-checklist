<template>
    <div class="item">
        <VueCheckbox  :value="id" v-model="checked">{{ name }}</VueCheckbox>
        <span>{{ details }}</span>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { VueCheckbox  } from 'vue-material-checkbox';

// localStorage persistence
const STORAGE_KEY = 'todos-vuejs-2.0'
const checkboxStorage: any = {
  fetch: () => {
    let checked = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
    checked.forEach(function (check: any, index: number) {
      check.id = index;
    })
    checkboxStorage.uid = checked.length;
    return checked;
  },
  save: function (checked: any) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(checked))
  }
}


@Component({
    components: {
        VueCheckbox,
    },
    data: () => {
        return {
            checked: checkboxStorage.fetch(),
        }
    },
})
export default class ChecklistItem extends Vue {
    @Prop() private id!: string;
    @Prop() private name!: string;
    @Prop() private details!: string;
}
</script>

<style scoped lang="scss">
    .item{
        padding: 0.5em 1em;
        margin: 0.5em 0;


        // background: #FFF;
        // box-shadow: 
        //     0 -1px 0 #e0e0e0, 
        //     0 0 2px rgba(0,0,0,.12), 
        //     0 2px 4px rgba(0,0,0,.24);
        // border-radius: 2px;
    }
</style>

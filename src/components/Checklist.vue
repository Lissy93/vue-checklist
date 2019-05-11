<template>
    <div class="checklist">
        <ChecklistHeader :title="title" />
        <div v-for="(checkItem, index) in theList" :key="checkItem.name" :name="`chk-${index}`" class="item">
            <ChecklistItem :id="makeId(index, checkItem.name)" :name="checkItem.name">
                {{ checkItem.description }}
            </ChecklistItem>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

import { VueCheckbox  } from 'vue-material-checkbox';

import ChecklistItem from './ChecklistItem.vue';
import ChecklistHeader from './ChecklistHeader.vue';

@Component({
    components: {
        VueCheckbox,
        ChecklistItem,
        ChecklistHeader,
    },
    methods: {
        makeId: (index, name) => {
            return `chk-${index}-${name.match(/\b(\w)/g).splice(0, 12).join('')}`;
        },
    },
})
export default class Checklist extends Vue {
    @Prop() private theList!: [object];
    @Prop() private title?: string;
    @Prop() private showCounter?: boolean;
}
</script>

<style scoped lang="scss">

    .checklist{
        max-width: 800px;
        margin: 0 auto;
        padding: 1em;

        background: #FFF;
        box-shadow: 
            0 -1px 0 #e0e0e0, 
            0 0 2px rgba(0,0,0,.12), 
            0 2px 4px rgba(0,0,0,.24);
        
        .item{
            border-bottom: 1px solid #d0d0d0;
            &:last-child { border-bottom: none; }
        }
    }

</style>

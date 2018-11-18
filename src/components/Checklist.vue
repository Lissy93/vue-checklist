<template>
    <div class="checklist">
        <ChecklistHeader/>
        <div v-for="(checkItem, index) in theList" :key="checkItem.name" :name="`chk-${index}`" class="item">
            <ChecklistItem :id="`chk-${index}`" :name="checkItem.name">
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
    data: () => {
        return {
            checkedItems: [],
        };
    },
})
export default class Checklist extends Vue {
    @Prop() private theList!: [object];
}
</script>

<style scoped lang="scss">

    .checklist{
        max-width: 800px;
        margin: 0 auto;
        padding: 1em;

        background: #FFF;
        
        .item{
            border-bottom: 1px solid #d0d0d0;
            &:last-child { border-bottom: none; }
        }
    }

</style>

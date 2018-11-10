<template>
    <div class="checklist">
        <div v-for="(checkItem, index) in theList" :key="checkItem.name" :name="`chk-${index}`">
            <ChecklistItem :id="`chk-${index}`" :name="checkItem.name" :details="checkItem.description"/>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

import { VueCheckbox  } from 'vue-material-checkbox';

import ChecklistItem from './ChecklistItem.vue';

@Component({
    components: {
        VueCheckbox,
        ChecklistItem,
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
    }

</style>

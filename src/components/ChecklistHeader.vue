<template>
    <div class="checklist-header">
        <div>{{ checker }}</div>
        <div>{{ shortName }}</div>
        <div>{{ details }}</div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({
    props: {
         checker: {
            type: String,
            default: () => {
                return 'Done';
            }
        },
         shortName: {
            type: String,
            default: () => {
                return 'Name';
            }
        },
         details: {
            type: String,
            default: () => {
                return 'Details';
            }
        },
    },
})
export default class ChecklistHeader extends Vue {}
</script>

<style scoped lang="scss">
    
</style>

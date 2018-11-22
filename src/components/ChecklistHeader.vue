<template>
    <div class="checklist-header">
        <div class="header-item" :v-if="title">{{ title }}</div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({})
export default class ChecklistHeader extends Vue {
        @Prop() private title?: string;
}
</script>

<style scoped lang="scss">

.checklist-header{
    align-items: stretch;
    display: flex;
    justify-content: space-between;
    padding: 0;
    margin: 0;
    width: 100%;
    padding: 0.5em;
    text-align: left;
    font-weight: bold;
    font-size: 1.6rem;
}

.counter{
    width: 120px;
    font-size: 1rem;
    color: #d0d0d0;
    font-weight: normal;
}
    
</style>

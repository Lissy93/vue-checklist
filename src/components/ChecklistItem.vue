<template>
    <div class="inner-item" v-bind:class="{ checked: checked }">
        <VueCheckbox  
            :value="id" 
            v-model="checked" 
            class="item-checkbox">
                {{ name }}
        </VueCheckbox>
        <div class="item-details">
            <slot></slot>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { VueCheckbox  } from 'vue-material-checkbox';

@Component({
    components: {
        VueCheckbox,
    },
    methods: {
        initSeshStorage: () => {
            if (!localStorage.checkedItems) {
                localStorage.checkedItems = JSON.stringify({});
            }
        },
        readFromStorage(id: string) {
            (this as any).initSeshStorage();
            const seshStorage = JSON.parse(localStorage.checkedItems) || {};
            return seshStorage[id] || false;
        },
        storeInStorage(id: string, value: boolean) {
            (this as any).initSeshStorage();
            const seshStorage = JSON.parse(localStorage.checkedItems) || {};
            seshStorage[id] = value;
            localStorage.checkedItems = JSON.stringify(seshStorage);
        },
    },
    data() {
        return {
            isChecked: false,
        };
    },
    computed: {
        checked: {
            get() {
                this.$data.isChecked = (this as any).readFromStorage((this as any).id);
                return this.$data.isChecked;
            },
            set(val) {
                this.$data.isChecked = val;
                (this as any).storeInStorage((this as any).id, val);
            },
            },
    },

})
export default class ChecklistItem extends Vue {
    @Prop() private id!: string;
    @Prop() private name!: string;
    @Prop() private details!: string;
}
</script>

<style lang="scss">

    @media only screen and (max-width: 768px) {
        .inner-item {
            display: flex;
            flex-direction: column;

            .item-checkbox {
                margin-left: auto;
                margin-right: auto;
                text-align: center;
            }

            .item-checkbox .checkbox-group{
                display: none;
            }

            .item-details {
                margin : 0 auto;
            }
        }

    }

    .inner-item{
        display: flex;
        padding: 0 0 0 0.5em;
        margin: 0;
        width: 100%;

        &.checked{
            background: #80808017;
        }

        .item-checkbox{
            max-height: 60px;
            min-width: 180px;
            width: 150px;
        }

        .item-details{
            flex-grow: 1;
            display: flex;
            justify-content: center;
            flex-direction: column;
            text-align: left;
        }

        .checkbox-container.item-checkbox > label {
            display: flex;
            justify-content: center;
            flex-direction: column;
            text-align: left;
            font-weight: bold;
            font-size: 1.2rem;
        }

        .checkbox-container .checkbox-group{
            height: 20px;
            width: 20px;
            border-radius: 20px;
        }

        .checkbox-container .checkbox-group:after{
            width: 6px;
            height: 12px;
            top: 1px;
            left: 5px;
        }

        .checkbox-container.checkbox-active .checkbox-group {
            background-color: #ee6e73;
            border-color: #ee6e73;
        }
    }
</style>

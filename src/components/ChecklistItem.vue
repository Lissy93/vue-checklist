<template>
    <div class="item checked">
        <VueCheckbox  
            :value="id" 
            v-model="checked" 
            @change="checkboxChanged"
            class="item-checkbox">
                {{ name }}
        </VueCheckbox>
        <div class="item-details">{{ details }}</div>
        <span>{{ checked }}</span>
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
  },
  isChecked: () => {
      return true;
  },

}


@Component({
    components: {
        VueCheckbox,
    },
    mounted() {

    },
    methods: {
        checkboxChanged: function (newVal) {

        },
        initSeshStorage: () => {
            if (!localStorage.checkedItems) {
                localStorage.checkedItems = JSON.stringify({});
            }
        },
        readFromStorage: function (id: string) {
            (this as any).initSeshStorage();
            const seshStorage = JSON.parse(localStorage.checkedItems) || {};
            return seshStorage[id] || false;
        },
        storeInStorage: function (id: string, value: boolean) {
            (this as any).initSeshStorage();
            const seshStorage = JSON.parse(localStorage.checkedItems) || {};
            seshStorage[id] = value;
            localStorage.checkedItems = JSON.stringify(seshStorage);
        },
    },
    data: function () {
        return {
            isChecked: false,
        }
    },
    computed: {
        checked: {
            get: function() {
                this.$data.isChecked = (this as any).readFromStorage((this as any).id);
                return this.$data.isChecked;
            },
            set: function(val) {
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
    .item{
        display: flex;
        padding: 0.5em 1em;
        margin: 0.5em 0;

        &.checked{
            background: #80808017;
        }

        .item-checkbox{
            width: 250px;
        }

        .item-details{
            flex-grow: 1;
            display: flex;
            justify-content: center;
            flex-direction: column;
            text-align: center;
        }

        .checkbox-container .checkbox-group{
            height: 40px;
            width: 40px;
            border-radius: 20px;
        }

        .checkbox-container .checkbox-group:after{
            width: 12px;
            height: 23px;
            top: 2px;
            left: 10px;
        }

        .checkbox-container.checkbox-active .checkbox-group {
            background-color: #ee6e73;
            border-color: #ee6e73;
        }
    }
</style>

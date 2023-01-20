<template>
    <div>
        <select v-model="selected">
        <option v-for="(value, key) in Type" :value="value" :key="key">
            {{ key }}
        </option>
            
        </select>
        </div>
</template>
<script>
    export default {
        name: "TypeMapSelector",
        props: {
            selectedTypeMap: {
                type: String,
                default: "k"
            }
        },
        emits: ["TypeMapChange"],
        data() {
            return {
                Type : {Satelite: 'k',
                Normal: 'm',
                Terrain: 'p',
                Hybrid: 'h',},
                selected: ""
            }
        },
        mounted() {
            this.selected = this.selectedTypeMap;
        },
        watch: {
            selectedTypeMap: function(newTypeMap) {
                this.selected = newTypeMap;
            },
            selected: function(newTypeMap) {
                this.$emit("TypeMapChange", newTypeMap);
            }
        }
    }
</script>
<template>
    <div class="selection-wrapper">
        <v-progress-circular 
        v-if="isLoading"
        indeterminate></v-progress-circular>
        <input
            class="input-field"
            type="text"
            :value="search"
            @input="$emit('update:search', $event.target.value)"
            :placeholder="placeholder"
        >
        <v-divider></v-divider>
        <v-expand-transition>
            <v-list 
                class="suggestion-list"
                v-if="isOpen"
            >
                <v-list-item v-for="(item, i) in items" :key="i"
                    @click="$emit('update:selection', item); $emit('update:search', item)"
                >
                    <v-list-item-title>{{item}}</v-list-item-title>
                </v-list-item>
            </v-list>
        </v-expand-transition>
    </div>
</template>

<script>
export default {
    props: {
        search: {
            type: String,
            default: '',
            required: true,
        },
        selection: {
            type: String,
            default: '',
            required: true,
        },
        items: {
            type: Array,
            default: () => [],
            required: false,
        },
        isLoading: {
            type: Boolean,
            default: false,
            required: false,
        },
        placeholder: {
            type: String,
            default: '',
            required: false,
        },
    },
    computed: {
        isOpen() {
            return this.items.length > 0 && this.selection != this.search;
        },
    }
}
</script>

<style scoped>
.selection-wrapper {
    position: relative;
}
.input-field {
    width: 100%;
    border: 1px solid lightgray;
    outline: none;
    padding: 5px 10px;
}

.suggestion-list {
    border: 1px solid gray;
    position: absolute;
    width: 100%;
}
</style>
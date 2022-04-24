<template>
    <v-progress-circular 
        v-if="isLoading"
        indeterminate></v-progress-circular>
    <input
        type="text"
        style="border: 1px solid black"
        :value="search"
        @input="$emit('update:search', $event.target.value)"
    >
    <v-divider></v-divider>
    <v-expand-transition>
        <v-list v-if="isOpen">
            <v-list-item v-for="(item, i) in items" :key="i"
                @click="$emit('update:selection', item); $emit('update:search', item)"
            >
                <v-list-item-title>{{item}}</v-list-item-title>
            </v-list-item>
        </v-list>
    </v-expand-transition>
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
        }
    },
    computed: {
        isOpen() {
            return this.items.length > 0 && this.selection != this.search;
        },
    }
}
</script>

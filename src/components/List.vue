<template>
    <div class="list">
        <div class="list_header">
            {{ airports.length }} {{ placeholderText }} listed
        </div>
    
        <div class="list_content">
            <ul>
                <ListItem 
                    :airport="airport" 
                    v-for="(airport, index) in airports" 
                    :key="airport.index"
                    @deleteAirport="deleteAirport(index)" />
            </ul>
        </div>
    </div>
</template>

<script>
import ListItem from './ListItem.vue';

export default {
    props: ["airports"],
    components: {
		ListItem
    },
    computed: {
        placeholderText() {
            if (this.airports.length == 1) {
                return "Airport"
            } else {
                return "Airports"
            }
        }
    },
    methods: {
        deleteAirport(index) {
            this.$emit("delete-airport", index);
        }
    }
}
</script>

<style scoped>
.list {
    width: 100%;

    display: flex;
    flex-direction: column;
    gap: 10px
}

.list_header {
    height: 60px;
    padding-left: 34px;
    padding-right: 34px;
    
    display: flex;
    align-items: center;
    
    background-color: var(--dark_grey);
    color: var(--light_grey);
}

.list_content {    
    width: 800px;
    height: 380px;
    overflow-y: scroll;

    gap: 10px;
}

ul {    
    display: flex;
    flex-direction: column;
    gap: 10px;
}
</style>
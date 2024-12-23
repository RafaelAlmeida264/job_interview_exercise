<template>
    <li v-on:mouseover="showActions=true" v-on:mouseleave="showActions=false" v-on:keydown.d="deleteWithKey">
        {{ airport.iata }}, {{ airport.name }}

        <div class="actions" v-show=showActions>
            <font-awesome-icon class="action" icon="edit" @click="openEditPopup"/>
            <font-awesome-icon class="action" icon="trash" @click="openCloseDeletePopup" />
        </div>
    </li>

    <DeletePopup v-show=showDeletePopup @close-delete-popup="openCloseDeletePopup" @confirm-delete-entry="confirmDelete" />

    <Form 
        v-show="showEditPopup" 
        popupTitle="Update Airport Data" 
        :airportToEdit="airport" 
        :isUpdateForm=true
        @toggle-popup="openEditPopup" 
        @update-airport="updateAirportData($event)" />
</template>

<script>
import DeletePopup from './DeletePopup.vue';
import Form from './Form.vue';

export default {
    props: ["airport"],
    emits: ["deleteAirport"],
    components: {
        DeletePopup,
        Form
    },
    data() {
        return {
            showDeletePopup: false,
            showActions: false,
            showEditPopup: false,
        }
    },
    methods: {
        openCloseDeletePopup() {
			this.showDeletePopup = !this.showDeletePopup;
		},
        
        confirmDelete() {
            this.$emit('deleteAirport');
        },
        
        openEditPopup() {
            this.showEditPopup = !this.showEditPopup;
        },

        updateAirportData(newData) {
            this.airport.iata = newData.iata;
            this.airport.name = newData.name;
        },

        deleteWithKey() {
            console.log("You pressed D")
            if (this.showActions) {
                this.openCloseDeletePopup();
            }
        }
    }
}
</script>

<style scoped>
li {
    background-color: var(--light_grey);
    
    height: 50px;
    padding-left: 34px;
    padding-right: 34px;
    border-radius: 5px;

    display: flex;
    align-items: center;
    justify-content: space-between;
    
    color: var(--dark_text);
    font-weight: var(--font_weight_medium);
    text-decoration: none;
}
li:hover {
    background-color: var(--grey);
    color: var(--light_grey);
}

.actions .action {
    padding: 10px;
    font-size: 18px;
    border-radius: 5px;
    cursor: pointer;
}
.actions .action:hover {
    background-color: var(--white);
    color: var(--dark_grey);
}
.actions .action:first-child {
    margin-right: 10px;
}

input {
    appearance: none;
    border: none;
    outline: none;
    background: none;
    cursor: initial;
}
</style>
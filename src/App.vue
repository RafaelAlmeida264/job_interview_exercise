<template>
<body>
    <main>
        <Button
            label="Insert New Airport"
            :hasIcon=true
            @click="openCloseFormPopup" />
        
        <List :airports="airportsList" @delete-airport="deleteAnAirport($event)" />
        
        <!-- Aditional Feature -->
        <!-- <Feedback class="feedbackComponent" /> -->
    </main>

    <Form
        popupTitle="Insert New Airport"
        v-show=showPopupForm
        @toggle-popup="openCloseFormPopup" @add-new-airport="addNewAirport($event)" />
</body>
</template>
    
<script>
import Button from './components/Button.vue';
import List from './components/List.vue';
import Form from "./components/Form.vue";
    
// Aditional Feature
import Feedback from './components/Feedback.vue';
    
export default {
    data() {
        return {
            showPopupForm: false,
            airportsList: [],
        }
    },
    components: {
        Button,
        List,
        Form,
    
        // Aditional Feature
        Feedback
    },
    computed: {
        getAirportsFromLS() {
            return JSON.parse(localStorage.getItem("airports-list") || "[]");
        },
    },
    watch: {
        airportsList: {
            handler(newAirport) {
                localStorage.setItem("airports-list", JSON.stringify(newAirport));
            }, deep: true,
        },
    },
    methods: {
        openCloseFormPopup() {
            this.showPopupForm = !this.showPopupForm;
        },
    
        addNewAirport(newAirportData) {
            this.airportsList.push({
                iata: newAirportData.iata,
                name: newAirportData.name
            });
        },
            
        deleteAnAirport(index) {
            this.airportsList.splice(index, 1);
            }
    },
    created() {
        this.airportsList = this.getAirportsFromLS;
    }
}
</script>
    
<style scoped>
body {
    width: 100%;
    height: 100vh;
    
    display: flex;
    align-items: center;
    justify-content: center;
}
    
main {
    display: flex;
    flex-direction: column;
    gap: 30px;
}
    
Button {
    align-self: flex-end;
}
    
/* Aditional Feature */
.feedbackComponent {
    align-self: center;
}
</style>
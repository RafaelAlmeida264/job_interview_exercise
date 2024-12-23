<template>
    <div class="popup_screen">
        <div class="popup">
            <div class="popup_header">
                {{ popupTitle }}
            </div>
            
            <form @submit.prevent="submitData">
                <div class="popup_body">
                    <div class="airport_form">
                        <div class="iata_box">
                            <label for="aIata">IATA</label>
                            <input v-model="airportIata" id="aIata" type="text" placeholder="_ _ _" />
                        </div>

                        <div class="name_box">
                            <label for="aName">Airport Name</label>
                            <input v-model="airportName" id="aName" type="text" placeholder="Insert name" />
                        </div>
                    </div>
    
                    <div class="listOfMessages">
                        <i class="error_message" v-show="iataAndNameRequired">
                            <font-awesome-icon icon="circle-exclamation"/>
                            {{ feedback_error_bothRequired }}
                        </i>
    
                        <i class="error_message" v-show="iataIncorrectNrChars">
                            <font-awesome-icon icon="circle-exclamation"/>
                            {{ feedback_error_nrChars }}
                        </i>
    
                        <i class="error_message" v-show="iataNotOnlyAlphaChars">
                            <font-awesome-icon icon="circle-exclamation"/>
                            {{ feedback_error_alphaChars }}
                        </i>
    
                        <!-- Additional Feature: check if an airport with that IATA already exists [hardcoded "iatas"] -->
                        <i class="warning_message" v-show="iataAlreadyExists">
                            <font-awesome-icon icon="triangle-exclamation"/>
                            {{ feedback_warning_alreadyExists }}
                        </i>
                    </div>
                </div>
    
                <div class="popup_footer">
                    <Button 
                        label="Cancel"
                        class="secondary"
                        :hasIcon="false"
                        @click="closePopupForm" type="button" />
                    
                    <Button
                        label="Confirm"
                        :hasIcon=false
                        type="submit" />
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Button from './Button.vue';

export default {
    components: {
        Button
    },

    computed: {
        iataAndNameRequired() {
            if (this.firstDataCheck) {
                return !(this.airportIata && this.airportName);
            }
        },

        iataIncorrectNrChars() {
            if (this.firstDataCheck) {
                return this.airportIata.length != 3;
            }
        },

        iataNotOnlyAlphaChars() {
            if (this.firstDataCheck) {
                return !(this.regex.test(this.airportIata));
            }
        },

        // Additional Feature: check if an airport with that IATA already exists [hardcoded "iatas"]
        iataAlreadyExists() {
            if (this.airportIata != "") {
                return this.iatas.includes(this.airportIata.toUpperCase());
            }
        },
    }, 
    props: {
        popupTitle: {
            type: String,
            required: true,
        },
        airportToEdit: {
            type: Object,
            required: false,
            default: {},
        },
        isUpdateForm: {
            type: Boolean,
            required: false,
            default: false,
        }
    },
    data() {
        return {
            airportIata: "",
            airportName: "",

            // Do not show any error message until I click in the "Confirm Button"
            firstDataCheck: false,

            // Only alphabetic characters (from a-z and A-Z)
            regex: /^[A-Za-z]+$/,

            // Feedback Messages
            feedback_error_bothRequired: "Both IATA and Airport Name are required",
            feedback_error_nrChars: "IATA not accepted: it has to be 3 characters long.",
            feedback_error_alphaChars: "IATA not accepted: it can only contain alphabetic characters.",
            feedback_warning_alreadyExists: "There is already an airport with this IATA!",

            // Additional Feature: check if an airport with that IATA already exists [hardcoded "iatas"]
            iatas: [ "ABC", "BCD", "CDE" ],
        }
    },

    methods: {
        closePopupForm() {
            // Reset form data
            this.airportIata = "";
            this.airportName = "";
            this.firstDataCheck = false;

            // Close popup (send variable to parent)
            this.$emit("toggle-popup");
        },

        submitData() {
            this.firstDataCheck = true;

            // Send data if all parameters are correct
            if (this.iataIncorrectNrChars || this.iataNotOnlyAlphaChars || this.iataAndNameRequired) {
                console.log("There are some errors!")
            } else {
                // Edit data
                if (this.isUpdateForm) {
                    this.$emit("update-airport", { iata: this.airportIata.toUpperCase(), name: this.airportName });
                }

                // Add new airport
                else {
                    // Add new airport (send variable to parent)
                    this.$emit("add-new-airport", { iata: this.airportIata.toUpperCase(), name: this.airportName });
    
                    // Reset form data
                    this.airportIata = "";
                    this.airportName = "";
                    this.firstDataCheck = false;
                }
                
                // Close popup (send variable to parent)
                this.$emit("toggle-popup");
            }
        }
    }
}
</script>

<style scoped>
.popup_screen {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 10;

    background-color: rgba(0, 0, 0, 0.5);

    display: flex;
    align-items: center;
    justify-content: center;
}

.popup {
    width: 520px;

    background-color: var(--white);
    border-radius: 5px;
    box-shadow: 0px 4px 16px rgba(var(--dark_grey_rgb), 0.25);

    padding: 25px;
}

.popup,
form {
    display: flex;
    flex-direction: column;
    color: var(--dark_text);
    gap: 20px;
}

.popup_header {
    font-weight: var(--font_weight_medium);
    padding-bottom: 10px;
    border-bottom: 2px solid var(--light_grey);
}

.popup_body {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.airport_form {
    display: flex;
    gap: 20px;
}

.iata_box,
.name_box {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.iata_box {
    width: 70px;
}

.name_box {
    flex-grow: 1;
}

.iata_box label,
.name_box label {
    font-weight: var(--font_weight_medium);
}

.iata_box input,
.name_box input {
    height: 40px;
    padding-left: 10px;
    padding-right: 10px;
    font-size: 16px;
}

.iata_box input {
    text-transform: uppercase;
}

.iata_box label,
.iata_box input {
    text-align: center;
}

.listOfMessages {
    display: flex;
    flex-direction: column;
    gap: 2px;

    font-size: 14px;
}

.error_message {
    color: var(--warning_red);
}

.warning_message {
    color: var(--dark_green);
}

.popup_footer {
    display: flex;
    align-items: center;
    justify-content: end;
    gap: 12px;
}
</style>
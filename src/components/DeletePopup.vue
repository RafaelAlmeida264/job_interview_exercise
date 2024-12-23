<template>
    <div class="popup_screen" v-on:keyup.y="confirmDelete" v-on:keyup.n="cancelDelete">
        <div class="popup">
            <div class="popup_header">
                <h3>{{ popupTitle }}</h3>
            </div>
            <div class="popup_body">
                <p>{{ popupMessage }}</p>
            </div>
            <div class="popup_footer">
                <Button 
                    label="Yes"
                    class="secondary"
                    :hasIcon="false"
                    @click="confirmDelete" />
                    
                <Button
                    label="No"
                    :hasIcon=false
                    @click="cancelDelete" />
            </div>
        </div>
    </div>
</template>

<script>
import Button from './Button.vue';

export default {
    components: {
        Button
    },
    data() {
        return {
            popupTitle: "WARNING!",
            popupMessage: "Are you sure you want to delete this entry?"
        }
    },
    methods: {
        confirmDelete() {
            this.$emit("confirm-delete-entry");
            this.closePopupForm();
        },

        cancelDelete() {
            this.closePopupForm();
        },

        closePopupForm() {
            this.$emit("close-delete-popup");
        },
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
    width: 280px;

    background-color: var(--white);
    border-radius: 5px;
    box-shadow: 0px 4px 16px rgba(var(--dark_grey_rgb), 0.25);

    padding: 25px;
    text-align: center;
}

.popup_body {
    margin-top: 10px;
    margin-bottom: 10px;
}

.popup_footer {
    display: flex;
    justify-content: space-around;
}
</style>
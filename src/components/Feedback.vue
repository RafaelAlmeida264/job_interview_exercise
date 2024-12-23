<template>
    <div class="feedback">
        {{ feedbackMessageAdded }}
    </div>
</template>

<script>
export default {
    data() {
        return {
            feedbackMessageAdded: "Airport successfully added to the list",
            feedbackMessageDeleted: "Airport successfully deleted from the list",
        }
    }
}
</script>

<style scoped>
.feedback {
    width: fit-content;

    background-color: var(--light_green);
    color: var(--dark_green);

    padding: 20px 50px;
    border-radius: 10px;
    text-align: center;

    z-index: 5;
    animation: fade-in 0.5s;
}

/* Animation */
@keyframes fade-in {
    0% {
        opacity: 0;
        transform: translateY(10px);
    }

    100% {
        opacity: 1;
        transform: translateY(0px);
    }
}

@keyframes fade-out {
    0% {
        opacity: 1;
        transform: translateY(0px);
    }

    100% {
        opacity: 0;
        transform: translateY(10px);
    }
}
</style>
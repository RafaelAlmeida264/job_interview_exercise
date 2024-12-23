<template>
    <button :class=class>
        <i v-show=hasIcon>
            <font-awesome-icon :icon=icon />
        </i>
        {{ label }}
    </button>
</template>


<script>
export default {
    props: {
        class: {
            type: String,
            required: false,
            default: ""
        },
        label: {
            type: String,
            required: true,
        },
        hasIcon: {
            type: Boolean,
            required: true,
        },
        icon: {
            type: String,
            required: false,
            default: "plus"
        }
    }
}
</script>

<style scoped>
button {
    display: flex;
    align-items: center;
    gap: 10px;
    background: var(--navy_blue);
    color: var(--white);
    padding: 10px 20px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
}
button:hover {
    opacity: 0.8;
}

button.secondary {
    background: var(--white);
    border: 1px solid var(--navy_blue);
    color: var(--navy_blue);
}
button.secondary:hover {
    background: var(--light_grey);
}
</style>
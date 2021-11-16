<template>
    <transition name="shift-in" appear>
        <div class="absolute" v-show="title === selectedTab.props.title">
            <slot/>
        </div>
    </transition>
</template>

<script>
import { inject } from "vue";

export default {
    name: "Tab",
    props: {title: String},
    setup() {
        const selectedTab = inject('selectedTab')
        return {selectedTab}
    }
}
</script>

<style scoped>
.absolute {
    position: absolute;
    padding: 30px;
}
.shift-in-enter-from {
    opacity: 0;
    transform: translateX(200px);
}
.shift-in-enter-to {
    position: absolute;
    transform: translateX(0px);
}
.shift-in-enter-active {
    transition: all 0.25s ease-out;
}
.shift-in-leave-from {
    opacity: 0.0;
    transform: translateX(0px);
}
.shift-in-leave-to {
    opacity: 0;
    transform: translateX(-200px);
}
.shift-in-leave-active {
    transition: all 0.25s ease-out;
}
.shift-in-move {
    transition: all 0.25s ease-out;
}
</style>

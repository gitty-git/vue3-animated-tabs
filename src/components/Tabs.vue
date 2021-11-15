<template>
    <div>
        <div class="titles">
            <div ref="tab1" class="title" v-for="(tab, id) in tabs" :key="tab.props.title" @click="selectTab(tab, id)">
                {{ tab.props.title }}
            </div>
        </div>
        <div class="indicator" ref="indicator"></div>
        <div class="out-w" :style="{width: selectedWidth, height: selectedHeight}">
            <slot/>
        </div>

    </div>
</template>

<script>
import Tab from "./Tab";
import { ref, provide, onMounted } from 'vue'

export default {
    name: "Tabs",
    components: {Tab},
    setup(props, context) {
        const tabs = ref(context.slots.default())
        const selectedTab = ref(tabs.value[0])
        const selectedWidth = ref(selectedTab.value.props.width)
        const selectedHeight = ref(selectedTab.value.props.height)
        const indicator = ref(null)
        const tab1 = ref(0)

        const selectTab = (tab, id) => {
            selectedTab.value = tab

            selectedWidth.value = tab.props.width
            selectedHeight.value = tab.props.height

            indicator.value.style.left = `calc(calc(100% / ${tabs.value.length}) * ${id})`
        }

        onMounted(() => {
            indicator.value.style.width = `${100 / tabs.value.length}%`
        })

        provide('selectedTab', selectedTab)

        return {selectedTab, tabs, selectedWidth, selectedHeight, selectTab, indicator, tab1}
    }
}
</script>

<style scoped>
.titles {
    display: flex;
}
.title {
    width: 100%;
    text-align: center;
    cursor: pointer;
}
.indicator {
    position: fixed;
    margin-bottom: 5px;
    left: 50px;
    background: blue;
    height: 5px;
    transition: all 0.4s ease;
    //width: 20px;
}

.out-w {
    background: red;
    transition: all 0.4s ease;
//width: 100%;
}
</style>

<template>
    <div class="tags">
        <div class="tags-titles">
            <div class="titles">
                <div class="title" v-for="(tab, id) in tabs" :key="tab.props.title" @click="selectTab(tab, id)">
                    {{ tab.props.title }}
                </div>
            </div>
            <div class="indicator" ref="indicator">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="10" viewBox="0 0 133 68.222">
                    <path id="Union_1" data-name="Union 1" d="M255.056,221H222l21.755-24.862.013-.015L277.212,157.9a15,15,0,0,1,22.577,0L326.125,188h0L355,221l0,0H255.056ZM355,221h0ZM355,221Z" transform="translate(-222 -152.779)" fill="#fff"/>
                </svg>
            </div>
        </div>
        <div class="tags-body" :style="{width: selectedWidth, height: selectedHeight}">
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

        const selectTab = (tab, id) => {
            selectedTab.value = tab

            selectedWidth.value = tab.props.width
            selectedHeight.value = tab.props.height

            indicator.value.style.left = `calc(${100 / tabs.value.length}% * ${id})`
        }

        onMounted(() => {
            indicator.value.style.left = '0px'
            indicator.value.style.width = `${Math.round(100 / tabs.value.length)}%`
        })

        provide('selectedTab', selectedTab)

        return {selectedTab, tabs, selectedWidth, selectedHeight, selectTab, indicator}
    }
}
</script>

<style scoped>
.tags {
    display: flex;
    flex-flow: column;
    align-items: center;
}
.tags-titles {
    width: 50%;
    display: flex;
    flex-flow: column;
    //align-items: center;
    position: relative;
}
.titles {
    width: 100%;
    display: flex;
    justify-content: space-between;
}
.title {
    width: 100%;
    padding: 20px 0;
    text-align: center;
    cursor: pointer;
}
.indicator {
    text-align: center;
    position: absolute;
    margin-top: 50px;
    margin-bottom: 5px;
    transition: all 0.4s ease;
}
.tags-body {
    margin-top: 5px;
    background: white;
    padding: 24px;
    transition: all 0.4s ease;
    border-radius: 7px;
    box-shadow: 0 12px 25px 8px rgba(0,0,0,0.05);
}
</style>

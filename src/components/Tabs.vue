<template>
    <div class="tags" @mouseleave="tabsShowed = false">
        <div v-if="tabsShowed" class="fixed-bg" @mouseenter="tabsShowed = false"></div>
        <div class="tags-titles">
            <div class="titles" @mouseleave="preventUwnatedPopUp()">
                <div class="title" v-for="(tab, id) in tabs" :key="tab.props.title" @mouseover="selectTab(tab, id)">
                    {{ tab.props.title }}
                </div>
            </div>
            <div v-show="tabsShowed" class="indicator" ref="indicator">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="8" viewBox="0 0 133 68.222">
                    <path id="Union_1" data-name="Union 1" d="M255.056,221H222l21.755-24.862.013-.015L277.212,157.9a15,15,0,0,1,22.577,0L326.125,188h0L355,221l0,0H255.056ZM355,221h0ZM355,221Z" transform="translate(-222 -152.779)" fill="#fff"/>
                </svg>
            </div>
        </div>
<!--        <transition name="">-->
            <div v-if="tabsShowed" class="tags-body" :style="{width: selectedWidth, height: selectedHeight}">
                <slot/>
            </div>
<!--        </transition>-->
    </div>
</template>

<script>
import Tab from "./Tab";
import { ref, provide, onMounted, watchEffect } from 'vue'

export default {
    name: "Tabs",
    components: {Tab},
    setup(props, context) {
        const tabs = ref(context.slots.default())
        const selectedTab = ref(tabs.value[0])
        const selectedWidth = ref(selectedTab.value.props.width)
        const selectedHeight = ref(selectedTab.value.props.height)
        const indicator = ref(null)
        const tabsShowed = ref(false)
        const selectedTabTime = ref(0)

        // to prevent unwanted pop-ups due to fast movement of the mouse over titles
        const preventUwnatedPopUp = () => {
            if (Date.now() - selectedTabTime.value < 100) {
                tabsShowed.value = false
            }
        }

        const selectTab = (tab, id) => {
            selectedTabTime.value = Date.now()

            tabsShowed.value = true
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

        return {
            selectedTab, tabs, selectedWidth, selectedHeight,
            selectTab, indicator, tabsShowed, preventUwnatedPopUp, selectedTabTime
        }
    }
}
</script>

<style scoped>
.tags {
    display: flex;
    flex-flow: column;
    align-items: center;
}
.fixed-bg {
    width: 100%;
    height: 100%;
    position: absolute;
}
.tags-titles {
    color: white;
    font-weight: bold;
    background: gray;
    width: 20%;
    display: flex;
    flex-flow: column;
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
    cursor: default;
    z-index: 1;
}
.indicator {
    text-align: center;
    position: absolute;
    margin-top: 45px;
    transition: all 0.25s ease;
}
.tags-body {
    z-index: 1;
    width: auto;
    background: white;
    padding: 24px;
    transition: all 0.25s ease;
    border-radius: 7px;
    box-shadow: 0 12px 25px 8px rgba(0,0,0,0.05);
}
</style>

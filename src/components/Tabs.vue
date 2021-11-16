<template>
    <div class="tags" @mouseleave="tabsShowedActive">
        <div v-if="tabsShowed" class="fixed-bg" @mouseenter="tabsShowedActive"></div>
        <div class="tags-titles">
            <div class="titles" @mouseleave="onTitlesLeave">
                <div style="width: 100%;" v-for="(tab, id) in tabs" :key="tab.props.title" @mouseover="selectTab(tab, id)">
                    <a v-if="tab.props.href"  :href="tab.props.href">
                        <div class="title link" :class="{ 'active': active === id, 'opacity-5': active !== null }">
                            {{ tab.props.title }}
                        </div>
                    </a>
<!--                    <router-link v-else-if="tab.props.to" :to="tab.props.to">-->
<!--                        <div class="title link" :class="{ 'active': active === id }">-->
<!--                            {{ tab.props.title }}-->
<!--                        </div>-->
<!--                    </router-link>-->
                    <div class="title" :class="{ 'active': active === id, 'opacity-5': active !== null }" v-else>
                        {{ tab.props.title }}
                    </div>
                </div>
            </div>
            <transition name="slide-up">
            <div v-show="tabsShowed" class="indicator" ref="indicator">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="8" viewBox="0 0 133 68.222">
                    <path id="Union_1" data-name="Union 1" d="M255.056,221H222l21.755-24.862.013-.015L277.212,157.9a15,15,0,0,1,22.577,0L326.125,188h0L355,221l0,0H255.056ZM355,221h0ZM355,221Z" transform="translate(-222 -152.779)" fill="#fff"/>
                </svg>
            </div>
            </transition>
        </div>
        <transition name="fade-scale">
            <div v-show="tabsShowed" class="tags-body overflow-relative" :style="{width: selectedWidth, height: selectedHeight}">
                <slot/>
            </div>
        </transition>
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
        const active = ref(null)

        // to prevent unwanted pop-ups due to fast movement of the mouse over titles
        const onTitlesLeave = () => {
            active.value = null
            if (Date.now() - selectedTabTime.value < 100) {
                tabsShowed.value = false
            }
        }

        const tabsShowedActive = () => {
            tabsShowed.value = false
            active.value = null
        }

        const selectTab = (tab, id) => {
            active.value = id

            selectedTabTime.value = Date.now()
            if (tab.props.href || tab.props.to) {
                return tabsShowed.value = false
            }

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

        // watchEffect(() => {
        //     if (!tabsShowed.value) {
        //         active.value = null
        //     }
        // })

        provide('selectedTab', selectedTab)

        return {
            selectedTab, tabs, selectedWidth, selectedHeight, active, tabsShowedActive,
            selectTab, indicator, tabsShowed, onTitlesLeave, selectedTabTime
        }
    }
}
</script>

<style scoped>
.opacity-5 {
    opacity: 0.5;
}
.overflow-relative {
    position: relative;
    overflow: hidden;
}
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
    //background: gray;
    width: 30%;
    display: flex;
    flex-flow: column;
    position: relative;
}
.titles {
    z-index: 2;
    width: 100%;
    display: flex;
    justify-content: space-between;
}
.title {
    width: 100%;
    padding: 20px 0;
    text-align: center;
    cursor: default;
    transition: all 0.25s ease-out;
}
.active {
    opacity: 1;
    transition: all 0.25s ease-out;
}
a {
    color: white;
    text-decoration: none;
}
.link {
    cursor: pointer;
}

.indicator {
    text-align: center;
    position: absolute;
    margin-top: 45px;
    transition: all 0.25s ease-out;
    z-index: 1;
}
.tags-body {
    z-index: 1;
    width: auto;
    background: white;
    transition: all 0.25s ease;
    border-radius: 7px;
    box-shadow: 0 12px 25px 8px rgba(0,0,0,0.05);
}
.fade-scale-leave-to,
.fade-scale-enter-from {
    //transform: translateX(-200px);
    transform: scale(1.05) translateY(20px);
    opacity: 0;
}
.fade-scale-active {
    transition: all 0.16s ease;
}
.slide-up-leave-to,
.slide-up-enter-from {
    transform: scaleX(0) translateY(20px);
    opacity: 0;
}
.slide-up-enter-active {
    transition: all 0.25s ease;
}
.slide-up-leave-active {
    transition: all 0.08s ease;
}

</style>

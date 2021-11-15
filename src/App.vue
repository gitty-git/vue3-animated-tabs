<template>
    <Tabs>
        <Tab height="200px" width="20%" title="First" class="w-50">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, libero?
        </Tab>
        <Tab height="200px" width="30%" title="Second" class="w-30">
            Lorem ipsum dolor sit amet.
        </Tab>
        <Tab height="200px" width="40%" title="Third" class="w-20">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. A asperiores consectetur dicta ducimus, enim ex ipsum iste quibusdam recusandae veritatis.
        </Tab>
    </Tabs>
</template>

<script>

import Tabs from "./components/Tabs";
import Tab from "./components/Tab";
import { provide } from "vue";

export default {
    name: 'App',
    components: {Tabs, Tab},
    setup() {
    }
}
</script>

<style>
.w-20 {
    width: 50%;
}

.w-30 {
    width: 30%;
}

.w-50 {
    width: 100%;
}
</style>

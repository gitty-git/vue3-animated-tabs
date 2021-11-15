<template>
    <Tabs>
        <Tab height="300px" width="60%" title="First" class="w-50">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, libero?
        </Tab>
        <Tab height="200px" width="20%" title="Second" class="w-30">
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
}
</script>

<style>
body {
    margin: 0;
    padding: 0;
    background: gainsboro;
}
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

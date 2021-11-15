<template>
    <Tabs>
        <Tab height="300px" width="60%" title="First">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, libero?
        </Tab>
        <Tab height="200px" width="20%" title="Second">
            Lorem ipsum dolor sit amet.
        </Tab>
        <Tab height="200px" width="40%" title="Third">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. A asperiores consectetur dicta ducimus, enim ex ipsum iste quibusdam recusandae veritatis.
        </Tab>
    </Tabs>
</template>

<script>

import Tabs from "./components/Tabs";
import Tab from "./components/Tab";

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
</style>

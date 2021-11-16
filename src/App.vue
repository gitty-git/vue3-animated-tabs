<template>
    <Tabs>
        <Tab height="600px" width="40%" title="First">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus at atque consequuntur cupiditate impedit iure laboriosam magni maxime natus omnis pariatur quae quod repudiandae sint sit, soluta vero voluptatibus! Accusamus dolore earum minus modi nam porro! Architecto excepturi molestias veniam?
        </Tab>
        <Tab height="400px" width="30%" title="Second">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusantium ducimus facere impedit laborum nulla, perspiciatis quasi rem repudiandae tempore veritatis. Aperiam aut deleniti distinctio maxime!
        </Tab>
        <Tab height="300px" width="20%" title="Third">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cupiditate eum inventore nisi perferendis quaerat voluptatem.
        </Tab>
        <Tab title="Link" href="#"></Tab>
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
    background: #878787;
}
</style>

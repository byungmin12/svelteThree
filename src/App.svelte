<script lang="ts">
    import * as THREE from 'three';
    import { FontLoader } from 'three/examples/jsm/loaders/FontLoader.js';
    import DefaultBox from "./components/DefaultBox.svelte";
    import Line from "./components/Line.svelte"
    import Text from "./components/Text.svelte"
    import LoaderGltf from "./components/LoaderGltf.svelte";
</script>

<main>
    <DefaultBox />
    <Line />
    <Text />
    <LoaderGltf />
</main>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }


    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
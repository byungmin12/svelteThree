<script lang="ts">
    import * as THREE from 'three';
    import { FontLoader } from 'three/examples/jsm/loaders/FontLoader.js';
    // export let name: string;
    // const renderer = new THREE.WebGLRenderer();
    // renderer.setSize( window.innerWidth, window.innerHeight );
    // document.body.appendChild( renderer.domElement );
    //
    // const camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 1, 500 );
    // camera.position.set( 0, 0, 100 );
    //
    // const scene = new THREE.Scene();

    /*
    * 여기는 Qube 생성에 대한 코드입니다.
    * */
    // const geometry = new THREE.BoxGeometry(1, 1, 1);
    // const material = new THREE.MeshBasicMaterial({color: 0x00ff00});
    // const cube = new THREE.Mesh(geometry, material);
    // const cubeTwo = new THREE.Mesh(geometry, material);


    // camera.position.z = 5;
    //
    // function animate() {
    //     requestAnimationFrame(animate);
    //
    //     cube.rotation.x += 0.01;
    //     cube.rotation.y += 0.01;
    //
    //     renderer.render(scene, camera);
    // };
    //
    // animate();

    /*
    * 여기서부터는 line을 그리는 예제입니다.
    * */
    // 여기는 재질을 그리는 부분입니다
    // const material = new THREE.LineBasicMaterial({color:"red"})
    // //라인은 버텍스가 필요하다고 합니다
    // const points = []
    // points.push( new THREE.Vector3( - 15, 0, 0 ) );
    // points.push( new THREE.Vector3( 0, 15, 0 ) );
    // points.push( new THREE.Vector3( 15, 0, 0 ) );
    // const geometry = new THREE.BufferGeometry().setFromPoints(points)
    // // 이제 그려줍니다.
    // const line = new THREE.Line(geometry,material)
    // scene에 그린 라인을 추가합니다.
    // scene.add(line)
    // renderer.render(scene,camera)

    /*
    * text를 추가합니다.
    * */

    let camera, scene, renderer;
    init()
    function init(){
        camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 1, 10000 );
        camera.position.set( 0, - 400, 600 );

        scene = new THREE.Scene();
        scene.background = new THREE.Color( 0xf0f0f0 );

        const loader = new FontLoader();

        loader.load('fonts/helvetiker_regular.typeface.json', function (font){
            const color = 0x006699;

            const matDark = new THREE.LineBasicMaterial({
                color ,
                side : THREE.DoubleSide
            })

            const matLite = new THREE.MeshBasicMaterial({
                color,
                transparent: true,
                opacity: 0.4,
                side: THREE.DoubleSide
            })

            const message = '   Three.js\nSimple text.'

            const shapes = font.generateShapes(message, 100)

            const geometry = new THREE.ShapeGeometry(shapes)

            geometry.computeBoundingBox()

            const xMid = -0.5 * (geometry.boundingBox.max.x - geometry.boundingBox.min.x)

            geometry.translate(xMid, 0, 0)

            const holeShapes = []
            const shapesLength = shapes.length
            for(let i=0 ; i< shapesLength ; i ++){
                const shape = shapes[i]
                const holeLength = shape.holes.length
                if(shape.holes && holeLength >0 ){
                    for(let j =0 ; j<holeLength; j++){
                        const hole = shape.holes[j]
                        holeShapes.push(hole)
                    }
                }
            }

            shapes.push(...shapes, ...holeShapes)

            const lineText = new THREE.Object3D()

            for(let i =0 ; i< shapes.length; i++){
                const shape = shapes[i]
                const points = shape.getPoints()
                const geometry = new THREE.BufferGeometry().setFromPoints(points)

                geometry.translate(xMid,0,0)

                const lineMesh = new THREE.Line(geometry, matDark)
                lineText.add(lineText)
            }

            scene.add(lineText)
            render()
        },()=>{},()=>{})

        renderer = new THREE.WebGLRenderer({antialias: true})
        renderer.setPixelRatio(window.devicePixelRatio)
        renderer.setSize(window.innerWidth,window.innerHeight)
        document.body.appendChild(renderer.domElement)

    }

    function render(){
        renderer.render(scene, camera)
    }
</script>

<main>

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
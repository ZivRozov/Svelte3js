<div class='bg-slate-100 w-full h-full' bind:this={canvas}></div>
<script>
import * as THREE from 'three';
let canvas;
let animating = false;
const textureLoader = new THREE.TextureLoader();
const matcapTexture = textureLoader.load('/matcap0.png');
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
scene.addEventListener('pointerdown',()=>{
    console.log('hello');
})
const renderer = new THREE.WebGLRenderer({canvas, alpha:true});
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshMatcapMaterial();
material.matcap = matcapTexture;
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );

var geo = new THREE.CylinderGeometry(0.2, 0.1, 3, 10, 10);
var mesh = new THREE.Mesh(geo, new THREE.MeshNormalMaterial());
mesh.position.set(1.3,-1,0);
mesh.rotation.set(0.9,0,0);
scene.add(mesh);

const directionalLight = new THREE.DirectionalLight( 0xffffff, 0.5 );
scene.add( directionalLight );

camera.position.z = 5;

function animate() {
	requestAnimationFrame( animate );
	renderer.render( scene, camera );
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    if(animating) {
        mesh.rotation.x+= 0.1;
    }
}
animate();
</script>
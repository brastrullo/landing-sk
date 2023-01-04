<script>
	import { onMount } from 'svelte'
	import { browser } from '$app/environment'
	import * as THREE from 'three'
	// import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

	export let scrollY

	onMount(async () => {
	  const dat = await import('dat.gui');
	  if (browser) {
	    let sizes = {
	      width: window.innerWidth,
	      height: window.innerHeight,
	    }
	    const scene = new THREE.Scene();
	    // scene.background = new THREE.Color( 0xffffff );
	    const renderer = new THREE.WebGLRenderer({ alpha: true });
	    renderer.setSize( sizes.width, sizes.height );
	    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
	    document.querySelector('#threejs-scene')?.appendChild( renderer.domElement );

	    const camera = new THREE.PerspectiveCamera( 75, window.innerWidth/ window.innerHeight, 0.1, 1000 );
	    // const orbit = new OrbitControls(camera, renderer.domElement);
	    // orbit.enableDamping = true
	    // const axesHelper = new THREE.AxesHelper(5);
	    // scene.add(axesHelper);

	    camera.position.set(0, -1.25, 10);

	    const cube = new THREE.Mesh(
	      new THREE.BoxGeometry( 1, 1, 1 ),
	      new THREE.MeshNormalMaterial()
	    );
	    scene.add( cube );

	    const sphere = new THREE.Mesh(
	      new THREE.SphereGeometry( 4, 50, 50 ),
	      new THREE.MeshNormalMaterial({wireframe:true})
	    );
	    scene.add(sphere);

	    /*
	    * GUI
	    */

	    // const gui = new dat.GUI({ autoPlace: false });
	    // document.querySelector('.moveGUI').appendChild(gui.domElement);

	    // const options = {
	    //   sphereColour: '#ffea00',
	    //   wireframe: true
	    // };

	    // gui.addColor(options, 'sphereColour').onChange((e) => {
	    //   sphere.material.color.set(e);
	    // });

	    // gui.add(options, 'wireframe').onChange((e) => {
	    //   sphere.material.wireframe = e;
	    // });

	    const clock = new THREE.Clock()

	    const tick = () => {
	      const elapsedTime = clock.getElapsedTime();

	      cube.rotation.x = elapsedTime * Math.PI * .3;
	      cube.rotation.y = elapsedTime * Math.PI * .7;
	      cube.rotation.z = elapsedTime * Math.PI * .05;

	      sphere.rotation.y = elapsedTime * Math.PI * .03;
	      sphere.rotation.x = (Math.cos(elapsedTime) * .05);

	      renderer.render( scene, camera );
	      // orbit.update();
	      requestAnimationFrame( tick );
	    }
	    tick();

	    window.addEventListener('resize', function() {
	      sizes = {
	        width: window.innerWidth,
	        height: window.innerHeight,
	      }
	      camera.aspect = sizes.width / sizes.height;
	      camera.updateProjectionMatrix();
	      renderer.setSize(sizes.width, sizes.height);
	      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
	    })
	  }
	});
</script>

<div class="fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
  <section id="threejs-scene">
    <div class="moveGUI absolute" />
  </section>
</div>
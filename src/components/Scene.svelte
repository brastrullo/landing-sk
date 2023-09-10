<script>
	import { onMount } from 'svelte'
	import { browser } from '$app/environment'
	import * as THREE from 'three'
	import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
	import { DRACOLoader } from 'three/examples/jsm/loaders/DRACOLoader.js';
	import * as SC from 'svelte-cubed'
	export let scrollY

	const dracoLoader = new DRACOLoader()
	const loader = new GLTFLoader()
	dracoLoader.setDecoderPath('https://www.gstatic.com/draco/v1/decoders/')
	dracoLoader.setDecoderConfig({ type: 'js' })
	loader.setDRACOLoader(dracoLoader)

	let model;
	let texture;

	let sizes = {}
	let cubeRotationX = 0
	let cubeRotationY = 0
	let cubeRotationZ = 0

	let sphereRotationX = 0
	let sphereRotationY = 0
	let devicePixelRatio = 1

	const clock = new THREE.Clock()

	onMount(async () => {
		if (browser) {
			sizes = {
				width: window.innerWidth,
				height: window.innerHeight
			}
			window.addEventListener('resize', function () {
				sizes = {
					width: window.innerWidth,
					height: window.innerHeight
				}
			})

			devicePixelRatio = window.devicePixelRatio
			const image = new Image()
			texture = new THREE.Texture(image)
			image.onload = () => {
				texture.needsUpdate = true
			}
			image.src = 'bird/textures/bird.png'
			loadGLTF().then(_model => model = _model);
		}
	})
	SC.onFrame(() => {
		const elapsedTime = clock.getElapsedTime()
		cubeRotationX = elapsedTime * Math.PI * 0.3
		cubeRotationY = elapsedTime * Math.PI * 0.7
		cubeRotationZ = elapsedTime * Math.PI * 0.05

		sphereRotationX = elapsedTime * Math.PI * 0.1
		sphereRotationY = Math.cos(elapsedTime) * 0.1
	})
	function loadGLTF() {
		const model = loader.loadAsync("bird/source/bird.glb")
		return model
	}
</script>

<SC.Canvas
	antialias
	alpha={true}
	width={sizes.width}
	height={sizes.height}
	pixelRatio={Math.min(devicePixelRatio, 2)}
>
	{#if model}
		<SC.Primitive
			object={model.scene}
		/>
	{/if}
	<!-- <SC.Mesh
		geometry={new THREE.SphereGeometry(7, 50, 50)}
		material={new THREE.MeshNormalMaterial({ wireframe: true })}
		rotation={[sphereRotationY, sphereRotationX, 0]}
	/>
	<SC.Mesh
		geometry={new THREE.BoxGeometry()}
		material={new THREE.MeshNormalMaterial()}
		rotation={[cubeRotationX, cubeRotationY, cubeRotationZ]}
	/> -->
	<SC.PerspectiveCamera position={[1000 / scrollY * 1.5, -10, 20]} />
</SC.Canvas>



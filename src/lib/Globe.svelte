<script>
  import { onMount } from 'svelte';
  import {
    AmbientLight,
    DirectionalLight,
    Group,
    Mesh,
    MeshBasicMaterial,
    MeshStandardMaterial,
    PerspectiveCamera,
    QuadraticBezierCurve3,
    Scene,
    SphereGeometry,
    TubeGeometry,
    Vector3,
    WebGLRenderer
  } from 'three';

  let host;

  const connections = [
    [-61.55, 16.25, 2.35, 48.85],
    [-61.55, 16.25, -73.56, 45.5],
    [-61.55, 16.25, -4.03, 5.35],
    [-61.55, 16.25, 6.13, 49.61],
    [2.35, 48.85, -118.24, 34.05]
  ];

  function toVector(lon, lat, radius = 1) {
    const phi = (90 - lat) * (Math.PI / 180);
    const theta = (lon + 180) * (Math.PI / 180);

    return new Vector3(
      -radius * Math.sin(phi) * Math.cos(theta),
      radius * Math.cos(phi),
      radius * Math.sin(phi) * Math.sin(theta)
    );
  }

  function makeArc(start, end) {
    const midpoint = start.clone().add(end).normalize().multiplyScalar(1.34);
    const curve = new QuadraticBezierCurve3(start, midpoint, end);
    const geometry = new TubeGeometry(curve, 36, 0.004, 8, false);
    const material = new MeshBasicMaterial({
      color: 0xffba20,
      transparent: true,
      opacity: 0.72
    });

    return new Mesh(geometry, material);
  }

  onMount(() => {
    const reducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
    const scene = new Scene();
    const camera = new PerspectiveCamera(38, 1, 0.1, 100);
    const renderer = new WebGLRenderer({ alpha: true, antialias: true });
    const group = new Group();
    const arcs = new Group();
    let frameId = 0;

    camera.position.set(0, 0, 3.3);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    host.appendChild(renderer.domElement);

    const sphere = new Mesh(
      new SphereGeometry(1, 64, 64),
      new MeshStandardMaterial({
        color: 0x14a45c,
        roughness: 0.55,
        metalness: 0.08,
        transparent: true,
        opacity: 0.92
      })
    );
    group.add(sphere);

    const wire = new Mesh(
      new SphereGeometry(1.012, 32, 32),
      new MeshBasicMaterial({
        color: 0xfdfff5,
        transparent: true,
        opacity: 0.28,
        wireframe: true
      })
    );
    group.add(wire);

    const nodeMaterial = new MeshBasicMaterial({ color: 0xffec3d });
    const nodeGeometry = new SphereGeometry(0.023, 14, 14);

    for (const [fromLon, fromLat, toLon, toLat] of connections) {
      const start = toVector(fromLon, fromLat, 1.035);
      const end = toVector(toLon, toLat, 1.035);
      const startNode = new Mesh(nodeGeometry, nodeMaterial);
      const endNode = new Mesh(nodeGeometry, nodeMaterial);

      startNode.position.copy(start);
      endNode.position.copy(end);
      arcs.add(makeArc(start, end));
      arcs.add(startNode);
      arcs.add(endNode);
    }

    group.add(arcs);
    scene.add(group);

    scene.add(new AmbientLight(0xfdfff5, 1.15));
    const light = new DirectionalLight(0xfdfff5, 2);
    light.position.set(2, 1.6, 3);
    scene.add(light);

    function resize() {
      const rect = host.getBoundingClientRect();
      const size = Math.max(1, Math.min(rect.width, rect.height || rect.width));
      renderer.setSize(size, size, false);
      camera.aspect = 1;
      camera.updateProjectionMatrix();
    }

    const observer = new ResizeObserver(resize);
    observer.observe(host);
    resize();

    function render() {
      if (!reducedMotion) {
        group.rotation.y += 0.0022;
        arcs.rotation.y -= 0.0008;
      }
      renderer.render(scene, camera);
      frameId = window.requestAnimationFrame(render);
    }

    render();

    return () => {
      window.cancelAnimationFrame(frameId);
      observer.disconnect();
      renderer.dispose();
      sphere.geometry.dispose();
      sphere.material.dispose();
      wire.geometry.dispose();
      wire.material.dispose();
      nodeGeometry.dispose();
      nodeMaterial.dispose();
      arcs.traverse((child) => {
        child.geometry?.dispose();
        child.material?.dispose();
      });
      renderer.domElement.remove();
    };
  });
</script>

<div class="globe-stage" bind:this={host} aria-hidden="true"></div>

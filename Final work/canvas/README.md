# DAT505-GitHub
## B161006063  Shu Ding ##
  * I was inspired by an astronomical book about Saturn, which I think is the most mysterious and romantic of the eight planets. Saturn's beautiful rings are actually tiny gravels. They buzz around Saturn. Saturn's dry and cold environment, described in classical astrology, seems to form a centripetal force that controls the rings by keeping them at a certain distance and at a certain height, producing different syllables, like celestial music. So I want to use this software to make a Saturn-like model.

```javascript
var container = document.getElementById("container");
var width = container.clientWidth;
var height = container.clientHeight;
var aspect = width / height;
var renderer = new THREE.WebGLRenderer();
renderer.setSize(width, height);
container.appendChild(renderer.domElement);

var scene = new THREE.Scene();

var camera = new THREE.PerspectiveCamera(50, aspect, 0.1, 1000);
camera.position.z = 500

system = new THREE.Group(); // planetary system

  ```
  * Considering that the whole space is immeasurable and my level is limited, I chose black as the background color and some white dots represent other plants. So it is simple and clear, and it can highlight my main works very well.The next step is create a scene, renderer, camera, and set the camera's position on the z-axis.

```javascript
  new THREE.AmbientLight(0xFFFFFF, 0.2)
);

var light = new THREE.DirectionalLight(0xFFFFFF, 2.5);
light.position.set(1500, 2500, 0);
scene.add(light);
```

* Create an ambient light and parallel light and set its coordinate position.

```javascript
var material = new THREE.MeshLambertMaterial({
  color: 0x0C2D4D
});

var planet = new THREE.Mesh(
  new THREE.IcosahedronGeometry(100, 3),
  material
);

for (var i = 0; i < planet.geometry.vertices.length; i++)
  planet.geometry.vertices[i].multiplyScalar(
    Math.random() * 0.05 + 0.95
  );

planet.geometry.computeFlatVertexNormals();
system.add(planet);

var asteroids = new THREE.Group();

for (var p = 0; p < Math.PI * 2; p = p + Math.random() * 0.15) {
  var asteroid = new THREE.Mesh(
    new THREE.IcosahedronGeometry(8, 0),
    material
  );

  var size = Math.random() * 0.5;
  for (var i = 0; i < asteroid.geometry.vertices.length; i++)
    asteroid.geometry.vertices[i].multiplyScalar(
      Math.random() * 0.5 + size
    );

  rand = Math.random() * 60 - 30;
  asteroid.position.set(200 * Math.sin(p) + rand, rand, 200 * Math.cos(p) + rand);

  asteroid.geometry.computeFlatVertexNormals();
  asteroids.add(asteroid);
}

system.add(asteroids);
```
* This step is define the material and the wealthy planet related properties.

```javascript
system.add(asteroids);

system.rotation.x = 0.1;
system.rotation.y = -.3;
system.rotation.z = -0.4;
```
* Last but not least, create an asteroid system and set the rotation of this system on the axis. I remember that one of our previous homework assignments was to change the static case material into a random rotation pattern (small color squares), so I used previous experience and similar methods (rewriting part of the code) to define an asteroid to rotate randomly according to its trajectory.

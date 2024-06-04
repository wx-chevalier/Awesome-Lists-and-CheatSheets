# Three.js CheatSheet | Three.js 入门与实践

OpenGL 是最常用的跨平台图形库；WebGL 是基于 OpenGL 设计的面向 web 的图形标准，提供了一系列 JavaScript API，通过这些 API 进行图形渲染将得以利用图形硬件从而获得较高性能。而 Three.js 是通过对 WebGL 接口的封装与简化而形成的一个易用的图形库。WebGL 门槛相对较高，需要相对较多的数学知识。虽然 WebGL 提供的是面向前端的 API，但本质上 WebGL 跟前端开发完全是两个不同的方向，知识的重叠很少。

# 基本概念

Scene 场景，即构建的三维空间。

## Camera

Camera，即选定的观察点，确定观察方向/角度等。首先我们要描述空间中的位置，Three.js 中使用采用常见的右手坐标系定位。

![image](https://user-images.githubusercontent.com/5803001/42416327-53bf587a-829e-11e8-8a09-a06a76578db1.png)

接下来要确定三维投影方式，视景体是一个几何体，只有视景体内的物体才会被我们看到，视景体之外的物体将被裁剪掉。这是为了去除不必要的运算。Three 中的相机有两种，分别是正投影相机 THREE.OrthographicCamera 和透视投影相机 THREE.PerspectiveCamera。

![image](https://user-images.githubusercontent.com/5803001/42416337-8875c978-829e-11e8-85d0-54c1194f3524.png)

正交投影与透视投影的区别如上图所示，左图是正交投影，物体发出的光平行地投射到屏幕上，远近的方块都是一样大的；右图是透视投影，近大远小，符合我们平时看东西的感觉。

![image](https://user-images.githubusercontent.com/5803001/42416347-bc035fc6-829e-11e8-8830-36f1419f322b.png)

正交投影相机的视景体是一个长方体，OrthographicCamera 的构造函数是这样的：OrthographicCamera( left, right, top, bottom, near, far )
Camera 本身可以看作是一个点，left 则表示左平面在左右方向上与 Camera 的距离。另外几个参数同理。于是六个参数分别定义了视景体六个面的位置。可以近似地认为，视景体里的物体平行投影到近平面上，然后近平面上的图像被渲染到屏幕上。

![image](https://user-images.githubusercontent.com/5803001/42416362-dc512808-829e-11e8-8d45-670d4a3e690b.png)

透视投影相机的视景体是个四棱台，它的构造函数是这样的：PerspectiveCamera( fov, aspect, near, far )
fov 对应着图中的视角，是上下两面的夹角。aspect 是近平面的宽高比。在加上近平面距离 near，远平面距离 far，就可以唯一确定这个视景体了。透视投影相机很符合我们通常的看东西的感觉，因此大多数情况下我们都是用透视投影相机展示 3D 效果。

## Objects

Three 中供显示的物体有很多，它们都继承自 Object3D 类，这里我们主要看一下 Mesh 和 Points 两种。一条弧线是由有限个点构成的有限条线段连接得到的。线段很多时，看起来就是一条平滑的弧线了。计算机中的三维模型也是类似的，普遍的做法是用三角形组成的网格来描述，我们把这种模型称之为 Mesh 模型。

![image](https://user-images.githubusercontent.com/5803001/42416375-1492da36-829f-11e8-9993-b628d06d22c1.png)

这是那只著名的斯坦福兔子。它在 3D 图形中的地位与数字图像处理领域中著名的 lena 是类似的。看这只兔子，随着三角形数量的增加，它的表面越来越平滑/准确。在 Three 中，Mesh 的构造函数是这样的：`Mesh(geometry, material)` geometry 是它的形状，material 是它的材质。Geometry 通过存储模型用到的点集和点间关系(哪些点构成一个三角形)来达到描述物体形状的目的。Three 提供了立方体(其实是长方体)、平面(其实是长方形)、球体、圆形、圆柱、圆台等许多基本形状；对于比较复杂的形状，我们还可以通过外部的模型文件导入。

材质其实是物体表面除了形状以为所有可视属性的集合，例如色彩、纹理、光滑度、透明度、反射率、折射率、发光度。材质(Material) 包括了贴图(Map)和纹理(Texture)，贴图包括了图片和图片应当贴到什么位置，纹理本质上就是图。Three.js 提供了多种材质可供选择，能够自由地选择漫反射/镜面反射等材质。

Points 其实就是一堆点的集合，它在之前很长时间都被称为 ParticleSystem(粒子系统)，r68 版本时更名为 PointCloud,r72 版本时才更名为 Points。更名主要是因为，Mr.doob 认为，粒子系统应当是包括粒子和相关的物理特性的处理的一套完整体系，而 Three 中的 Points 简单得多。因此最终这个类被命名为 Points。

# 简单使用

## 旋转正方体

实际的 Three.js 应用中需要包含上述提及的关键对象，首先需要构建渲染器：

```js
function initRenderer() {
  width = document.getElementById("three_canvas").clientWidth;
  height = document.getElementById("three_canvas").clientHeight;
  renderer = new THREE.WebGLRenderer({
    canvas: document.getElementById("three_canvas")
  });
  renderer.setSize(width, height);
  renderer.setClearColor(0xffffff, 1.0);
}
```

然后初始化 Camera:

```js
function initCamera() {
  camera = new THREE.OrthographicCamera(
    width / -2,
    width / 2,
    height / 2,
    height / -2,
    1,
    1000
  );
  camera.position.x = 0;
  camera.position.y = 0;
  camera.position.z = 200;
  camera.up.x = 0;
  camera.up.y = 1;
  camera.up.z = 0;
  camera.lookAt({
    x: 0,
    y: 0,
    z: 0
  });
}
```

接下来则是初始化场景与场景中的物体：

```js
function initScene() {
  scene = new THREE.Scene();
}
function initObject() {
  var geometry = new THREE.CubeGeometry(100, 100, 100);
  object = new THREE.Mesh(geometry, new THREE.MeshNormalMaterial());
  scene.add(object);
}
```

最后是定期执行重渲染操作：

```js
function render() {
  requestAnimationFrame(render);
  object.rotation.x += 0.05;
  object.rotation.y += 0.05;
  renderer.render(scene, camera);
}
```

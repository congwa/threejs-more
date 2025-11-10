# threejs-more
Multiple three.js linked small examples.

## 归档说明

受精力所限，不打算在three.js 3d方向深挖，解惑为主


## use

```hs
npx http-server .
```


## three.js的对象体系

![three](/imgs/three.webp)


所有三维场景中的东西都加到 scene 里来管理。

三维世界本来是黑的，有了 light 之后才能看到东西，有点光源、环境光等不同的光源。

三维世界中的物体，可以从不同角度去观察，改变位置就可以看到不同的风景，这就是相机 camera 的事情。

三维世界中的物体叫做 mesh，任何一个物体都有一个形状，比如圆柱、立方体等，也就是 geometry，然后还得有材质 material，比如金属材质可以反光、普通材质不能。材质可以指定颜色、还可以指定图片作为纹理 texture。

场景中的所有物体，会由渲染器 WebGLRenderer 渲染出来。

场景、物体、灯光、相机、渲染器，这就是 three.js 的核心概念。

每一个物体都可以设置位置 position、缩放 scale、旋转 rotation。

每一帧渲染的时候，改变物体的位置、颜色、旋转角度等就可以实现动画效果了。


## three.js的坐标体系

![axes](/imgs/axes.webp)

原点在scene的中心


## 摄像机

![camera](/imgs/camera.webp)

从相机往前看，会有个角度 fov，这是第一个参数。

然后视野范围的矩形会有个宽高比 aspect，这是第二个参数。

视野范围会形成一个椎体，叫做视椎体，三四个参数是指定视椎体的范围，从哪里看到哪里。

```js
const camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 1000);
```

所以 PerspectiveCamera 的这 4个参数分别制定了 45 度的观察角度，宽高比和窗口宽高比一样。视野范围为 0.1 到 10000。


- fov  人睁开眼睛，眼睛睁大和眼镜眯的很小，竖向事业的范围是不同的，那么这角度可以理解为"睁眼睛的大小"
- 比例，就是缩放效果
- 0.1  near- 人睁开眼睛，看到的第一个切面，离眼睛成像最近的一个切面
- 100  far- 人睁开眼睛，看到的最远的切面，离眼睛成像最远的一个切面

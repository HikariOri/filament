# Filament

[![Android 构建状态](https://github.com/google/filament/actions/workflows/status-android.yml/badge.svg)](https://github.com/google/filament/actions/workflows/status-android.yml)
[![iOS 构建状态](https://github.com/google/filament/actions/workflows/status-ios.yml/badge.svg)](https://github.com/google/filament/actions/workflows/status-ios.yml)
[![Linux 构建状态](https://github.com/google/filament/actions/workflows/status-linux.yml/badge.svg)](https://github.com/google/filament/actions/workflows/status-linux.yml)
[![macOS 构建状态](https://github.com/google/filament/actions/workflows/status-macos.yml/badge.svg)](https://github.com/google/filament/actions/workflows/status-macos.yml)
[![Windows 构建状态](https://github.com/google/filament/actions/workflows/status-windows.yml/badge.svg)](https://github.com/google/filament/actions/workflows/status-windows.yml)
[![Web 构建状态](https://github.com/google/filament/actions/workflows/status-web.yml/badge.svg)](https://github.com/google/filament/actions/workflows/status-web.yml)

Filament 是一个实时物理渲染引擎，支持 Android、iOS、Linux、macOS、Windows 和 WASM 平台。其设计目标是体积尽可能小，且在 Android 上尽可能高效。

## 下载

[下载 Filament 发行版](https://github.com/google/filament/releases) 获取稳定版本。Filament 发行版归档中包含生成资源所需的主机端工具。

请确保始终使用与运行时库相同版本的工具，这对 `matc`（材质编译器）尤为重要。

如果你希望自行构建 Filament，请参考我们的[构建手册](/BUILDING.md)。

### Android

Android 项目可以直接将 Filament 库声明为 Maven 依赖：

```gradle
repositories {
    // ...
    mavenCentral()
}

dependencies {
    implementation 'com.google.android.filament:filament-android:1.71.3'
}
```

以下是 `com.google.android.filament` 组下所有可用的库：

| Artifact | 描述 |
| ------------- | ------------- |
| [![filament-android](https://img.shields.io/maven-central/v/com.google.android.filament/filament-android?label=filament-android&color=green)](https://mvnrepository.com/artifact/com.google.android.filament/filament-android) | Filament 渲染引擎本体。 |
| [![filament-android-debug](https://img.shields.io/maven-central/v/com.google.android.filament/filament-android-debug?label=filament-android-debug&color=green)](https://mvnrepository.com/artifact/com.google.android.filament/filament-android-debug) | `filament-android` 的调试版本。 |
| [![gltfio-android](https://img.shields.io/maven-central/v/com.google.android.filament/gltfio-android?label=gltfio-android&color=green)](https://mvnrepository.com/artifact/com.google.android.filament/gltfio-android) | Filament 的 glTF 2.0 加载器，依赖 `filament-android`。 |
| [![filament-utils-android](https://img.shields.io/maven-central/v/com.google.android.filament/filament-utils-android?label=filament-utils-android&color=green)](https://mvnrepository.com/artifact/com.google.android.filament/filament-utils-android) | KTX 加载、Kotlin 数学库和相机工具，依赖 `gltfio-android`。 |
| [![filamat-android](https://img.shields.io/maven-central/v/com.google.android.filament/filamat-android?label=filamat-android&color=green)](https://mvnrepository.com/artifact/com.google.android.filament/filamat-android) | 运行时材质构建/编译器。该库体积较大，但包含完整的着色器编译器/校验器/优化器，同时支持 OpenGL 和 Vulkan。 |

### iOS

iOS 项目可以使用 CocoaPods 安装最新发行版：

```shell
pod 'Filament', '~> 1.71.3'
```

## 文档

- [Filament](https://google.github.io/filament/Filament.html)，深入讲解实时物理渲染、Filament 的图形能力及实现。该文档解释了大多数设计决策背后的数学原理和推理，是图形程序员学习 PBR 的优秀入门资料。
- [Materials](https://google.github.io/filament/Materials.html)，材质系统的完整参考文档。该文档讲解了不同的材质模型、如何使用材质编译器 `matc` 以及如何编写自定义材质。
- [Material Properties](https://google.github.io/filament/notes/material_properties.html)，标准材质模型的参考速查表。

## 示例

![夜景场景](docs/images/samples/example_bistro1.jpg)
![夜景场景](docs/images/samples/example_bistro2.jpg)
![材质](docs/images/samples/example_materials1.jpg)
![材质](docs/images/samples/example_materials2.jpg)
![头盔](docs/images/samples/example_helmet.jpg)
![屏幕空间折射](docs/images/samples/example_ssr.jpg)

## 功能特性

### API

- Android、iOS、Linux、macOS 和 Windows 的原生 C++ API
- Android 的 Java/JNI API
- JavaScript API

### 渲染后端

- Linux、macOS 和 Windows 上的 OpenGL 4.1+
- Android 和 iOS 上的 OpenGL ES 3.0+
- macOS 和 iOS 上的 Metal
- Android、Linux、macOS 和 Windows 上的 Vulkan 1.0
- Android、Linux、macOS 和 Windows 上的 WebGPU
- 所有支持 WebGL 2.0 的浏览器

### 渲染

- 聚类前向渲染器
- Cook-Torrance 微面元高光 BRDF
- Lambertian 漫反射 BRDF
- 自定义光照/表面着色
- HDR/线性光照
- 金属度工作流
- 清漆（Clear Coat）
- 各向异性光照
- 近似半透明（次表面散射）材质
- 布料/织物/丝绒着色
- 法线贴图和环境光遮蔽贴图
- 基于图像的光照（IBL）
- 基于物理的相机模型（快门速度、感光度、光圈）
- 物理光照单位
- 点光源、聚光灯和方向光
- 高光抗锯齿
- 点光源、聚光灯和方向光阴影
- 级联阴影
- EVSM、PCSS、DPCF 或 PCF 阴影
- 透明阴影
- 接触阴影
- 屏幕空间环境光遮蔽
- 屏幕空间反射
- 屏幕空间折射
- 全局雾效
- 动态分辨率（支持 AMD FidelityFX FSR）

### 后处理

- HDR 泛光（Bloom）
- 散景景深（Depth of Field Bokeh）
- 多种色调映射器：PBR Neutral、AgX、通用（可自定义）、ACES、Filmic 等
- 色彩和色调管理：亮度缩放、色域映射
- 颜色分级：曝光、暗部适应、白平衡、通道混合器、阴影/中间调/高光、ASC CDL、对比度、饱和度等
- TAA、FXAA、MSAA
- 屏幕空间镜头光晕

### glTF 2.0

- 编码格式
  - [x] 内嵌式
  - [x] 二进制

- 图元类型
  - [x] 点
  - [x] 线段
  - [ ] 线段环
  - [x] 连续线段
  - [x] 三角形
  - [x] 连续三角形
  - [ ] 三角形扇

- 动画
  - [x] 变换动画
  - [x] 线性插值
  - [x] 变形动画
    - [x] 稀疏访问器
  - [x] 蒙皮动画
  - [x] 骨骼动画

- 扩展
  - [x] KHR_draco_mesh_compression
  - [x] KHR_lights_punctual
  - [x] KHR_materials_clearcoat
  - [x] KHR_materials_dispersion
  - [x] KHR_materials_emissive_strength
  - [x] KHR_materials_ior
  - [x] KHR_materials_pbrSpecularGlossiness
  - [x] KHR_materials_sheen
  - [x] KHR_materials_specular
  - [x] KHR_materials_transmission
  - [x] KHR_materials_unlit
  - [x] KHR_materials_variants
  - [x] KHR_materials_volume
  - [x] KHR_mesh_quantization
  - [x] KHR_texture_basisu
  - [x] KHR_texture_transform
  - [x] EXT_meshopt_compression

## 使用 Filament 进行渲染

### 原生 Linux、macOS 和 Windows

你需要创建一个 `Engine`、一个 `Renderer` 和一个 `SwapChain`。`SwapChain` 通过原生窗口指针（例如 macOS 上的 `NSView` 或 Windows 上的 `HWND`）创建：

```c++
Engine* engine = Engine::create();
SwapChain* swapChain = engine->createSwapChain(nativeWindow);
Renderer* renderer = engine->createRenderer();
```

渲染一帧时，还需要创建一个 `View`、一个 `Scene` 和一个 `Camera`：

```c++
Camera* camera = engine->createCamera(EntityManager::get().create());
View* view = engine->createView();
Scene* scene = engine->createScene();

view->setCamera(camera);
view->setScene(scene);
```

将可渲染对象添加到场景中：

```c++
Entity renderable = EntityManager::get().create();
// 构建一个四边形
RenderableManager::Builder(1)
        .boundingBox({{ -1, -1, -1 }, { 1, 1, 1 }})
        .material(0, materialInstance)
        .geometry(0, RenderableManager::PrimitiveType::TRIANGLES, vertexBuffer, indexBuffer, 0, 6)
        .culling(false)
        .build(*engine, renderable);
scene->addEntity(renderable);
```

材质实例从材质中获取，材质本身则通过 `matc` 生成的二进制 Blob 加载：

```c++
Material* material = Material::Builder()
        .package((void*) BAKED_MATERIAL_PACKAGE, sizeof(BAKED_MATERIAL_PACKAGE))
        .build(*engine);
MaterialInstance* materialInstance = material->createInstance();
```

要了解更多关于材质和 `matc` 的信息，请参考[材质文档](https://google.github.io/filament/Materials.html)。

渲染时，只需将 `View` 传递给 `Renderer` 即可：

```c++
// 如果返回 false 表示需要跳过此帧
if (renderer->beginFrame(swapChain)) {
    // 对每个 View
    renderer->render(view);
    renderer->endFrame();
}
```

关于 Linux、macOS 和 Windows 上完整的 Filament 应用程序示例，请查看 `samples/` 目录中的源文件。这些示例均基于 `libs/filamentapp/`，其中包含了使用 SDL2 创建原生窗口并初始化 Filament 引擎、渲染器和视图的代码。

有关如何为基于图像的光照准备环境贴图的更多信息，请参考[BUILDING.md](/BUILDING.md#running-the-native-samples)。

### Android

查看 `android/samples` 了解如何在 Android 上使用 Filament。

你必须始终先调用 `Filament.init()` 来初始化 Filament。

在 Android 上使用 Filament 渲染与原生代码渲染类似（API 在不同语言之间基本一致）。你可以通过将 `Surface` 传递给 `createSwapChain` 方法将内容渲染到 `Surface` 上，这允许你渲染到 `SurfaceTexture`、`TextureView` 或 `SurfaceView`。为简化操作，我们在 `com.google.android.filament.android` 包中提供了一个名为 `UiHelper` 的 Android 专用 API。你只需在 helper 上设置渲染回调，并将你的 `SurfaceView` 或 `TextureView` 附加到它上面即可。你仍然需要在 `onNativeWindowChanged()` 回调中自行创建交换链。

### iOS

Filament 支持 iOS 11.0 及以上版本。查看 `ios/samples` 了解在 iOS 上使用 Filament 的示例。

iOS 上的 Filament 与原生 C++ 渲染基本相同。将 `CAEAGLLayer` 或 `CAMetalLayer` 传递给 `createSwapChain` 方法即可。iOS 版 Filament 同时支持 Metal（推荐）和 OpenGL ES。

## 资源

入门时，你可以使用 `third_party/textures` 和 `third_party/environments` 目录中的纹理和环境贴图。这些资源基于 CC0 许可协议。请参阅各自的 `URL.txt` 文件以了解原作者信息。

环境贴图必须使用 [`cmgen`](/BUILDING.md#running-the-native-samples) 或 `libiblprefilter` 库进行预处理。

## 如何贡献

请阅读并遵循 [CONTRIBUTING.md](/CONTRIBUTING.md) 中的步骤。确保你熟悉[代码风格](/CODE_STYLE.md)。

## 目录结构

此仓库不仅包含核心的 Filament 引擎，还包含其支持库和工具。

- `android`:                  Android 库和项目
  - `filamat-android`:        Android 的 Filament 材质生成库（AAR）
  - `filament-android`:       Android 的 Filament 库（AAR）
  - `filament-utils-android`: 额外工具（KTX 加载器、数学类型等）
  - `gltfio-android`:         Android 的 Filament glTF 加载库（AAR）
  - `samples`:                面向 Android 的 Filament 示例
- `art`:                      各种艺术资源的源文件（Logo、PDF 手册等）
- `assets`:                   示例应用程序使用的 3D 资源
- `build`:                    CMake 构建脚本
- `docs`:                     文档
  - `math`:                   用于探索 BRDF、方程等的 Mathematica 笔记本
- `filament`:                 Filament 渲染引擎（最小依赖）
  - `backend`:                渲染后端/驱动（Vulkan、Metal、OpenGL/ES）
- `ide`:                      各 IDE 的配置文件（CLion 等）
- `ios`:                      iOS 示例项目
- `libs`:                     库
  - `bluegl`:                 macOS、Linux 和 Windows 的 OpenGL 绑定
  - `bluevk`:                 macOS、Linux、Windows 和 Android 的 Vulkan 绑定
  - `camutils`:               相机操控工具
  - `filabridge`:             Filament 引擎与主机工具之间共享的库
  - `filaflat`:               用于材质的序列化/反序列化库
  - `filagui`:                [Dear ImGui](https://github.com/ocornut/imgui) 的辅助库
  - `filamat`:                材质生成库
  - `filamentapp`:            SDL2 骨架，用于构建示例应用
  - `filameshio`:             微型 filamesh 解析库（另见 `tools/filamesh`）
  - `geometry`:               网格相关工具
  - `gltfio`:                 glTF 2.0 加载器
  - `ibl`:                    基于图像的光照生成工具
  - `image`:                  图像滤波和简单变换
  - `imageio`:                图像文件读写，仅供内部使用
  - `matdbg`:                 调试服务器，用于运行时检查着色器（仅调试构建）
  - `math`:                   数学库
  - `mathio`:                 数学类型对输出流的支持
  - `utils`:                  工具库（线程、内存、数据结构等）
  - `viewer`:                 glTF 查看器库（需要 gltfio）
- `samples`:                  桌面示例应用程序
- `shaders`:                  `filamat` 和 `matc` 使用的着色器
- `third_party`:              外部库和资源
  - `environments`:           CC0 许可的环境贴图，可与 `cmgen` 配合使用
  - `models`:                 宽松许可的模型
  - `textures`:               CC0 许可的纹理
- `tools`:                    主机工具
  - `cmgen`:                  基于图像的光照资源生成器
  - `filamesh`:               网格转换器
  - `glslminifier`:           压缩 GLSL 源代码
  - `matc`:                   材质编译器
  - `matedit`:                已编译材质的材质编辑器
  - `matinfo`                 显示通过 `matc` 编译的材质信息
  - `mipgen`                  从源图像生成一系列 Mip 级别
  - `normal-blending`:        混合法线贴图工具
  - `resgen`                  将二进制 Blob 聚合为可嵌入资源
  - `roughness-prefilter`:    从法线贴图预滤波粗糙度贴图以减少锯齿
  - `specular-color`:         基于光谱数据计算导体的高光颜色
- `web`:                      JavaScript 绑定、文档和示例

## 许可证

请参阅 [LICENSE](/LICENSE)。

## 免责声明

这不是一个受 Google 官方支持的产品。

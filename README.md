# Three.js 单手粒子交互系统

一个使用 Three.js、MediaPipe 和手势识别技术构建的互动式 3D 粒子系统。通过单手手势（张开/捏合手指、左右移动手掌）控制粒子模型的缩放和旋转，创造沉浸式的视觉体验。

## 功能特点

- ✨ **手势交互**：通过摄像头实时识别单手手势控制粒子系统
  - 张开/捏合手指控制缩放
  - 左右移动手掌控制旋转
- 🎨 **多种粒子模型**：内置四种粒子模型（心形、土星、花朵、星系）
- 🎭 **自定义配色**：每种模型都有默认颜色，也支持自定义颜色
- 🌌 **粒子动画**：粒子具有呼吸效果和平滑过渡动画
- 🖥️ **全屏支持**：一键进入全屏模式获得更好体验
- 📱 **响应式设计**：适配不同屏幕尺寸

## 技术栈

- [Three.js](https://threejs.org/) - 3D 图形库，用于渲染粒子系统
- [MediaPipe](https://mediapipe.dev/) - 谷歌的机器学习框架，用于手势识别
- [lil-gui](https://lil-gui.georgealways.com/) - 轻量级控制面板库
- 原生 JavaScript 和 WebGL

## 快速开始

### 前置要求

- 支持 WebGL 的现代浏览器（Chrome、Firefox、Safari、Edge 等）
- 带有摄像头的设备（笔记本、平板电脑、手机等）
- 允许浏览器访问摄像头权限

### 使用方法

1. 打开 `index.html` 文件（直接在浏览器中打开即可，无需服务器）
2. 允许浏览器访问摄像头权限
3. 等待模型加载完成（屏幕中央加载提示消失）
4. 使用单手进行以下操作：
   - **缩放**：张开/捏合拇指和食指
   - **旋转**：将手掌左右移动
5. 无手时模型会自动旋转

### 控制面板

点击界面右上角的控制面板图标，可以调整：
- **模型选择**：切换不同的粒子模型（心形、土星、花朵、星系）
- **颜色**：自定义粒子颜色

## 代码结构

```
├── index.html           # 主HTML文件，包含所有代码
```

主要代码模块：

- **初始化部分**：设置场景、相机、渲染器和粒子系统
- **形状生成器**：定义不同粒子模型的生成函数
- **手势识别**：使用 MediaPipe 处理摄像头输入，识别手势并映射为控制指令
- **动画循环**：更新粒子位置、应用缩放和旋转、处理过渡动画

## 自定义开发

如果您想修改或扩展此项目，可以考虑以下几个方面：

### 添加新模型

在 `shapes` 对象中添加新的生成函数：

```javascript
shapes['NewShape'] = (i) => {
    // 自定义坐标生成逻辑
    return [x, y, z];
};
```

### 调整粒子参数

修改全局配置参数以调整粒子效果：

```javascript
const PARTICLE_COUNT = 18000;  // 粒子数量
const PARTICLE_SIZE = 0.15;     // 粒子大小
```

### 修改手势灵敏度

在 `onResults` 函数中调整手势识别的映射参数：

```javascript
// 缩放映射
const targetScaleUnclamped = THREE.MathUtils.mapLinear(pinchDistance, 0.03, 0.2, 0.3, 2.5);

// 旋转速度映射
if (palmX < 0.4) {
    state.rotationSpeed = - (0.4 - palmX) * 0.15;
} else if (palmX > 0.6) {
    state.rotationSpeed = (palmX - 0.6) * 0.15;
}
```

## 浏览器支持

- Chrome (最新版本)
- Firefox (最新版本)
- Safari (最新版本)
- Microsoft Edge (最新版本)

## 注意事项

- 确保在光线充足的环境下使用，以提高手势识别准确性
- 保持手部在摄像头可视范围内
- 手势距离适中（不要太近或太远）以获得最佳识别效果
- 移动设备可能需要授予额外的摄像头权限

## 许可证

本项目采用 MIT 许可证。

## 致谢

- [Three.js](https://threejs.org/) - 强大的 JavaScript 3D 库
- [MediaPipe](https://mediapipe.dev/) - 提供优秀的手势识别能力
- [lil-gui](https://lil-gui.georgealways.com/) - 提供简洁的控制界面
- [Disc Sprite Texture](https://threejs.org/examples/textures/sprites/disc.png) - 粒子纹理

---

希望您喜欢这个交互式粒子系统！如有任何问题或建议，欢迎提出。

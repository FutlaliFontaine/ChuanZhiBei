# ChuanZhiBei
传智杯作品
# 老年人智能伴侣 · 真实智能体版

**在线体验地址：** [https://futlalifontaine.github.io/ChuanZhiBei/](https://futlalifontaine.github.io/ChuanZhiBei/)

---

## 📖 项目介绍

**老年人智能伴侣**是一款专为老年群体设计的适老化 Web 智能应用。项目采用高对比度暖色调界面、大字号排版（支持 18px–24px 动态切换）以及全页面语音播报机制，致力于消除老年人使用智能设备的“数字鸿沟”[cite: 1]。

### 核心功能模块
* **🎙️ 语音陪伴与真实 AI 对话**：集成语音识别（STT）、语音合成（TTS）与大语言模型，支持自然口语化多轮对话[cite: 1]。内置意图识别拦截器，当识别到“吃药/提醒”、“新闻”、“戏曲”、“故事”或“转账/银行卡”等敏感词时，可自动完成页面跳转或触发防诈骗安全弹窗警告[cite: 1]。
* **📰 今日资讯与哲理故事**：内置养生、防诈骗、用药安全等精选适老资讯与经典哲理故事，支持一键调用 AI 实时生成全新播报内容，并配合自动语音朗读[cite: 1]。
* **🎵 戏曲大观园**：内置黄梅戏、豫剧及经典轻音乐播放列表，同时支持上传并播放本地音频文件[cite: 1]。
* **⏰ 生活提醒**：支持手动添加日程提醒（如按时服药），也可通过 AI 一键推荐日常健康微习惯[cite: 1]。
* **📞 亲情联系（AI 拟人陪伴）**：支持管理家人通讯录，提供模拟视频通话界面，以及基于大模型的“家人角色扮演”文字/语音聊天（内置常见生活关怀关键词的毫秒级本地响应库与网络大模型双引擎）[cite: 1]。
* **🚨 紧急求助（SOS）**：配备防误触设计，长按求助按钮 3 秒触发警报，模拟向紧急联系人发送求救信号与当前位置[cite: 1]。

---

## 🏗️ 技术架构

本项目采用 **单页零构建（Zero-Build SPA）** 架构，所有样式、视图结构与业务逻辑均高度内聚于单个 HTML 文件中，无需打包编译即可部署运行[cite: 1]。

### 1. 技术栈选型
* **前端界面与样式**：原生 HTML5 + CSS3（使用 CSS Variables 实现全局字号动态缩放与暖色护眼主题，模拟 `375×667` 移动端视口容器）[cite: 1]。
* **逻辑控制与路由**：原生 ES6+ JavaScript，采用模块化对象字面量组织代码，通过 DOM `active` 状态切换实现无刷新单页路由（`Router`）[cite: 1]。
* **语音交互能力**：基于浏览器原生 **Web Speech API**（`SpeechRecognition` / `webkitSpeechRecognition` 实现语音转文字，`SpeechSynthesisUtterance` 实现全局页面与对话语音朗读）[cite: 1]。
* **AI 智能体接口**：通过 `Fetch API` 对接 Cloudflare Workers 部署的 LLM 代理接口（`openai-fast` 模型），配合 `AbortSignal.timeout(4000)` 超时熔断机制与本地多维兜底语料库，保障弱网或断网环境下的可用性[cite: 1]。
* **数据持久化**：基于浏览器 `localStorage` 封装内存级数据枢纽（`Store`），本地存储提醒事项与紧急联系人列表[cite: 1]。

### 2. 核心模块划分
| 模块名称 | 职责说明 |
| :--- | :--- |
| `Store` | 全局状态管理与 `localStorage` 本地数据持久化读写[cite: 1] |
| `System` | 全局 TTS 语音播报控制、自定义模态对话框（提示/输入/确认）、Toast 提示及全局字体缩放[cite: 1] |
| `Router` | 单页视图切换控制与页面进入时的生命周期数据渲染[cite: 1] |
| `AIService` | 主陪伴智能体上下文维护、系统指令路由拦截及大模型 API 通信[cite: 1] |
| `FamilyChat` | 亲情角色对话引擎，结合本地关键词秒回策略与大模型上下文生成[cite: 1] |
| `VoiceEngine` | 麦克风按住说话状态管理、STT 语音识别及键盘兜底输入[cite: 1] |
| `AudioPlayer` | 全局 `<audio>` 播放器控制、进度条拖拽及本地音频 `Blob URL` 解析[cite: 1] |
| `NewsManager` / `StoryManager` | 资讯与故事列表渲染及 AI 动态内容生成[cite: 1] |
| `ReminderManager` / `ContactManager` | 生活提醒与亲情联系人的增删改查（CRUD）[cite: 1] |
| `SOSEngine` | 紧急求助长按 3 秒进度条计算与警报触发器[cite: 1] |

---

## 🚀 安装与运行指南

由于项目为纯原生前端单文件应用，不依赖 Node.js 构建环境或第三方打包工具[cite: 1]，您可以通过以下任意一种方式运行：

### 方式一：直接在线访问（推荐）
无需任何安装配置，直接使用现代浏览器（推荐 Chrome、Edge 或 Safari）访问 GitHub Pages 部署地址：
👉 (https://futlalifontaine.github.io/ChuanZhiBei/)

### 方式二：本地启动服务运行
若需在本地进行二次开发或调试语音功能（注意：浏览器安全策略要求使用 `http://localhost` 或 `https://` 协议才能正常调用麦克风权限）：

1. **克隆或下载项目代码**
   ```bash
   git clone [https://github.com/futlalifontaine/ChuanZhiBei.git](https://github.com/futlalifontaine/ChuanZhiBei.git)
   cd ChuanZhiBei

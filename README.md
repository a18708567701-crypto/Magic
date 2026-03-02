<html lang="zh-CN"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI设计师 - 专业电商设计服务</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- GSAP 动画库 -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <!-- Three.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        :root {
            --primary-color: #0066ff;
            --secondary-color: #ff6600;
            --dark-bg: #0a0a1a;
            --light-text: #ffffff;
            --accent-gradient: linear-gradient(135deg, #0066ff, #ff6600);
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: var(--dark-bg);
            color: var(--light-text);
            overflow-x: hidden;
        }
        
        .gradient-text {
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .btn-primary {
            background: var(--accent-gradient);
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: 50px;
            font-weight: 600;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 102, 255, 0.3);
        }
        
        .btn-primary::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: all 0.6s ease;
            z-index: -1;
        }
        
        .btn-primary:hover::before {
            left: 100%;
        }
        
        .card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            padding: 2rem;
            transition: all 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0, 102, 255, 0.2);
            border-color: rgba(255, 255, 255, 0.2);
        }
        
        .service-icon {
            width: 60px;
            height: 60px;
            background: var(--accent-gradient);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 1.5rem;
            font-size: 1.5rem;
        }
        
        .portfolio-item {
            position: relative;
            overflow: hidden;
            border-radius: 15px;
            cursor: pointer;
        }
        
        .portfolio-item img {
            transition: all 0.5s ease;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .portfolio-item:hover img {
            transform: scale(1.1);
        }
        
        .portfolio-overlay {
            position: absolute;
            bottom: -100%;
            left: 0;
            width: 100%;
            padding: 2rem;
            background: linear-gradient(to top, rgba(0, 0, 0, 0.9), transparent);
            transition: all 0.5s ease;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
        }
        
        .portfolio-item:hover .portfolio-overlay {
            bottom: 0;
        }
        
        #hero-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        
        .ai-preview-container {
            background: rgba(255, 255, 255, 0.03);
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            overflow: hidden;
        }
        
        .upload-area {
            border: 2px dashed rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .upload-area:hover {
            border-color: var(--primary-color);
            background: rgba(0, 102, 255, 0.05);
        }
        
        .dynamic-island {
            position: fixed;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 50px;
            padding: 0.75rem 1.5rem;
            display: flex;
            align-items: center;
            gap: 1rem;
            z-index: 1000;
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .dynamic-island:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateX(-50%) translateY(-5px);
        }
        
        .nav-link {
            position: relative;
            padding: 0.5rem 0;
            margin: 0 1rem;
            color: rgba(255, 255, 255, 0.7);
            transition: all 0.3s ease;
        }
        
        .nav-link:hover {
            color: white;
        }
        
        .nav-link::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent-gradient);
            transition: all 0.3s ease;
        }
        
        .nav-link:hover::after {
            width: 100%;
        }
        
        .active-nav {
            color: white;
        }
        
        .active-nav::after {
            width: 100%;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .mobile-menu {
                position: fixed;
                top: 0;
                right: -100%;
                width: 80%;
                height: 100vh;
                background: rgba(10, 10, 26, 0.95);
                backdrop-filter: blur(20px);
                z-index: 1000;
                padding: 2rem;
                transition: all 0.5s ease;
                border-left: 1px solid rgba(255, 255, 255, 0.1);
            }
            
            .mobile-menu.active {
                right: 0;
            }
            
            .menu-overlay {
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.5);
                z-index: 999;
                opacity: 0;
                visibility: hidden;
                transition: all 0.5s ease;
            }
            
            .menu-overlay.active {
                opacity: 1;
                visibility: visible;
            }
        }
        
        /* 滚动条样式 */
        ::-webkit-scrollbar {
            width: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.05);
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--primary-color);
            border-radius: 4px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: var(--secondary-color);
        }
        
        /* 加载动画 */
        .loader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--dark-bg);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            transition: all 0.5s ease;
        }
        
        .loader.hidden {
            opacity: 0;
            visibility: hidden;
        }
        
        .loader-circle {
            width: 50px;
            height: 50px;
            border: 3px solid rgba(255, 255, 255, 0.1);
            border-top: 3px solid var(--primary-color);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* 动画类 */
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease;
        }
        
        .fade-in.active {
            opacity: 1;
            transform: translateY(0);
        }
        
        /* 3D旋转卡片 */
        .rotate-card-container {
            perspective: 1000px;
        }
        
        .rotate-card {
            transition: transform 0.8s;
            transform-style: preserve-3d;
        }
        
        .rotate-card-container:hover .rotate-card {
            transform: rotateY(180deg);
        }
        
        .rotate-card-front, .rotate-card-back {
            backface-visibility: hidden;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        
        .rotate-card-back {
            transform: rotateY(180deg);
        }
    </style>
</head>
<body>
    <!-- 加载动画 -->
    <div class="loader">
        <div class="loader-circle"></div>
    </div>

    <!-- 导航栏 -->
    <nav class="fixed top-0 left-0 w-full bg-transparent backdrop-blur-md z-50 transition-all duration-300" id="navbar">
        <div class="container mx-auto px-4 py-4 flex justify-between items-center">
            <a href="#" class="text-2xl font-bold gradient-text">电商AI设计服务</a>
            
            <!-- 桌面导航 -->
            <div class="hidden md:flex items-center">
                <a href="#home" class="nav-link active-nav">首页</a>
                <a href="#services" class="nav-link">服务</a>
                <a href="#ai-tool" class="nav-link">AI工具</a>
                <a href="#portfolio" class="nav-link">作品</a>
                <a href="#about" class="nav-link">关于</a>
                <a href="#contact" class="btn-primary ml-4">联系我</a>
            </div>
            
            <!-- 移动端菜单按钮 -->
            <button class="md:hidden text-white text-2xl" id="menu-toggle">
                <i class="fas fa-bars"></i>
            </button>
        </div>
    </nav>
    
    <!-- 移动端菜单 -->
    <div class="mobile-menu md:hidden">
        <div class="flex justify-end mb-8">
            <button class="text-white text-2xl" id="menu-close">
                <i class="fas fa-times"></i>
            </button>
        </div>
        <div class="flex flex-col space-y-4">
            <a href="#home" class="text-xl py-2 border-b border-gray-700 mobile-nav-link">首页</a>
            <a href="#services" class="text-xl py-2 border-b border-gray-700 mobile-nav-link">服务</a>
            <a href="#ai-tool" class="text-xl py-2 border-b border-gray-700 mobile-nav-link">AI工具</a>
            <a href="#portfolio" class="text-xl py-2 border-b border-gray-700 mobile-nav-link">作品</a>
            <a href="#about" class="text-xl py-2 border-b border-gray-700 mobile-nav-link">关于</a>
            <a href="#contact" class="btn-primary text-center mt-4 mobile-nav-link">联系我</a>
        </div>
    </div>
    <div class="menu-overlay"></div>

    <!-- 英雄区 -->
    <section id="home" class="min-h-screen flex items-center relative overflow-hidden pt-20">
        <canvas id="hero-canvas"></canvas>
        <div class="container mx-auto px-4 py-20">
            <div class="grid md:grid-cols-2 gap-12 items-center">
                <div class="fade-in">
                    <h1 class="text-4xl md:text-6xl font-bold mb-6">
                        <span class="gradient-text">做AI时代的设计师                     
                    </span></h1>
                    <p class="text-xl text-gray-300 mb-8">结合AI与创意设计，为电商产品打造令人惊艳的视觉体验，提升转化率和品牌价值；在
                    </p>
                    <div class="flex flex-wrap gap-4">
                        <a href="#services" class="btn-primary">
                            <i class="fas fa-paint-brush mr-2"></i> 我的服务
                        </a>
                        <a href="#ai-tool" class="bg-transparent border-2 border-white text-white px-6 py-3 rounded-full font-semibold hover:bg-white hover:text-black transition-all duration-300">
                            <i class="fas fa-magic mr-2"></i> AI预览工具
                        </a>
                    </div>
                    <div class="mt-12 flex items-center space-x-6">
                        <div class="flex -space-x-2">
                            <img src="https://p3-doubao-search-sign.byteimg.com/labis/8ca7c7659a7faa790c52a43570ac4550~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=GwdONggllF44TqeB1Jb4BlYupw0%3D" alt="客户头像" class="w-10 h-10 rounded-full border-2 border-white">
                            <img src="https://p26-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/902349685226602537~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=7iXOsCTCELdCSMn7zKxZCtNWe5E%3D" alt="客户头像" class="w-10 h-10 rounded-full border-2 border-white">
                            <img src="https://p11-doubao-search-sign.byteimg.com/labis/b2ad8471cdd66485f01a45a98fecb8c1~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=OOfRpUpOXIua64ZD%2Fd64pP6oLJw%3D" alt="客户头像" class="w-10 h-10 rounded-full border-2 border-white">
                        </div>
                        <div>
                            <div class="flex items-center">
                                <i class="fas fa-star text-yellow-400"></i>
                                <i class="fas fa-star text-yellow-400"></i>
                                <i class="fas fa-star text-yellow-400"></i>
                                <i class="fas fa-star text-yellow-400"></i>
                                <i class="fas fa-star text-yellow-400"></i>
                                <span class="ml-2 text-gray-300">5.0 (100+ 评价)</span>
                            </div>
                            <p class="text-sm text-gray-400">来自满意客户的评价</p>
                        </div>
                    </div>
                </div>
                <div class="fade-in" style="animation-delay: 0.3s;">
                    <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/15f2bd18921a45ddb581ec282a35e050~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=2026030214501292D0F9101901283FA128&amp;rrcfp=e75484ac&amp;x-expires=1773039015&amp;x-signature=deU8qx8b59AOrSkJv7g0ykqSkQY%3D" alt="AI设计" class="w-full rounded-3xl shadow-2xl">
                </div>
            </div>
        </div>
        <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 animate-bounce">
            <a href="#services" class="text-white text-3xl">
                <i class="fas fa-chevron-down"></i>
            </a>
        </div>
    </section>

    <!-- 服务展示 -->
    <section id="services" class="py-20 relative">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16 fade-in">
                <h2 class="text-3xl md:text-5xl font-bold mb-4">我的<span class="gradient-text">服务</span></h2>
                <p class="text-xl text-gray-300 max-w-3xl mx-auto">
                    提供全方位的AI设计解决方案，帮助您的电商产品脱颖而出，吸引更多客户
                </p>
            </div>
            
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- 服务卡片 1 -->
                <div class="card fade-in">
                    <div class="service-icon">
                        <i class="fas fa-camera"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-4">电商产品主图设计</h3>
                    <p class="text-gray-300 mb-6">
                        使用AI技术创建高质量的产品主附图，优化构图、高度契合人群、光影和色彩，提高点击率和转化率。
                    </p>
                    <div class="flex justify-between items-center">
                        <span class="text-xl font-bold gradient-text">¥299起</span>
                        <a href="#contact" class="text-white hover:text-blue-400 transition-colors">
                            了解更多 <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
                
                <!-- 服务卡片 2 -->
                <div class="card fade-in" style="animation-delay: 0.2s;">
                    <div class="service-icon">
                        <i class="fas fa-store"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-4">电商详情页与A+设计</h3>
                    <p class="text-gray-300 mb-6">
                        设计引人入胜的产品详情页或A+页面，结合AI生成的场景图和信息图表，提升用户体验和购买意愿。
                    </p>
                    <div class="flex justify-between items-center">
                        <span class="text-xl font-bold gradient-text">￥399起</span>
                        <a href="#contact" class="text-white hover:text-blue-400 transition-colors">
                            了解更多 <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
                
                <!-- 服务卡片 3 -->
                <div class="card fade-in" style="animation-delay: 0.4s;">
                    <div class="service-icon">
                        <i class="fas fa-paint-roller"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-4">品牌视觉识别系统</h3>
                    <p class="text-gray-300 mb-6">
                        创建独特的品牌视觉识别系统，包括标志、色彩方案和设计元素，提升品牌认知度和忠诚度。
                    </p>
                    <div class="flex justify-between items-center">
                        <span class="text-xl font-bold gradient-text">¥1999起</span>
                        <a href="#contact" class="text-white hover:text-blue-400 transition-colors">
                            了解更多 <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
                
                <!-- 服务卡片 4 -->
                <div class="card fade-in" style="animation-delay: 0.6s;">
                    <div class="service-icon">
                        <i class="fas fa-video"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-4">产品短视频制作</h3>
                    <p class="text-gray-300 mb-6">
                        使用AI技术创建引人注目的产品短视频，展示产品特性和使用场景，提高用户参与度。
                    </p>
                    <div class="flex justify-between items-center">
                        <span class="text-xl font-bold gradient-text">¥399起</span>
                        <a href="#contact" class="text-white hover:text-blue-400 transition-colors">
                            了解更多 <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
                
                <!-- 服务卡片 5 -->
                <div class="card fade-in" style="animation-delay: 0.8s;">
                    <div class="service-icon">
                        <i class="fas fa-mobile-alt"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-4">社交媒体素材设计</h3>
                    <p class="text-gray-300 mb-6">
                        设计适合各平台的社交媒体素材，包括海报、故事和广告图，增强品牌在社交平台的影响力。
                    </p>
                    <div class="flex justify-between items-center">
                        <span class="text-xl font-bold gradient-text">¥199起</span>
                        <a href="#contact" class="text-white hover:text-blue-400 transition-colors">
                            了解更多 <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
                
                <!-- 服务卡片 6 -->
                <div class="card fade-in" style="animation-delay: 1s;">
                    <div class="service-icon">
                        <i class="fas fa-robot"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-4">AI设计定制服务</h3>
                    <p class="text-gray-300 mb-6">
                        根据您的特定需求，提供个性化的AI设计解决方案，包括特殊效果、3D渲染和交互式设计。
                    </p>
                    <div class="flex justify-between items-center">
                        <span class="text-xl font-bold gradient-text">¥399起</span>
                        <a href="#contact" class="text-white hover:text-blue-400 transition-colors">
                            了解更多 <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- AI预览工具 -->
    <section id="ai-tool" class="py-20 relative bg-gradient-to-b from-[#0a0a1a] to-[#0f1a3a]">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16 fade-in">
                <h2 class="text-3xl md:text-5xl font-bold mb-4">AI<span class="gradient-text">预览工具</span></h2>
                <p class="text-xl text-gray-300 max-w-3xl mx-auto">
                    上传您的产品图片，体验AI设计效果，预览您的产品在不同场景和风格下的呈现效果
                </p>
            </div>
            
            <div class="ai-preview-container p-8 fade-in">
                <div class="grid md:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-2xl font-bold mb-4">上传产品图片</h3>
                        <div class="upload-area p-8 text-center mb-6" id="upload-area">
                            <input type="file" id="product-image" class="hidden" accept="image/*">
                            <i class="fas fa-cloud-upload-alt text-4xl text-gray-400 mb-4"></i>
                            <p class="text-gray-300 mb-2">点击或拖拽上传产品图片</p>
                            <p class="text-sm text-gray-500">支持 JPG, PNG 格式，最大 5MB</p>
                        </div>
                        
                        <div class="mb-6">
                            <h4 class="text-lg font-semibold mb-3">选择设计风格</h4>
                            <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
                                <button class="style-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors active" data-style="modern">
                                    <i class="fas fa-building text-blue-500 mb-2"></i>
                                    <p class="text-sm">现代简约</p>
                                </button>
                                <button class="style-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-style="elegant">
                                    <i class="fas fa-gem text-purple-500 mb-2"></i>
                                    <p class="text-sm">优雅奢华</p>
                                </button>
                                <button class="style-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-style="natural">
                                    <i class="fas fa-leaf text-green-500 mb-2"></i>
                                    <p class="text-sm">自然清新</p>
                                </button>
                                <button class="style-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-style="vintage">
                                    <i class="fas fa-clock text-amber-500 mb-2"></i>
                                    <p class="text-sm">复古怀旧</p>
                                </button>
                                <button class="style-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-style="futuristic">
                                    <i class="fas fa-rocket text-cyan-500 mb-2"></i>
                                    <p class="text-sm">未来科技</p>
                                </button>
                                <button class="style-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-style="artistic">
                                    <i class="fas fa-palette text-pink-500 mb-2"></i>
                                    <p class="text-sm">艺术创意</p>
                                </button>
                            </div>
                        </div>
                        
                        <div class="mb-6">
                            <h4 class="text-lg font-semibold mb-3">选择场景</h4>
                            <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
                                <button class="scene-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors active" data-scene="studio">
                                    <i class="fas fa-camera text-blue-500 mb-2"></i>
                                    <p class="text-sm">专业棚拍</p>
                                </button>
                                <button class="scene-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-scene="home">
                                    <i class="fas fa-home text-amber-500 mb-2"></i>
                                    <p class="text-sm">家居环境</p>
                                </button>
                                <button class="scene-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-scene="office">
                                    <i class="fas fa-briefcase text-gray-400 mb-2"></i>
                                    <p class="text-sm">办公场景</p>
                                </button>
                                <button class="scene-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-scene="outdoor">
                                    <i class="fas fa-mountain text-green-600 mb-2"></i>
                                    <p class="text-sm">户外场景</p>
                                </button>
                                <button class="scene-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-scene="social">
                                    <i class="fas fa-hashtag text-pink-500 mb-2"></i>
                                    <p class="text-sm">社交媒体</p>
                                </button>
                                <button class="scene-option p-3 border border-gray-700 rounded-lg hover:border-blue-500 transition-colors" data-scene="custom">
                                    <i class="fas fa-sliders-h text-purple-500 mb-2"></i>
                                    <p class="text-sm">自定义</p>
                                </button>
                            </div>
                        </div>
                        
                        <button id="generate-btn" class="btn-primary w-full">
                            <i class="fas fa-magic mr-2"></i> 生成预览效果
                        </button>
                    </div>
                    
                    <div>
                        <h3 class="text-2xl font-bold mb-4">预览效果</h3>
                        <div class="bg-gray-900 rounded-lg p-4 h-[500px] flex items-center justify-center relative overflow-hidden" id="preview-container">
                            <div class="text-center" id="preview-placeholder">
                                <i class="fas fa-image text-5xl text-gray-700 mb-4"></i>
                                <p class="text-gray-500">上传产品图片并点击生成按钮查看预览效果</p>
                            </div>
                            <div id="preview-result" class="hidden w-full h-full">
                                <img id="result-image" class="w-full h-full object-contain" alt="预览效果">
                            </div>
                            <div id="preview-loading" class="hidden absolute inset-0 bg-black bg-opacity-70 flex items-center justify-center">
                                <div class="loader-circle"></div>
                                <p class="text-white ml-4">AI正在生成预览效果...</p>
                            </div>
                        </div>
                        
                        <div class="mt-6 flex justify-between">
                            <button id="download-btn" class="hidden px-6 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
                                <i class="fas fa-download mr-2"></i> 下载图片
                            </button>
                            <button id="share-btn" class="hidden px-6 py-2 bg-transparent border border-white text-white rounded-lg hover:bg-white hover:text-black transition-colors">
                                <i class="fas fa-share-alt mr-2"></i> 分享效果
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 作品案例 -->
    <section id="portfolio" class="py-20 relative">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16 fade-in">
                <h2 class="text-3xl md:text-5xl font-bold mb-4">作品<span class="gradient-text">案例</span></h2>
                <p class="text-xl text-gray-300 max-w-3xl mx-auto">
                    浏览我的精选作品，了解AI设计如何为不同类型的电商产品提升视觉效果和营销价值
                </p>
            </div>
            
            <!-- 作品分类筛选 -->
            <div class="flex flex-wrap justify-center gap-4 mb-12 fade-in">
                <button class="portfolio-filter px-6 py-2 rounded-full bg-blue-600 text-white active" data-filter="all">全部作品</button>
                <button class="portfolio-filter px-6 py-2 rounded-full bg-transparent border border-white text-white hover:bg-white hover:text-black transition-colors" data-filter="fashion">时尚家居</button>
                <button class="portfolio-filter px-6 py-2 rounded-full bg-transparent border border-white text-white hover:bg-white hover:text-black transition-colors" data-filter="electronics">电子产品</button>
                <button class="portfolio-filter px-6 py-2 rounded-full bg-transparent border border-white text-white hover:bg-white hover:text-black transition-colors" data-filter="beauty">美妆护肤</button>
                <button class="portfolio-filter px-6 py-2 rounded-full bg-transparent border border-white text-white hover:bg-white hover:text-black transition-colors" data-filter="home">汽车汽配</button>
            </div>
            
            <!-- 作品网格 -->
            <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- 作品项 1 -->
                <div class="portfolio-item fade-in cursor-pointer" data-category="fashion" onclick="openImageViewer('fashion-packaging')">
                    <img src="https://p3-doubao-search-sign.byteimg.com/labis/2a6f97976868e404be6f12f0e28290f1~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=51frPvxtJ1PUhNGuDrBB0blnCNE%3D" alt="时尚服饰包装设计">
                    <div class="portfolio-overlay">
                        <h3 class="text-xl font-bold mb-2">时尚服饰包装设计</h3>
                        <p class="text-gray-300 mb-4">为淘宝服饰品牌设计的包装盒，采用现代几何图案和鲜明色彩</p>
                        <div class="flex items-center text-blue-400">
                            <i class="fas fa-images mr-2"></i>
                            <span>查看3张图片</span>
                        </div>
                    </div>
                </div>
                
                <!-- 作品项 2 -->
                <div class="portfolio-item fade-in cursor-pointer" style="animation-delay: 0.2s;" data-category="electronics" onclick="openImageViewer('smartwatch')">
                    <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/22b85ffa08094c138049bc0bdfb6f990~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=20260228172422E381F39E4B09C7921E2A&amp;rrcfp=f06b921b&amp;x-expires=1774862700&amp;x-signature=wASp55yLDwr%2BZSSJmuAyOG8LAng%3D" alt="智能手表设计">
                    <div class="portfolio-overlay">
                        <h3 class="text-xl font-bold mb-2">智能手表电商主图</h3>
                        <p class="text-gray-300 mb-4">高科技感的智能手表产品展示，突出产品特性和设计感</p>
                        <div class="flex items-center text-blue-400">
                            <i class="fas fa-images mr-2"></i>
                            <span>查看4张图片</span>
                        </div>
                    </div>
                </div>
                
                <!-- 作品项 3 -->
                <div class="portfolio-item fade-in cursor-pointer" style="animation-delay: 0.4s;" data-category="beauty" onclick="openImageViewer('cosmetics')">
                    <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/896492772e3e4cd3a74405b2687efc53~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=202603021353166E8D12F6AAA9D2CD1DB0&amp;rrcfp=e75484ac&amp;x-expires=1773035597&amp;x-signature=AHOGxzg3gNI5WY6%2BvQfO%2FvnuTS0%3D" alt="化妆品系列设计">
                    <div class="portfolio-overlay">
                        <h3 class="text-xl font-bold mb-2">化妆品系列设计</h3>
                        <p class="text-gray-300 mb-4">为护肤品牌设计的产品展示图，采用蓝橙渐变背景增强视觉冲击力</p>
                        <div class="flex items-center text-blue-400">
                            <i class="fas fa-images mr-2"></i>
                            <span>查看5张图片</span>
                        </div>
                    </div>
                </div>
                
                <!-- 作品项 4 -->
                <div class="portfolio-item fade-in cursor-pointer" style="animation-delay: 0.6s;" data-category="electronics" onclick="openImageViewer('phone-case')">
                    <img src="https://p11-doubao-search-sign.byteimg.com/tos-cn-i-qvj2lq49k0/d83b8bac5c214158bc34798038c00aa0~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=JB8ToJoZGtEtIXKodrDAcdm3KpY%3D" alt="手机壳设计">
                    <div class="portfolio-overlay">
                        <h3 class="text-xl font-bold mb-2">创意手机壳设计</h3>
                        <p class="text-gray-300 mb-4">结合AI绘画技术设计的趣味手机壳图案，吸引年轻消费群体</p>
                        <div class="flex items-center text-blue-400">
                            <i class="fas fa-images mr-2"></i>
                            <span>查看3张图片</span>
                        </div>
                    </div>
                </div>
                
                <!-- 作品项 5 -->
                <div class="portfolio-item fade-in cursor-pointer" style="animation-delay: 0.8s;" data-category="fashion" onclick="openImageViewer('ai-tryon')">
                    <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/697590e9c48c4cc2977b1d02a464148f~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=2026030214020148F3A4625C871FCB8FF6&amp;rrcfp=e75484ac&amp;x-expires=1773036126&amp;x-signature=9ike9C7WmFq4NZhOH6EmT3g3Z40%3D" alt="AI首饰试戴">
                    <div class="portfolio-overlay">
                        <h3 class="text-xl font-bold mb-2">AI首饰试戴系统</h3>
                        <p class="text-gray-300 mb-4">创新的AI试戴技术，让用户在线体验首饰和服装搭配效果</p>
                        <div class="flex items-center text-blue-400">
                            <i class="fas fa-images mr-2"></i>
                            <span>查看4张图片</span>
                        </div>
                    </div>
                </div>
                
                <!-- 作品项 6 -->
                <div class="portfolio-item fade-in cursor-pointer" style="animation-delay: 1s;" data-category="home" onclick="openImageViewer('golden-horse')">
                    <img src="https://p26-doubao-search-sign.byteimg.com/labis/ecf4acccf0a8b618fc26381b3824dc60~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=YuZ6cMjuSrvrMiz0zrzanwJMOAI%3D" alt="金色马摆件设计">
                    <div class="portfolio-overlay">
                        <h3 class="text-xl font-bold mb-2">金色马摆件设计</h3>
                        <p class="text-gray-300 mb-4">AI矢量设计的家居装饰品，采用几何风格和金色配色提升奢华感</p>
                        <div class="flex items-center text-blue-400">
                            <i class="fas fa-images mr-2"></i>
                            <span>查看2张图片</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 图片查看器模态框 -->
            <div id="image-viewer" class="fixed inset-0 bg-black bg-opacity-90 z-50 flex items-center justify-center hidden">
                <div class="relative w-full max-w-6xl mx-auto px-4">
                    <!-- 关闭按钮 -->
                    <button id="close-viewer" class="absolute top-4 right-4 text-white text-3xl hover:text-gray-300 transition-colors z-10">
                        <i class="fas fa-times"></i>
                    </button>
                    
                    <!-- 图片导航 -->
                    <button id="prev-image" class="absolute left-4 top-1/2 transform -translate-y-1/2 text-white text-4xl hover:text-gray-300 transition-colors z-10">
                        <i class="fas fa-chevron-left"></i>
                    </button>
                    <button id="next-image" class="absolute right-4 top-1/2 transform -translate-y-1/2 text-white text-4xl hover:text-gray-300 transition-colors z-10">
                        <i class="fas fa-chevron-right"></i>
                    </button>
                    
                    <!-- 图片显示区域 -->
                    <div class="bg-gray-900 rounded-lg p-4">
                        <div class="flex flex-col items-center">
                            <h3 id="viewer-title" class="text-2xl font-bold mb-4 text-center">作品标题</h3>
                            <div class="relative w-full h-[60vh] flex items-center justify-center">
                                <img id="viewer-image" class="max-w-full max-h-full object-contain" src="" alt="作品图片">
                                <div id="viewer-loading" class="absolute inset-0 flex items-center justify-center bg-black bg-opacity-50 hidden">
                                    <div class="loader-circle"></div>
                                </div>
                            </div>
                            <p id="viewer-caption" class="text-gray-300 mt-4 text-center">图片描述</p>
                            <div class="mt-4 text-gray-400">
                                <span id="viewer-counter">1 / 3</span>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 缩略图导航 -->
                    <div id="thumbnail-nav" class="mt-6 flex gap-4 overflow-x-auto pb-4">
                        <!-- 缩略图将通过JavaScript动态添加 -->
                    </div>
                </div>
            </div>
            
            <div class="text-center mt-12 fade-in">
                <a href="#" class="btn-primary">
                    查看更多作品 <i class="fas fa-arrow-right ml-2"></i>
                </a>
            </div>
        </div>
    </section>

    <!-- 电商AI资讯 -->
    <section id="ai-news" class="py-20 relative bg-gradient-to-b from-[#0a0a1a] to-[#1a1a2e]">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16 fade-in">
                <h2 class="text-3xl md:text-5xl font-bold mb-4">电商<span class="gradient-text">AI资讯</span></h2>
                <p class="text-xl text-gray-300 max-w-3xl mx-auto">
                    了解最新的电商AI设计趋势、技术动态和行业洞察，助您把握设计前沿
                </p>
            </div>
            
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- 资讯卡片 1 -->
                <div class="card fade-in">
                    <div class="relative mb-4 overflow-hidden rounded-xl">
                        <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/5552050a4bbf4633ae2a67713fecb909~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=20260228173458515FD5EE1B666EB6A744&amp;rrcfp=e75484ac&amp;x-expires=1772876101&amp;x-signature=Z6p7i9%2B5YwC%2FkljL%2FYdgSpSJg0o%3D" alt="AI设计趋势" class="w-full h-48 object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-3 left-3 bg-blue-600 text-white text-xs px-2 py-1 rounded-full">
                            设计趋势
                        </div>
                    </div>
                    <div class="mb-2 flex items-center text-sm text-gray-400">
                        <i class="far fa-calendar-alt mr-2"></i>
                        <span>2024年1月15日</span>
                    </div>
                    <h3 class="text-xl font-bold mb-3">2024年电商设计的五大AI技术趋势</h3>
                    <p class="text-gray-300 mb-4 line-clamp-3">
                        从AI生成式设计到智能个性化推荐，探索如何利用最新的AI技术提升电商产品的视觉吸引力和转化率...
                    </p>
                    <a href="#" class="text-blue-400 hover:text-blue-300 transition-colors flex items-center">
                        阅读全文 <i class="fas fa-arrow-right ml-2"></i>
                    </a>
                </div>
                
                <!-- 资讯卡片 2 -->
                <div class="card fade-in" style="animation-delay: 0.2s;">
                    <div class="relative mb-4 overflow-hidden rounded-xl">
                        <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/0573336e481a40948f8770f21094f173~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=20260228173458515FD5EE1B666EB6A744&amp;rrcfp=e75484ac&amp;x-expires=1772876101&amp;x-signature=422k3rqYv%2Bv7GzW3m43%2F1j5rBw%3D" alt="AI设计工具" class="w-full h-48 object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-3 left-3 bg-purple-600 text-white text-xs px-2 py-1 rounded-full">
                            工具教程
                        </div>
                    </div>
                    <div class="mb-2 flex items-center text-sm text-gray-400">
                        <i class="far fa-calendar-alt mr-2"></i>
                        <span>2024年1月10日</span>
                    </div>
                    <h3 class="text-xl font-bold mb-3">10个必备的AI电商设计工具详解</h3>
                    <p class="text-gray-300 mb-4 line-clamp-3">
                        深度解析当前最流行的AI设计工具，从图像生成到智能排版，让您的电商设计工作事半功倍...
                    </p>
                    <a href="#" class="text-blue-400 hover:text-blue-300 transition-colors flex items-center">
                        阅读全文 <i class="fas fa-arrow-right ml-2"></i>
                    </a>
                </div>
                
                <!-- 资讯卡片 3 -->
                <div class="card fade-in" style="animation-delay: 0.4s;">
                    <div class="relative mb-4 overflow-hidden rounded-xl">
                        <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/e7b96c8af7c44f1594570a9259f161e3~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=20260228173458515FD5EE1B666EB6A744&amp;rrcfp=e75484ac&amp;x-expires=1772876101&amp;x-signature=%2F7MvUQHpi72VIEYbSnPrWhU3u5w%3D" alt="AI设计案例" class="w-full h-48 object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-3 left-3 bg-green-600 text-white text-xs px-2 py-1 rounded-full">
                            案例分析
                        </div>
                    </div>
                    <div class="mb-2 flex items-center text-sm text-gray-400">
                        <i class="far fa-calendar-alt mr-2"></i>
                        <span>2024年1月5日</span>
                    </div>
                    <h3 class="text-xl font-bold mb-3">AI设计如何帮助中小电商提升300%转化率</h3>
                    <p class="text-gray-300 mb-4 line-clamp-3">
                        真实案例分享：一家普通电商店铺如何通过AI设计优化，在3个月内实现转化率提升300%的惊人成果...
                    </p>
                    <a href="#" class="text-blue-400 hover:text-blue-300 transition-colors flex items-center">
                        阅读全文 <i class="fas fa-arrow-right ml-2"></i>
                    </a>
                </div>
            </div>
            
            <!-- 资讯订阅 -->
            <div class="mt-16 bg-gradient-to-r from-blue-900/30 to-purple-900/30 rounded-2xl p-8 md:p-12 fade-in" style="animation-delay: 0.6s;">
                <div class="grid md:grid-cols-2 gap-8 items-center">
                    <div>
                        <h3 class="text-2xl md:text-3xl font-bold mb-4">订阅电商AI资讯</h3>
                        <p class="text-gray-300 mb-6">
                            第一时间获取最新的电商AI设计资讯、工具教程和行业洞察，助力您的电商业务增长
                        </p>
                        <form class="flex flex-col sm:flex-row gap-4">
                            <input type="email" placeholder="输入您的邮箱地址" class="flex-1 bg-black/30 border border-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:border-blue-500 transition-colors">
                            <button type="submit" class="btn-primary whitespace-nowrap">
                                立即订阅 <i class="fas fa-paper-plane ml-2"></i>
                            </button>
                        </form>
                    </div>
                    <div class="hidden md:block">
                        <img src="https://p3-doubao-search-sign.byteimg.com/labis/1b3c1bb82a7baa3b74597bc14105f28f~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=tM22L%2BzF2QiCGE8j9SaWEEDHpWU%3D" alt="AI资讯" class="w-full rounded-xl shadow-2xl">
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 关于我 -->
    <section id="about" class="py-20 relative bg-gradient-to-b from-[#0a0a1a] to-[#0f1a3a]">
        <div class="container mx-auto px-4">
            <div class="grid md:grid-cols-2 gap-12 items-center">
                <div class="fade-in">
                    <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/2dcb7bec0b764dfab7321ae642dd8cd0~tplv-a9rns2rl98-image.image?lk3s=8e244e95&amp;rcl=20260302134954CF1CDA09DF9C959E3AEA&amp;rrcfp=e75484ac&amp;x-expires=1773035399&amp;x-signature=zRHFYLsVqO8VPbzESCLnhBDTa%2FY%3D" alt="设计师形象" class="w-full rounded-3xl shadow-2xl">
                </div>
                <div class="fade-in" style="animation-delay: 0.3s;">
                    <h2 class="text-3xl md:text-5xl font-bold mb-6">关于<span class="gradient-text">我</span></h2>
                    <p class="text-xl text-gray-300 mb-6">我是一名专注于AI设计的从业者，拥有9年电商设计经验和深厚的AI技术应用能力。
                    </p>
                    <p class="text-gray-300 mb-6">
                        我擅长将人工智能技术与创意设计相结合，为电商产品打造独特而有效的视觉体验。我的设计理念是"技术赋能创意，创意提升价值"，通过不断探索AI在设计领域的应用边界，为客户提供更高效、更具创意的设计解决方案。
                    </p>
                    <p class="text-gray-300 mb-8">
                        我曾为多家知名电商品牌提供设计服务，帮助他们提升品牌形象和销售业绩。我相信，在AI技术的助力下，设计将变得更加个性化、智能化和高效化。
                    </p>
                    
                    <div class="grid grid-cols-2 gap-6 mb-8">
                        <div>
                            <h4 class="text-3xl font-bold gradient-text mb-2">9+</h4>
                            <p class="text-gray-400">年设计经验</p>
                        </div>
                        <div>
                            <h4 class="text-3xl font-bold gradient-text mb-2">200+</h4>
                            <p class="text-gray-400">满意客户</p>
                        </div>
                        <div>
                            <h4 class="text-3xl font-bold gradient-text mb-2">500+</h4>
                            <p class="text-gray-400">完成项目</p>
                        </div>
                        <div>
                            <h4 class="text-3xl font-bold gradient-text mb-2">15+</h4>
                            <p class="text-gray-400">行业领域</p>
                        </div>
                    </div>
                    
                    <div class="flex gap-4">
                        <a href="#" class="w-10 h-10 rounded-full bg-blue-600 flex items-center justify-center hover:bg-blue-700 transition-colors">
                            <i class="fab fa-behance"></i>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-blue-400 flex items-center justify-center hover:bg-blue-500 transition-colors">
                            <i class="fab fa-dribbble"></i>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-red-600 flex items-center justify-center hover:bg-red-700 transition-colors">
                            <i class="fab fa-instagram"></i>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-blue-800 flex items-center justify-center hover:bg-blue-900 transition-colors">
                            <i class="fab fa-linkedin-in"></i>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 客户评价 -->
    <section class="py-20 relative">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16 fade-in">
                <h2 class="text-3xl md:text-5xl font-bold mb-4">客户<span class="gradient-text">评价</span></h2>
                <p class="text-xl text-gray-300 max-w-3xl mx-auto">
                    听听我的客户怎么说，他们的成功案例是我最好的证明
                </p>
            </div>
            
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- 评价卡片 1 -->
                <div class="card fade-in">
                    <div class="flex items-center mb-4">
                        <img src="https://p3-doubao-search-sign.byteimg.com/labis/8ca7c7659a7faa790c52a43570ac4550~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=GwdONggllF44TqeB1Jb4BlYupw0%3D" alt="客户头像" class="w-12 h-12 rounded-full mr-4">
                        <div>
                            <h4 class="font-bold">李明</h4>
                            <p class="text-sm text-gray-400">电商创业者</p>
                        </div>
                    </div>
                    <div class="mb-4">
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                    </div>
                    <p class="text-gray-300">
                        "AI设计师的作品让我的产品在竞争激烈的电商平台上脱颖而出。使用AI预览工具后，我的产品图片点击率提升了35%，销售额增长了20%。非常专业的服务！"
                    </p>
                </div>
                
                <!-- 评价卡片 2 -->
                <div class="card fade-in" style="animation-delay: 0.2s;">
                    <div class="flex items-center mb-4">
                        <img src="https://p26-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/902349685226602537~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=7iXOsCTCELdCSMn7zKxZCtNWe5E%3D" alt="客户头像" class="w-12 h-12 rounded-full mr-4">
                        <div>
                            <h4 class="font-bold">张婷</h4>
                            <p class="text-sm text-gray-400">美妆品牌创始人</p>
                        </div>
                    </div>
                    <div class="mb-4">
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                    </div>
                    <p class="text-gray-300">
                        "作为一个初创美妆品牌，我们需要专业的视觉设计来建立品牌形象。AI设计师不仅提供了高质量的设计作品，还帮助我们节省了大量时间和成本。非常推荐！"
                    </p>
                </div>
                
                <!-- 评价卡片 3 -->
                <div class="card fade-in" style="animation-delay: 0.4s;">
                    <div class="flex items-center mb-4">
                        <img src="https://p11-doubao-search-sign.byteimg.com/labis/b2ad8471cdd66485f01a45a98fecb8c1~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&amp;x-expires=1787822675&amp;x-signature=OOfRpUpOXIua64ZD%2Fd64pP6oLJw%3D" alt="客户头像" class="w-12 h-12 rounded-full mr-4">
                        <div>
                            <h4 class="font-bold">王强</h4>
                            <p class="text-sm text-gray-400">电子产品销售经理</p>
                        </div>
                    </div>
                    <div class="mb-4">
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star text-yellow-400"></i>
                        <i class="fas fa-star-half-alt text-yellow-400"></i>
                    </div>
                    <p class="text-gray-300">
                        "我们的电子产品需要专业的产品展示图，AI设计师使用AI技术创建的3D渲染效果非常出色，让我们的产品看起来更高级、更有科技感。合作非常愉快！"
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- 联系我 -->
    <section id="contact" class="py-20 relative bg-gradient-to-b from-[#0a0a1a] to-[#0f1a3a]">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16 fade-in">
                <h2 class="text-3xl md:text-5xl font-bold mb-4">联系<span class="gradient-text">我</span></h2>
                <p class="text-xl text-gray-300 max-w-3xl mx-auto">
                    无论您有任何问题或项目需求，都可以通过以下方式联系我，我将尽快回复您
                </p>
            </div>
            
            <div class="grid md:grid-cols-2 gap-12">
                <div class="fade-in">
                    <form class="space-y-6">
                        <div>
                            <label for="name" class="block text-gray-300 mb-2">姓名</label>
                            <input type="text" id="name" class="w-full bg-transparent border border-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:border-blue-500 transition-colors" placeholder="请输入您的姓名">
                        </div>
                        <div>
                            <label for="email" class="block text-gray-300 mb-2">邮箱</label>
                            <input type="email" id="email" class="w-full bg-transparent border border-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:border-blue-500 transition-colors" placeholder="请输入您的邮箱">
                        </div>
                        <div>
                            <label for="subject" class="block text-gray-300 mb-2">主题</label>
                            <input type="text" id="subject" class="w-full bg-transparent border border-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:border-blue-500 transition-colors" placeholder="请输入主题">
                        </div>
                        <div>
                            <label for="message" class="block text-gray-300 mb-2">咨询问题</label>
                            <textarea id="message" rows="5" class="w-full bg-transparent border border-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:border-blue-500 transition-colors" placeholder="请输入您的消息"></textarea>
                        </div>
                        <button type="submit" class="btn-primary w-full">
                            发送消息 <i class="fas fa-paper-plane ml-2"></i>
                        </button>
                    </form>
                </div>
                
                <div class="fade-in" style="animation-delay: 0.3s;">
                    <div class="bg-gray-900 bg-opacity-50 p-8 rounded-2xl h-full">
                        <h3 class="text-2xl font-bold mb-6">联系方式</h3>
                        
                        <div class="space-y-6">
                            <div class="flex items-start">
                                <div class="w-12 h-12 rounded-full bg-blue-600 flex items-center justify-center mr-4 flex-shrink-0">
                                    <i class="fas fa-map-marker-alt text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold mb-1">地址</h4>
                                    <p class="text-gray-300">广州市白云区江夏</p>
                                </div>
                            </div>
                            
                            <div class="flex items-start">
                                <div class="w-12 h-12 rounded-full bg-blue-600 flex items-center justify-center mr-4 flex-shrink-0">
                                    <i class="fas fa-envelope text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold mb-1">邮箱</h4>
                                    <p class="text-gray-300">moquiet@foxmail.com</p>
                                </div>
                            </div>
                            
                            <div class="flex items-start">
                                <div class="w-12 h-12 rounded-full bg-blue-600 flex items-center justify-center mr-4 flex-shrink-0">
                                    <i class="fas fa-phone-alt text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold mb-1">电话</h4>
                                    <p class="text-gray-300">+86 13501479737</p>
                                </div>
                            </div>
                            
                            <div class="flex items-start">
                                <div class="w-12 h-12 rounded-full bg-blue-600 flex items-center justify-center mr-4 flex-shrink-0">
                                    <i class="fas fa-clock text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold mb-1">工作时间</h4>
                                    <p class="text-gray-300">周一至周五: 9:00 - 18:00</p>
                                    <p class="text-gray-300">周六至周日: 休息</p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="mt-8">
                            <h4 class="font-bold mb-4">关注我</h4>
                            <div class="flex gap-4">
                                <a href="#" class="w-10 h-10 rounded-full bg-blue-600 flex items-center justify-center hover:bg-blue-700 transition-colors">
                                    <i class="fab fa-behance"></i>
                                </a>
                                <a href="#" class="w-10 h-10 rounded-full bg-blue-400 flex items-center justify-center hover:bg-blue-500 transition-colors">
                                    <i class="fab fa-dribbble"></i>
                                </a>
                                <a href="#" class="w-10 h-10 rounded-full bg-red-600 flex items-center justify-center hover:bg-red-700 transition-colors">
                                    <i class="fab fa-instagram"></i>
                                </a>
                                <a href="#" class="w-10 h-10 rounded-full bg-blue-800 flex items-center justify-center hover:bg-blue-900 transition-colors">
                                    <i class="fab fa-linkedin-in"></i>
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 页脚 -->
    <footer class="bg-black py-12">
        <div class="container mx-auto px-4">
            <div class="grid md:grid-cols-4 gap-8">
                <div>
                    <h3 class="text-2xl font-bold gradient-text mb-4">AI设计师</h3>
                    <p class="text-gray-400 mb-6">
                        专业的AI电商设计服务，为您的产品打造独特的视觉体验
                    </p>
                    <div class="flex gap-4">
                        <a href="#" class="text-gray-400 hover:text-white transition-colors">
                            <i class="fab fa-behance"></i>
                        </a>
                        <a href="#" class="text-gray-400 hover:text-white transition-colors">
                            <i class="fab fa-dribbble"></i>
                        </a>
                        <a href="#" class="text-gray-400 hover:text-white transition-colors">
                            <i class="fab fa-instagram"></i>
                        </a>
                        <a href="#" class="text-gray-400 hover:text-white transition-colors">
                            <i class="fab fa-linkedin-in"></i>
                        </a>
                    </div>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">服务</h4>
                    <ul class="space-y-2">
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">电商产品主图设计</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">详情页设计与优化</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">品牌视觉识别系统</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">产品短视频制作</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">社交媒体素材设计</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">快速链接</h4>
                    <ul class="space-y-2">
                        <li><a href="#home" class="text-gray-400 hover:text-white transition-colors">首页</a></li>
                        <li><a href="#services" class="text-gray-400 hover:text-white transition-colors">服务</a></li>
                        <li><a href="#ai-tool" class="text-gray-400 hover:text-white transition-colors">AI工具</a></li>
                        <li><a href="#portfolio" class="text-gray-400 hover:text-white transition-colors">作品</a></li>
                        <li><a href="#about" class="text-gray-400 hover:text-white transition-colors">关于</a></li>
                        <li><a href="#contact" class="text-gray-400 hover:text-white transition-colors">联系</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">订阅</h4>
                    <p class="text-gray-400 mb-4">
                        订阅我的新闻通讯，获取最新的AI设计资讯和优惠信息
                    </p>
                    <form class="flex">
                        <input type="email" placeholder="您的邮箱" class="bg-gray-800 border-none rounded-l-lg px-4 py-2 w-full focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded-r-lg hover:bg-blue-700 transition-colors">
                            <i class="fas fa-paper-plane"></i>
                        </button>
                    </form>
                </div>
            </div>
            
            <div class="border-t border-gray-800 mt-12 pt-8 flex flex-col md:flex-row justify-between items-center">
                <p class="text-gray-400 text-sm mb-4 md:mb-0">
                    © 2023 AI设计师. 保留所有权利.
                </p>
                <div class="flex gap-6">
                    <a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">隐私政策</a>
                    <a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">服务条款</a>
                    <a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Cookie政策</a>
                </div>
            </div>
        </div>
    </footer>

    <!-- 灵动岛 -->
    <div class="dynamic-island">
        <i class="fas fa-lightbulb text-yellow-400"></i>
        <span>需要设计服务？</span>
        <a href="#contact" class="bg-blue-600 text-white px-4 py-1 rounded-full text-sm hover:bg-blue-700 transition-colors">联系我</a>
    </div>

    <script>
        // 页面加载完成后执行
        document.addEventListener('DOMContentLoaded', function() {
            // 隐藏加载动画
            setTimeout(() => {
                document.querySelector('.loader').classList.add('hidden');
            }, 1000);
            
            // 初始化Three.js背景
            initThreeBackground();
            
            // 初始化滚动动画
            initScrollAnimations();
            
            // 初始化导航栏滚动效果
            initNavbarScroll();
            
            // 初始化移动端菜单
            initMobileMenu();
            
            // 初始化作品筛选
            initPortfolioFilter();
            
            // 初始化AI预览工具
            initAiPreviewTool();
            
            // 初始化平滑滚动
            initSmoothScroll();
        });
        
        // Three.js背景
        function initThreeBackground() {
            const canvas = document.getElementById('hero-canvas');
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            
            const renderer = new THREE.WebGLRenderer({
                canvas: canvas,
                alpha: true,
                antialias: true
            });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(window.devicePixelRatio);
            
            // 创建粒子
            const particlesGeometry = new THREE.BufferGeometry();
            const particlesCount = 1500;
            
            const posArray = new Float32Array(particlesCount * 3);
            
            for(let i = 0; i < particlesCount * 3; i++) {
                posArray[i] = (Math.random() - 0.5) * 10;
            }
            
            particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
            
            const particlesMaterial = new THREE.PointsMaterial({
                size: 0.02,
                color: 0x0066ff,
                transparent: true,
                opacity: 0.8
            });
            
            const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
            scene.add(particlesMesh);
            
            camera.position.z = 5;
            
            // 动画
            function animate() {
                requestAnimationFrame(animate);
                
                particlesMesh.rotation.y += 0.001;
                particlesMesh.rotation.x += 0.0005;
                
                renderer.render(scene, camera);
            }
            
            animate();
            
            // 响应窗口大小变化
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
            
            // 鼠标移动效果
            document.addEventListener('mousemove', (event) => {
                const mouseX = (event.clientX / window.innerWidth) * 2 - 1;
                const mouseY = -(event.clientY / window.innerHeight) * 2 + 1;
                
                gsap.to(particlesMesh.rotation, {
                    x: mouseY * 0.1,
                    y: mouseX * 0.1,
                    duration: 2
                });
            });
        }
        
        // 滚动动画
        function initScrollAnimations() {
            const fadeElements = document.querySelectorAll('.fade-in');
            
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('active');
                    }
                });
            }, {
                threshold: 0.1
            });
            
            fadeElements.forEach(element => {
                observer.observe(element);
            });
        }
        
        // 导航栏滚动效果
        function initNavbarScroll() {
            const navbar = document.getElementById('navbar');
            
            window.addEventListener('scroll', () => {
                if (window.scrollY > 50) {
                    navbar.classList.add('bg-black', 'bg-opacity-80');
                    navbar.classList.remove('bg-transparent');
                } else {
                    navbar.classList.remove('bg-black', 'bg-opacity-80');
                    navbar.classList.add('bg-transparent');
                }
            });
        }
        
        // 移动端菜单
        function initMobileMenu() {
            const menuToggle = document.getElementById('menu-toggle');
            const menuClose = document.getElementById('menu-close');
            const mobileMenu = document.querySelector('.mobile-menu');
            const menuOverlay = document.querySelector('.menu-overlay');
            const mobileNavLinks = document.querySelectorAll('.mobile-nav-link');
            
            menuToggle.addEventListener('click', () => {
                mobileMenu.classList.add('active');
                menuOverlay.classList.add('active');
                document.body.style.overflow = 'hidden';
            });
            
            function closeMenu() {
                mobileMenu.classList.remove('active');
                menuOverlay.classList.remove('active');
                document.body.style.overflow = '';
            }
            
            menuClose.addEventListener('click', closeMenu);
            menuOverlay.addEventListener('click', closeMenu);
            
            mobileNavLinks.forEach(link => {
                link.addEventListener('click', closeMenu);
            });
        }
        
        // 作品筛选
        function initPortfolioFilter() {
            const filterButtons = document.querySelectorAll('.portfolio-filter');
            const portfolioItems = document.querySelectorAll('.portfolio-item');
            
            filterButtons.forEach(button => {
                button.addEventListener('click', () => {
                    // 移除所有按钮的active类
                    filterButtons.forEach(btn => {
                        btn.classList.remove('bg-blue-600');
                        btn.classList.add('bg-transparent', 'border', 'border-white');
                    });
                    
                    // 添加当前按钮的active类
                    button.classList.add('bg-blue-600');
                    button.classList.remove('bg-transparent', 'border', 'border-white');
                    
                    const filter = button.getAttribute('data-filter');
                    
                    portfolioItems.forEach(item => {
                        if (filter === 'all' || item.getAttribute('data-category') === filter) {
                            item.style.display = 'block';
                        } else {
                            item.style.display = 'none';
                        }
                    });
                });
            });
        }
        
        // AI预览工具
        function initAiPreviewTool() {
            const uploadArea = document.getElementById('upload-area');
            const fileInput = document.getElementById('product-image');
            const generateBtn = document.getElementById('generate-btn');
            const previewPlaceholder = document.getElementById('preview-placeholder');
            const previewResult = document.getElementById('preview-result');
            const resultImage = document.getElementById('result-image');
            const previewLoading = document.getElementById('preview-loading');
            const downloadBtn = document.getElementById('download-btn');
            const shareBtn = document.getElementById('share-btn');
            const styleOptions = document.querySelectorAll('.style-option');
            const sceneOptions = document.querySelectorAll('.scene-option');
            
            // 上传区域点击事件
            uploadArea.addEventListener('click', () => {
                fileInput.click();
            });
            
            // 拖拽上传
            uploadArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                uploadArea.classList.add('border-blue-500', 'bg-blue-900', 'bg-opacity-20');
            });
            
            uploadArea.addEventListener('dragleave', () => {
                uploadArea.classList.remove('border-blue-500', 'bg-blue-900', 'bg-opacity-20');
            });
            
            uploadArea.addEventListener('drop', (e) => {
                e.preventDefault();
                uploadArea.classList.remove('border-blue-500', 'bg-blue-900', 'bg-opacity-20');
                
                if (e.dataTransfer.files.length) {
                    fileInput.files = e.dataTransfer.files;
                    handleFileUpload(e.dataTransfer.files[0]);
                }
            });
            
            // 文件选择事件
            fileInput.addEventListener('change', () => {
                if (fileInput.files.length) {
                    handleFileUpload(fileInput.files[0]);
                }
            });
            
            // 处理文件上传
            function handleFileUpload(file) {
                if (!file.type.match('image.*')) {
                    alert('请上传图片文件');
                    return;
                }
                
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    // 这里可以显示上传的图片预览
                    // 为了简化，我们直接启用生成按钮
                    generateBtn.disabled = false;
                };
                
                reader.readAsDataURL(file);
            }
            
            // 样式选择
            styleOptions.forEach(option => {
                option.addEventListener('click', () => {
                    styleOptions.forEach(opt => opt.classList.remove('active', 'border-blue-500'));
                    option.classList.add('active', 'border-blue-500');
                });
            });
            
            // 场景选择
            sceneOptions.forEach(option => {
                option.addEventListener('click', () => {
                    sceneOptions.forEach(opt => opt.classList.remove('active', 'border-blue-500'));
                    option.classList.add('active', 'border-blue-500');
                });
            });
            
            // 生成预览
            generateBtn.addEventListener('click', () => {
                if (!fileInput.files.length) {
                    alert('请先上传产品图片');
                    return;
                }
                
                // 显示加载状态
                previewPlaceholder.style.display = 'none';
                previewResult.style.display = 'none';
                previewLoading.style.display = 'flex';
                
                // 模拟AI生成过程
                setTimeout(() => {
                    // 隐藏加载状态，显示结果
                    previewLoading.style.display = 'none';
                    previewResult.style.display = 'block';
                    
                    // 获取选中的样式和场景
                    const selectedStyle = document.querySelector('.style-option.active').getAttribute('data-style');
                    const selectedScene = document.querySelector('.scene-option.active').getAttribute('data-scene');
                    
                    // 根据选择的样式和场景设置结果图片
                    // 这里使用预设的图片作为示例
                    let resultImageUrl = '';
                    
                    // 根据不同的组合选择不同的示例图片
                    if (selectedStyle === 'modern' && selectedScene === 'studio') {
                        resultImageUrl = 'https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/22b85ffa08094c138049bc0bdfb6f990~tplv-a9rns2rl98-image.image?lk3s=8e244e95&rcl=20260228172422E381F39E4B09C7921E2A&rrcfp=f06b921b&x-expires=1774862700&x-signature=wASp55yLDwr%2BZSSJmuAyOG8LAng%3D';
                    } else if (selectedStyle === 'elegant' && selectedScene === 'home') {
                        resultImageUrl = 'https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/0573336e481a40948f8770f21094f173~tplv-a9rns2rl98-image.image?lk3s=8e244e95&rcl=20260228172422E381F39E4B09C7921E2A&rrcfp=f06b921b&x-expires=1774862700&x-signature=422k3rqYv%2Bv7GzW3m43%2F1j5rBw%3D';
                    } else if (selectedStyle === 'futuristic' && selectedScene === 'office') {
                        resultImageUrl = 'https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/e7b96c8af7c44f1594570a9259f161e3~tplv-a9rns2rl98-image.image?lk3s=8e244e95&rcl=20260228172422E381F39E4B09C7921E2A&rrcfp=f06b921b&x-expires=1774862703&x-signature=%2F7MvUQHpi72VIEYbSnPrWhU3u5w%3D';
                    } else {
                        // 默认图片
                        resultImageUrl = 'https://p3-doubao-search-sign.byteimg.com/labis/2a6f97976868e404be6f12f0e28290f1~tplv-be4g95zd3a-image.jpeg?lk3s=feb11e32&x-expires=1787822675&x-signature=51frPvxtJ1PUhNGuDrBB0blnCNE%3D';
                    }
                    
                    resultImage.src = resultImageUrl;
                    
                    // 显示下载和分享按钮
                    downloadBtn.style.display = 'inline-block';
                    shareBtn.style.display = 'inline-block';
                }, 2000);
            });
            
            // 下载功能
            downloadBtn.addEventListener('click', () => {
                const link = document.createElement('a');
                link.href = resultImage.src;
                link.download = 'ai-design-preview.jpg';
                link.click();
            });
            
            // 分享功能
            shareBtn.addEventListener('click', () => {
                if (navigator.share) {
                    navigator.share({
                        title: 'AI设计预览效果',
                        text: '查看我使用AI设计师预览工具生成的设计效果！',
                        url: window.location.href
                    });
                } else {
                    // 复制链接到剪贴板
                    navigator.clipboard.writeText(window.location.href).then(() => {
                        alert('链接已复制到剪贴板');
                    });
                }
            });
        }
        
        // 平滑滚动
        function initSmoothScroll() {
            const navLinks = document.querySelectorAll('a[href^="#"]');
            
            navLinks.forEach(link => {
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    
                    const targetId = link.getAttribute('href');
                    const targetElement = document.querySelector(targetId);
                    
                    if (targetElement) {
                        window.scrollTo({
                            top: targetElement.offsetTop - 80,
                            behavior: 'smooth'
                        });
                    }
                });
            });
        }
    </script>

</body></html>

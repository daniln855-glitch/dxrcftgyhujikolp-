<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LIRISHA - Мир прекрасного</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --primary-color: #e91e63;
            --secondary-color: #f8bbd9;
            --accent-color: #ad1457;
            --text-color: #333;
            --light-text: #fff;
            --dark-bg: #2c3e50;
            --section-bg: #f9f9f9;
            --card-bg: #ffffff;
            --nav-bg: rgba(255, 255, 255, 0.95);
            --border-color: #e1e5e9;
            --hero-bg: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
        }

        /* Темная тема */
        [data-theme="dark"] {
            --primary-color: #ff4081;
            --secondary-color: #7b1fa2;
            --accent-color: #f50057;
            --text-color: #e0e0e0;
            --light-text: #ffffff;
            --dark-bg: #121212;
            --section-bg: #1e1e1e;
            --card-bg: #2d2d2d;
            --nav-bg: rgba(30, 30, 30, 0.95);
            --border-color: #444;
            --hero-bg: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
        }

        body {
            background: var(--section-bg);
            color: var(--text-color);
            overflow-x: hidden;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Навигация */
        nav {
            background: var(--nav-bg);
            backdrop-filter: blur(10px);
            padding: 1.2rem 2rem;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
            border-bottom: 1px solid var(--border-color);
            transition: all 0.3s ease;
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1400px;
            margin: 0 auto;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary-color);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .logo i {
            font-size: 1.5rem;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            align-items: center;
        }

        .nav-links a {
            text-decoration: none;
            color: var(--text-color);
            font-weight: 600;
            padding: 0.5rem 1rem;
            border-radius: 25px;
            transition: all 0.3s ease;
            position: relative;
        }

        .nav-links a:hover,
        .nav-links a.active {
            color: var(--primary-color);
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            width: 0;
            height: 2px;
            background: var(--primary-color);
            transition: all 0.3s ease;
            transform: translateX(-50%);
        }

        .nav-links a:hover::after,
        .nav-links a.active::after {
            width: 80%;
        }

        /* Переключатель темы */
        .theme-toggle {
            background: none;
            border: none;
            color: var(--text-color);
            font-size: 1.2rem;
            cursor: pointer;
            padding: 0.5rem;
            border-radius: 50%;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
        }

        .theme-toggle:hover {
            background: var(--primary-color);
            color: white;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--primary-color);
        }

        /* Страницы */
        .page {
            display: none;
            padding: 100px 2rem 2rem;
            max-width: 1400px;
            margin: 0 auto;
            min-height: 100vh;
        }

        .page.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Герой секция */
        .hero {
            height: 90vh;
            display: flex;
            align-items: center;
            padding: 0 2rem;
            background: var(--hero-bg);
            border-radius: 20px;
            margin-bottom: 3rem;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .hero-content {
            flex: 1;
            padding: 3rem;
            z-index: 2;
        }

        .hero-image {
            flex: 1;
            height: 100%;
            position: relative;
        }

        .hero-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 0 20px 20px 0;
        }

        .hero h1 {
            font-size: 4rem;
            margin-bottom: 1rem;
            color: var(--text-color);
            line-height: 1.1;
        }

        .hero .subtitle {
            font-size: 1.8rem;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
            font-weight: 300;
        }

        .hero p {
            font-size: 1.2rem;
            line-height: 1.6;
            margin-bottom: 2.5rem;
            max-width: 600px;
            color: var(--text-color);
            opacity: 0.8;
        }

        /* Кнопки */
        .btn {
            padding: 1rem 2.5rem;
            background: var(--primary-color);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(233, 30, 99, 0.3);
            text-decoration: none;
            display: inline-block;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(233, 30, 99, 0.4);
            background: var(--accent-color);
        }

        .btn-secondary {
            background: transparent;
            border: 2px solid var(--primary-color);
            color: var(--primary-color);
            margin-left: 1rem;
        }

        .btn-secondary:hover {
            background: var(--primary-color);
            color: white;
        }

        /* Секции */
        .section-title {
            text-align: center;
            font-size: 3rem;
            margin-bottom: 3rem;
            color: var(--primary-color);
            position: relative;
        }

        .section-title::after {
            content: '';
            display: block;
            width: 100px;
            height: 4px;
            background: var(--primary-color);
            margin: 1rem auto;
            border-radius: 2px;
        }

        /* Галерея */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .gallery-item {
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            height: 400px;
            position: relative;
            background: var(--card-bg);
        }

        .gallery-item:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
        }

        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.3s ease;
        }

        .gallery-item:hover img {
            transform: scale(1.05);
        }

        .gallery-caption {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(transparent, rgba(0,0,0,0.8));
            color: white;
            padding: 2rem 1rem 1rem;
            transform: translateY(100%);
            transition: transform 0.3s ease;
        }

        .gallery-item:hover .gallery-caption {
            transform: translateY(0);
        }

        /* О себе */
        .about-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
            margin-top: 3rem;
        }

        .about-text {
            font-size: 1.1rem;
            line-height: 1.8;
            color: var(--text-color);
            opacity: 0.8;
        }

        .about-text p {
            margin-bottom: 1.5rem;
        }

        .about-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 2rem;
            margin-top: 2rem;
        }

        .stat-item {
            text-align: center;
            padding: 2rem;
            background: var(--card-bg);
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease;
            border: 1px solid var(--border-color);
        }

        .stat-item:hover {
            transform: translateY(-5px);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 0.5rem;
        }

        .stat-label {
            color: var(--text-color);
            opacity: 0.8;
            font-weight: 500;
        }

        /* Хобби */
        .hobbies-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .hobby-card {
            background: var(--card-bg);
            border-radius: 15px;
            padding: 2.5rem 2rem;
            text-align: center;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease;
            border-top: 4px solid var(--primary-color);
            border: 1px solid var(--border-color);
        }

        .hobby-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
        }

        .hobby-icon {
            font-size: 3rem;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
        }

        .hobby-card h3 {
            margin-bottom: 1rem;
            color: var(--text-color);
        }

        .hobby-card p {
            color: var(--text-color);
            opacity: 0.8;
            line-height: 1.6;
        }

        /* Достижения */
        .timeline {
            position: relative;
            max-width: 800px;
            margin: 3rem auto;
        }

        .timeline::before {
            content: '';
            position: absolute;
            left: 50%;
            top: 0;
            bottom: 0;
            width: 2px;
            background: var(--primary-color);
            transform: translateX(-50%);
        }

        .timeline-item {
            margin-bottom: 3rem;
            position: relative;
            width: 45%;
        }

        .timeline-item:nth-child(odd) {
            left: 0;
        }

        .timeline-item:nth-child(even) {
            left: 55%;
        }

        .timeline-content {
            background: var(--card-bg);
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            position: relative;
            border: 1px solid var(--border-color);
        }

        .timeline-content::before {
            content: '';
            position: absolute;
            top: 20px;
            width: 20px;
            height: 20px;
            background: var(--primary-color);
            border-radius: 50%;
        }

        .timeline-item:nth-child(odd) .timeline-content::before {
            right: -50px;
        }

        .timeline-item:nth-child(even) .timeline-content::before {
            left: -50px;
        }

        .timeline-date {
            color: var(--primary-color);
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        /* Контакты */
        .contact-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            margin-top: 3rem;
        }

        .contact-info {
            background: var(--card-bg);
            padding: 3rem;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
            border: 1px solid var(--border-color);
        }

        .contact-item {
            display: flex;
            align-items: center;
            margin-bottom: 2rem;
            padding: 1rem;
            border-radius: 10px;
            transition: background 0.3s ease;
        }

        .contact-item:hover {
            background: var(--section-bg);
        }

        .contact-icon {
            font-size: 1.5rem;
            color: var(--primary-color);
            margin-right: 1rem;
            width: 40px;
        }

        .contact-form {
            background: var(--card-bg);
            padding: 3rem;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
            border: 1px solid var(--border-color);
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--text-color);
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 1rem;
            border: 2px solid var(--border-color);
            border-radius: 10px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
            background: var(--section-bg);
            color: var(--text-color);
        }

        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        .form-group textarea {
            height: 150px;
            resize: vertical;
        }

        /* Футер */
        footer {
            background: var(--dark-bg);
            color: white;
            text-align: center;
            padding: 3rem 2rem;
            margin-top: 5rem;
            border-radius: 20px 20px 0 0;
        }

        .footer-content {
            max-width: 1200px;
            margin: 0 auto;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            margin: 2rem 0;
        }

        .social-link {
            width: 50px;
            height: 50px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            text-decoration: none;
            font-size: 1.2rem;
            transition: all 0.3s ease;
        }

        .social-link:hover {
            background: var(--primary-color);
            transform: translateY(-3px);
        }

        /* Адаптивность */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
                position: absolute;
                top: 100%;
                left: 0;
                right: 0;
                background: var(--nav-bg);
                flex-direction: column;
                padding: 1rem;
                box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            }

            .nav-links.active {
                display: flex;
            }

            .mobile-menu-btn {
                display: block;
            }

            .hero {
                flex-direction: column;
                height: auto;
                text-align: center;
            }

            .hero-content {
                padding: 2rem 1rem;
            }

            .hero h1 {
                font-size: 2.5rem;
            }

            .hero .subtitle {
                font-size: 1.4rem;
            }

            .about-content {
                grid-template-columns: 1fr;
                gap: 2rem;
            }

            .contact-container {
                grid-template-columns: 1fr;
                gap: 2rem;
            }

            .timeline::before {
                left: 30px;
            }

            .timeline-item {
                width: calc(100% - 80px);
                left: 80px !important;
            }

            .timeline-content::before {
                left: -50px !important;
            }
        }

        /* Утилиты */
        .text-center {
            text-align: center;
        }
        
        .mt-2 { margin-top: 2rem; }
        .mt-3 { margin-top: 3rem; }
        .mb-2 { margin-bottom: 2rem; }
        .mb-3 { margin-bottom: 3rem; }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>
    <!-- Навигация -->
    <nav>
        <div class="nav-container">
            <div class="logo">
                <i class="fas fa-star"></i>
                LIRISHA|KWEUAGA
            </div>
            <div class="nav-links" id="navLinks">
                <a href="#" class="nav-link active" data-page="home">Главная</a>
                <a href="#" class="nav-link" data-page="gallery">Галерея</a>
                <a href="#" class="nav-link" data-page="about">Обо мне</a>
                <a href="#" class="nav-link" data-page="hobbies">Увлечения</a>
                <a href="#" class="nav-link" data-page="achievements">Достижения</a>
                <a href="#" class="nav-link" data-page="blog">Блог</a>
                <a href="#" class="nav-link" data-page="contact">Контакты</a>
                <button class="theme-toggle" id="themeToggle" title="Переключить тему">
                    <i class="fas fa-moon"></i>
                </button>
            </div>
            <button class="mobile-menu-btn" id="mobileMenuBtn">
                <i class="fas fa-bars"></i>
            </button>
        </div>
    </nav>

    <!-- Главная страница -->
    <div id="home" class="page active">
        <div class="hero">
            <div class="hero-content">
                <h1>Привет, я <span style="color: var(--primary-color);">Лера</span></h1>
                <div class="subtitle">Творческая личность & Мечтательница</div>
                <p>Добро пожаловать в мой мир! Здесь вы найдете историю моей жизни, увлечения, достижения и многое другое. Я верю, что каждый день - это новая возможность творить и вдохновлять.</p>
                <div>
                    <button class="btn" onclick="showPage('gallery')">
                        <i class="fas fa-images"></i> Смотреть галерею
                    </button>
                    <button class="btn btn-secondary" onclick="showPage('contact')">
                        <i class="fas fa-envelope"></i> Связаться со мной
                    </button>
                </div>
            </div>
            <div class="hero-image">
                <img src="https://source.unsplash.com/random/800x1000/?portrait,woman" alt="Портрет">
            </div>
        </div>

        <div class="text-center mt-3">
            <h2 class="section-title">Мир в моем восприятии</h2>
            <p style="font-size: 1.2rem; max-width: 800px; margin: 0 auto 3rem; line-height: 1.6; color: var(--text-color); opacity: 0.8;">
                Красота в деталях, искусство в повседневности, а вдохновение - во всем, что меня окружает. 
                Я нахожу радость в простых вещах и делюсь этим с миром.
            </p>
        </div>

        <div class="hobbies-grid">
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-camera"></i>
                </div>
                <h3>Фотография</h3>
                <p>Запечатлеваю моменты, которые рассказывают истории без слов. От портретов до пейзажей - каждый кадр особенный.</p>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-paint-brush"></i>
                </div>
                <h3>Рисование</h3>
                <p>Превращаю холст в мир эмоций и цветов. Акварель, масло, цифровая графика - каждая техника по-своему уникальна.</p>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-book"></i>
                </div>
                <h3>Писательство</h3>
                <p>Слова - это мои кисти, а страницы - холсты. Пишу рассказы, стихи и мысли, которые рождаются в тишине.</p>
            </div>
        </div>
    </div>

    <!-- Галерея -->
    <div id="gallery" class="page">
        <h2 class="section-title">Моя галерея</h2>
        <p style="text-align: center; font-size: 1.2rem; color: var(--text-color); opacity: 0.8; margin-bottom: 3rem; max-width: 800px; margin-left: auto; margin-right: auto;">
            Взгляд через объектив, моменты жизни, застывшие во времени. Каждая фотография - это часть моей истории.
        </p>
        
        <div class="gallery-grid">
            <div class="gallery-item">
                <img src="https://source.unsplash.com/random/600x800/?portrait,woman" alt="Портрет 1">
                <div class="gallery-caption">
                    <h4>Утренние мысли</h4>
                    <p>Тихий момент с чашкой кофе</p>
                </div>
            </div>
            <div class="gallery-item">
                <img src="https://source.unsplash.com/random/600x800/?nature,woman" alt="На природе">
                <div class="gallery-caption">
                    <h4>Единение с природой</h4>
                    <p>Прогулки по лесу вдохновляют</p>
                </div>
            </div>
            <div class="gallery-item">
                <img src="https://ibb.co/r2ck2Wx5" alt="Творчество">
                <div class="gallery-caption">
                    <h4>В процессе творения</h4>
                    <p>Работа над новым проектом</p>
                </div>
            </div>
            <div class="gallery-item">
                <img src="https://source.unsplash.com/random/600x800/?city,woman" alt="Город">
                <div class="gallery-caption">
                    <h4>Городские истории</h4>
                    <p>Улицы, которые рассказывают истории</p>
                </div>
            </div>
            <div class="gallery-item">
                <img src="https://source.unsplash.com/random/600x800/?travel,woman" alt="Путешествия">
                <div class="gallery-caption">
                    <h4>Дорога зовет</h4>
                    <p>Новые места, новые впечатления</p>
                </div>
            </div>
            <div class="gallery-item">
                <img src="https://source.unsplash.com/random/600x800/?studio,woman" alt="Студия">
                <div class="gallery-caption">
                    <h4>В творческой студии</h4>
                    <p>Место, где рождаются идеи</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Обо мне -->
    <div id="about" class="page">
        <h2 class="section-title">Обо мне</h2>
        
        <div class="about-content">
            <div>
                <div class="about-text">
                    <p>
                        Привет! Меня зовут Лера, и я творческая личность с безграничной любовью к искусству и красоте. 
                        С детства меня привлекало все, что связано с творческим самовыражением - от рисования до фотографии.
                    </p>
                    <p>
                        Я верю, что каждый человек обладает уникальным взглядом на мир, и мой - через призму искусства и эстетики. 
                        В своих работах я стараюсь передать не только видимую красоту, но и эмоции, истории, моменты.
                    </p>
                    <p>
                        Помимо творчества, я увлекаюсь психологией, философией и путешествиями. 
                        Эти увлечения помогают мне глубже понимать людей и мир вокруг, что находит отражение в моих проектах.
                    </p>
                </div>
                
                <div class="about-stats">
                    <div class="stat-item">
                        <div class="stat-number">150+</div>
                        <div class="stat-label">Завершенных проектов</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number">5</div>
                        <div class="stat-label">Лет опыта</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number">25</div>
                        <div class="stat-label">Выставок</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number">12</div>
                        <div class="stat-label">Стран посещено</div>
                    </div>
                </div>
            </div>
            
            <div>
                <div class="gallery-item" style="height: 500px;">
                    <img src="https://source.unsplash.com/random/600x800/?artist,woman" alt="Обо мне">
                </div>
            </div>
        </div>
        
        <div class="mt-3">
            <h3 style="text-align: center; margin-bottom: 2rem; color: var(--primary-color);">Мои принципы</h3>
            <div class="hobbies-grid">
                <div class="hobby-card">
                    <h3>Аутентичность</h3>
                    <p>Быть собой в каждом моменте и каждой работе. Искренность - ключ к настоящему искусству.</p>
                </div>
                <div class="hobby-card">
                    <h3>Развитие</h3>
                    <p>Постоянное обучение и рост. Каждый день - новая возможность стать лучше.</p>
                </div>
                <div class="hobby-card">
                    <h3>Вдохновение</h3>
                    <p>Находить красоту в обыденном и делиться этим с миром через свое творчество.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Увлечения -->
    <div id="hobbies" class="page">
        <h2 class="section-title">Мои увлечения</h2>
        <p style="text-align: center; font-size: 1.2rem; color: var(--text-color); opacity: 0.8; margin-bottom: 3rem; max-width: 800px; margin-left: auto; margin-right: auto;">
            То, что наполняет мою жизнь смыслом, радостью и вдохновением. Каждое увлечение - это часть меня.
        </p>
        
        <div class="hobbies-grid">
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-camera-retro"></i>
                </div>
                <h3>Фотография</h3>
                <p>Пленочная и цифровая фотография. Люблю портреты, уличную и художественную съемку.</p>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-palette"></i>
                </div>
                <h3>Живопись</h3>
                <p>Работа с акрилом, маслом и акварелью. Создаю абстрактные и реалистичные работы.</p>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-book-open"></i>
                </div>
                <h3>Чтение</h3>
                <p>Художественная литература, психология, философия. Любимые авторы: [список авторов].</p>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-hiking"></i>
                </div>
                <h3>Путешествия</h3>
                <p>Исследую новые культуры, природу и архитектуру. Предпочитаю самостоятельные маршруты.</p>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-utensils"></i>
                </div>
                <h3>Кулинария</h3>
                <p>Экспериментирую с рецептами, особенно люблю азиатскую и итальянскую кухни.</p>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-music"></i>
                </div>
                <h3>Музыка</h3>
                <p>Игра на гитаре, коллекционирование виниловых пластинок, посещение концертов.</p>
            </div>
        </div>
    </div>

    <!-- Достижения -->
    <div id="achievements" class="page">
        <h2 class="section-title">Мои достижения</h2>
        
        <div class="timeline">
            <div class="timeline-item">
                <div class="timeline-content">
                    <div class="timeline-date">2023</div>
                    <h3>Персональная выставка "Отражения"</h3>
                    <p>Успешная организация и проведение первой персональной выставки в галерее современного искусства. Представлено 25 работ.</p>
                </div>
            </div>
            <div class="timeline-item">
                <div class="timeline-content">
                    <div class="timeline-date">2022</div>
                    <h3>Публикация фотокниги "Городские сны"</h3>
                    <p>Издание авторской фотокниги с урбанистическими пейзажами. Тираж распродан за 3 месяца.</p>
                </div>
            </div>
            <div class="timeline-item">
                <div class="timeline-content">
                    <div class="timeline-date">2021</div>
                    <h3>Победа в конкурсе "Молодой фотограф года"</h3>
                    <p>Первое место в национальном конкурсе фотографии в номинации "Арт-фотография".</p>
                </div>
            </div>
            <div class="timeline-item">
                <div class="timeline-content">
                    <div class="timeline-date">2020</div>
                    <h3>Завершение художественного образования</h3>
                    <p>Окончание [Название Университета] по специальности "Изобразительное искусство" с отличием.</p>
                </div>
            </div>
            <div class="timeline-item">
                <div class="timeline-content">
                    <div class="timeline-date">2019</div>
                    <h3>Первая групповая выставка</h3>
                    <p>Участие в коллективной выставке молодых художников с серией работ "Внутренний мир".</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Блог -->
    <div id="blog" class="page">
        <h2 class="section-title">Мой блог</h2>
        <p style="text-align: center; font-size: 1.2rem; color: var(--text-color); opacity: 0.8; margin-bottom: 3rem; max-width: 800px; margin-left: auto; margin-right: auto;">
            Мысли, идеи, размышления и истории из моей творческой жизни. Делиться - значит вдохновлять.
        </p>
        
        <div class="gallery-grid">
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-feather"></i>
                </div>
                <h3>Искусство видеть</h3>
                <p>Как научиться замечать красоту в повседневности и превращать обычные моменты в искусство.</p>
                <button class="btn" style="margin-top: 1rem; width: 100%;">Читать</button>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-compass"></i>
                </div>
                <h3>Путь творца</h3>
                <p>Мой личный опыт преодоления творческих кризисов и поиска вдохновения.</p>
                <button class="btn" style="margin-top: 1rem; width: 100%;">Читать</button>
            </div>
            <div class="hobby-card">
                <div class="hobby-icon">
                    <i class="fas fa-heart"></i>
                </div>
                <h3>Любовь к процессу</h3>
                <p>Почему важно любить не только результат, но и сам процесс создания.</p>
                <button class="btn" style="margin-top: 1rem; width: 100%;">Читать</button>
            </div>
        </div>
    </div>

    <!-- Контакты -->
    <div id="contact" class="page">
        <h2 class="section-title">Свяжитесь со мной</h2>
        
        <div class="contact-container">
            <div class="contact-info">
                <h3 style="margin-bottom: 2rem; color: var(--primary-color);">Давайте общаться!</h3>
                
                <div class="contact-item">
                    <div class="contact-icon">
                        <i class="fas fa-envelope"></i>
                    </div>
                    <div>
                        <h4>Email</h4>
                        <p>lirisha021295@icloud.com</p>
                    </div>
                </div>
                
                <div class="contact-item">
                    <div class="contact-icon">
                        <i class="fas fa-phone"></i>
                    </div>
                    <div>
                        <h4>Телефон</h4>
                        <p>+7 (915) 682-77-70</p>
                    </div>
                </div>
                
                <div class="contact-item">
                    <div class="contact-icon">
                        <i class="fas fa-map-marker-alt"></i>
                    </div>
                    <div>
                        <h4>Адрес</h4>
                        <p>Донецк, Донецкая Народная Республика</p>
                    </div>
                </div>
                
                <div class="social-links" style="justify-content: flex-start; margin-top: 3rem;">
                    <a href="https://www.instagram.com/kweuaga/" class="social-link" target="_blank">
                        <i class="fab fa-instagram"></i>
                    </a>
                    <a href="https://t.me/kweuaga" class="social-link" target="_blank">
                        <i class="fab fa-telegram"></i>
                    </a>
                    <a href="https://www.pinterest.com/lirishabrand/" class="social-link" target="_blank">
                        <i class="fab fa-pinterest"></i>
                    </a>
                    <a href="https://www.vk.com/kweuaga" class="social-link" target="_blank">
                        <i class="fab fa-vk"></i>
                    </a>
                </div>
            </div>
            
            <div class="contact-form">
                <h3 style="margin-bottom: 2rem; color: var(--primary-color);">Напишите мне</h3>
                
                <div class="form-group">
                    <label for="name">Ваше имя</label>
                    <input type="text" id="name" placeholder="Как к вам обращаться?">
                </div>
                
                <div class="form-group">
                    <label for="email">Ваш email</label>
                    <input type="email" id="email" placeholder="example@email.com">
                </div>
                
                <div class="form-group">
                    <label for="subject">Тема сообщения</label>
                    <input type="text" id="subject" placeholder="О чем вы хотите поговорить?">
                </div>
                
                <div class="form-group">
                    <label for="message">Ваше сообщение</label>
                    <textarea id="message" placeholder="Напишите ваше сообщение здесь..."></textarea>
                </div>
                
                <button class="btn" style="width: 100%;">
                    <i class="fas fa-paper-plane"></i> Отправить сообщение
                </button>
            </div>
        </div>
    </div>

    <!-- Футер -->
    <footer>
        <div class="footer-content">
            <h3 style="margin-bottom: 1rem;">LIRISHA</h3>
            <p style="margin-bottom: 2rem; max-width: 600px; margin-left: auto; margin-right: auto;">
                Творчество - это моя страсть, искусство - мой язык, а вдохновение - мой путеводитель.
            </p>
           <div class="social-links">
    <a href="https://www.instagram.com/kweuaga/" class="social-link" target="_blank">
        <i class="fab fa-instagram"></i>
    </a>
    <a href="https://t.me/kweuaga" class="social-link" target="_blank">
        <i class="fab fa-telegram"></i>
    </a>
    <a href="https://www.pinterest.com/lirishabrand/" class="social-link" target="_blank">
        <i class="fab fa-pinterest"></i>
    </a>
    <a href="https://www.vk.com/kweuaga" class="social-link" target="_blank">
        <i class="fab fa-vk"></i>
    </a>
    <a href="https://www.youtube.com/@valerie-i8u7v" class="social-link" target="_blank">
        <i class="fab fa-youtube"></i>
    </a>
</div>
            <div style="margin-top: 2rem; color: #ccc;">
                <p>© LIRISHA SOCIAL BRAND GROUP COMPANY 2025. Все права защищены.</p>
            </div>
        </div>
    </footer>

    <script>
        // Управление темной темой
        const themeToggle = document.getElementById('themeToggle');
        const themeIcon = themeToggle.querySelector('i');
        
        // Проверяем сохраненную тему или системные настройки
        const savedTheme = localStorage.getItem('theme');
        const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
        
        if (savedTheme === 'dark' || (!savedTheme && systemPrefersDark)) {
            document.documentElement.setAttribute('data-theme', 'dark');
            themeIcon.className = 'fas fa-sun';
        } else {
            document.documentElement.setAttribute('data-theme', 'light');
            themeIcon.className = 'fas fa-moon';
        }
        
        // Переключение темы
        themeToggle.addEventListener('click', () => {
            const currentTheme = document.documentElement.getAttribute('data-theme');
            const newTheme = currentTheme === 'light' ? 'dark' : 'light';
            
            document.documentElement.setAttribute('data-theme', newTheme);
            localStorage.setItem('theme', newTheme);
            
            // Меняем иконку
            if (newTheme === 'dark') {
                themeIcon.className = 'fas fa-sun';
            } else {
                themeIcon.className = 'fas fa-moon';
            }
        });

        // Навигация между страницами
        function showPage(pageId) {
            // Скрыть все страницы
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // Показать выбранную страницу
            document.getElementById(pageId).classList.add('active');
            
            // Обновить активную ссылку в навигации
            document.querySelectorAll('.nav-link').forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('data-page') === pageId) {
                    link.classList.add('active');
                }
            });
            
            // Закрыть мобильное меню если открыто
            document.getElementById('navLinks').classList.remove('active');
            
            // Прокрутка к верху страницы
            window.scrollTo(0, 0);
        }

        // Мобильное меню
        document.getElementById('mobileMenuBtn').addEventListener('click', function() {
            document.getElementById('navLinks').classList.toggle('active');
        });

        // Навигация по ссылкам
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                const pageId = this.getAttribute('data-page');
                showPage(pageId);
            });
        });

        // Анимация появления элементов при прокрутке
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = 1;
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, observerOptions);

        // Наблюдаем за элементами для анимации
        document.addEventListener('DOMContentLoaded', function() {
            document.querySelectorAll('.hobby-card, .gallery-item, .stat-item, .timeline-content').forEach(el => {
                el.style.opacity = 0;
                el.style.transform = 'translateY(20px)';
                el.style.transition = 'opacity 0.5s, transform 0.5s';
                observer.observe(el);
            });
        });

        // Обработка формы
        document.querySelector('.contact-form .btn').addEventListener('click', function() {
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const subject = document.getElementById('subject').value;
            const message = document.getElementById('message').value;
            
            if (name && email && subject && message) {
                alert('Сообщение отправлено! Я свяжусь с вами в ближайшее время.');
                // Очистка формы
                document.getElementById('name').value = '';
                document.getElementById('email').value = '';
                document.getElementById('subject').value = '';
                document.getElementById('message').value = '';
            } else {
                alert('Пожалуйста, заполните все поля формы.');
            }
        });

        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', function() {
            showPage('home');
        });
    </script>
</body>
</html>

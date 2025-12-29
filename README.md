<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MinionStarsMarket - Магазин Звезд</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #ffd700;
            --secondary: #1a1a2e;
            --accent: #00b4d8;
            --success: #2ecc71;
            --text: #ffffff;
            --bg-dark: #0f0f23;
            --bg-card: #1e1e3a;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--bg-dark);
            color: var(--text);
            min-height: 100vh;
            padding: 20px;
            background-image: radial-gradient(circle at 20% 30%, rgba(255, 215, 0, 0.1) 0%, transparent 20%),
                              radial-gradient(circle at 80% 70%, rgba(0, 180, 216, 0.1) 0%, transparent 20%);
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: linear-gradient(135deg, var(--secondary), #2d2d4a);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            border: 2px solid var(--primary);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255, 215, 0, 0.1) 0%, transparent 70%);
            z-index: 0;
        }

        .header-content {
            position: relative;
            z-index: 1;
        }

        h1 {
            color: var(--primary);
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }

        .stars-icon {
            color: var(--primary);
            animation: twinkle 2s infinite;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .tagline {
            color: #aaa;
            font-size: 1.1rem;
            margin-bottom: 20px;
        }

        .user-info {
            display: flex;
            justify-content: space-between;
            background: var(--bg-card);
            padding: 15px;
            border-radius: 15px;
            margin-top: 15px;
            border: 1px solid rgba(255, 215, 0, 0.2);
        }

        .balance {
            text-align: center;
        }

        .balance-amount {
            font-size: 2rem;
            color: var(--primary);
            font-weight: bold;
        }

        .balance-label {
            color: #aaa;
            font-size: 0.9rem;
        }

        .referral-stats {
            display: flex;
            gap: 20px;
            justify-content: center;
        }

        .stat {
            text-align: center;
        }

        .stat-value {
            font-size: 1.5rem;
            color: var(--accent);
            font-weight: bold;
        }

        .stat-label {
            color: #aaa;
            font-size: 0.8rem;
        }

        .section-title {
            color: var(--primary);
            margin: 25px 0 15px;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .stars-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .star-card {
            background: var(--bg-card);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            transition: transform 0.3s, box-shadow 0.3s;
            border: 2px solid transparent;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .star-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.4);
            border-color: var(--primary);
        }

        .star-card.popular::before {
            content: 'ПОПУЛЯРНОЕ';
            position: absolute;
            top: 10px;
            right: -30px;
            background: var(--accent);
            color: white;
            padding: 5px 30px;
            transform: rotate(45deg);
            font-size: 0.8rem;
            font-weight: bold;
        }

        .star-icon {
            font-size: 3rem;
            color: var(--primary);
            margin-bottom: 15px;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .star-name {
            font-size: 1.3rem;
            margin-bottom: 10px;
            color: var(--primary);
        }

        .star-desc {
            color: #ccc;
            font-size: 0.9rem;
            margin-bottom: 15px;
            min-height: 60px;
        }

        .star-price {
            font-size: 1.8rem;
            color: var(--success);
            font-weight: bold;
            margin-bottom: 15px;
        }

        .buy-btn {
            background: linear-gradient(135deg, var(--primary), #ffaa00);
            color: var(--secondary);
            border: none;
            padding: 12px 25px;
            border-radius: 10px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
            font-size: 1rem;
        }

        .buy-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.5);
        }

        .referral-section {
            background: var(--bg-card);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
            border: 2px solid var(--accent);
        }

        .referral-title {
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--accent);
            margin-bottom: 20px;
            font-size: 1.3rem;
        }

        .referral-link-container {
            display: flex;
            margin-bottom: 20px;
            background: rgba(0, 180, 216, 0.1);
            border-radius: 10px;
            overflow: hidden;
        }

        #referralLink {
            flex-grow: 1;
            background: transparent;
            border: none;
            color: white;
            padding: 15px;
            font-size: 1rem;
        }

        .copy-btn {
            background: var(--accent);
            color: white;
            border: none;
            padding: 0 25px;
            cursor: pointer;
            font-weight: bold;
        }

        .referral-structure {
            margin-top: 25px;
        }

        .level {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
            margin-bottom: 10px;
            border-left: 4px solid var(--primary);
        }

        .level-number {
            background: var(--primary);
            color: var(--secondary);
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .level-reward {
            color: var(--success);
            font-weight: bold;
        }

        .history-section {
            background: var(--bg-card);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
        }

        .history-list {
            margin-top: 15px;
        }

        .history-item {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .history-item:last-child {
            border-bottom: none;
        }

        .history-amount {
            color: var(--success);
            font-weight: bold;
        }

        .history-date {
            color: #aaa;
            font-size: 0.9rem;
        }

        .footer {
            text-align: center;
            padding: 20px;
            color: #777;
            font-size: 0.9rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            margin-top: 20px;
        }

        .telegram-btn {
            background: #0088cc;
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin: 20px auto;
            font-size: 1rem;
            transition: all 0.3s;
        }

        .telegram-btn:hover {
            background: #0077b3;
            transform: scale(1.05);
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--success);
            color: white;
            padding: 15px 25px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            transform: translateX(150%);
            transition: transform 0.5s;
            z-index: 1000;
        }

        .notification.show {
            transform: translateX(0);
        }

        @media (max-width: 600px) {
            .stars-grid {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .user-info {
                flex-direction: column;
                gap: 15px;
            }
            
            .referral-stats {
                flex-wrap: wrap;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Шапка магазина -->
        <header class="header">
            <div class="header-content">
                <h1>
                    <i class="fas fa-star stars-icon"></i>
                    MinionStarsMarket
                    <i class="fas fa-star stars-icon"></i>
                </h1>
                <p class="tagline">Покупайте уникальные звезды и зарабатывайте на рефералах!</p>
                
                <div class="user-info">
                    <div class="balance">
                        <div class="balance-amount" id="userBalance">1,250 ★</div>
                        <div class="balance-label">Ваш баланс звезд</div>
                    </div>
                    
                    <div class="referral-stats">
                        <div class="stat">
                            <div class="stat-value" id="refCount">12</div>
                            <div class="stat-label">Рефералов</div>
                        </div>
                        <div class="stat">
                            <div class="stat-value" id="refEarned">350 ★</div>
                            <div class="stat-label">Заработано</div>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Каталог звезд -->
        <section class="catalog">
            <h2 class="section-title">
                <i class="fas fa-shopping-bag"></i>
                Каталог звезд
            </h2>
            
            <div class="stars-grid">
                <!-- Звезда 1 -->
                <div class="star-card">
                    <div class="star-icon">
                        <i class="fas fa-star"></i>
                    </div>
                    <h3 class="star-name">Обычная звезда</h3>
                    <p class="star-desc">Базовая звезда для начинающих коллекционеров. Идеальна для первого знакомства с космосом.</p>
                    <div class="star-price">100 ★</div>
                    <button class="buy-btn" onclick="buyStar(1)">
                        <i class="fas fa-shopping-cart"></i> Купить
                    </button>
                </div>
                
                <!-- Звезда 2 -->
                <div class="star-card popular">
                    <div class="star-icon">
                        <i class="fas fa-star"></i><i class="fas fa-star"></i>
                    </div>
                    <h3 class="star-name">Двойная звезда</h3>
                    <p class="star-desc">Пара гравитационно связанных звезд. Редкое явление в нашей галактике.</p>
                    <div class="star-price">250 ★</div>
                    <button class="buy-btn" onclick="buyStar(2)">
                        <i class="fas fa-shopping-cart"></i> Купить
                    </button>
                </div>
                
                <!-- Звезда 3 -->
                <div class="star-card">
                    <div class="star-icon">
                        <i class="fas fa-gem"></i>
                    </div>
                    <h3 class="star-name">Кристальная звезда</h3>
                    <p class="star-desc">Звезда с кристаллической структурой. Сияет всеми цветами радуги.</p>
                    <div class="star-price">500 ★</div>
                    <button class="buy-btn" onclick="buyStar(3)">
                        <i class="fas fa-shopping-cart"></i> Купить
                    </button>
                </div>
                
                <!-- Звезда 4 -->
                <div class="star-card">
                    <div class="star-icon">
                        <i class="fas fa-crown"></i>
                    </div>
                    <h3 class="star-name">Королевская звезда</h3>
                    <p class="star-desc">Элитная звезда для истинных ценителей. Самая яркая в коллекции.</p>
                    <div class="star-price">1,000 ★</div>
                    <button class="buy-btn" onclick="buyStar(4)">
                        <i class="fas fa-shopping-cart"></i> Купить
                    </button>
                </div>
            </div>
        </section>

        <!-- Реферальная система -->
        <section class="referral-section">
            <h2 class="referral-title">
                <i class="fas fa-users"></i>
                Реферальная система
            </h2>
            
            <p style="margin-bottom: 15px; color: #ccc;">
                Приглашайте друзей и получайте 10% от их покупок! Ваши рефералы также получают скидку 5% на первую покупку.
            </p>
            
            <div class="referral-link-container">
                <input type="text" id="referralLink" readonly value="https://t.me/MinionStarsMarketBot?start=ref_123456">
                <button class="copy-btn" onclick="copyReferralLink()">
                    <i class="fas fa-copy"></i> Копировать
                </button>
            </div>
            
            <div class="referral-structure">
                <h3 style="color: var(--accent); margin-bottom: 15px;">
                    <i class="fas fa-sitemap"></i> Уровни рефералов
                </h3>
                
                <div class="level">
                    <div class="level-info">
                        <div class="level-number">1</div>
                        <div style="margin-left: 15px;">
                            <div style="font-weight: bold;">Прямые рефералы</div>
                            <div style="color: #aaa; font-size: 0.9rem;">Ваши приглашенные друзья</div>
                        </div>
                    </div>
                    <div class="level-reward">10%</div>
                </div>
                
                <div class="level">
                    <div class="level-info">
                        <div class="level-number">2</div>
                        <div style="margin-left: 15px;">
                            <div style="font-weight: bold;">Рефералы 2-го уровня</div>
                            <div style="color: #aaa; font-size: 0.9rem;">Приглашенные вашими рефералами</div>
                        </div>
                    </div>
                    <div class="level-reward">5%</div>
                </div>
                
                <div class="level">
                    <div class="level-info">
                        <div class="level-number">3</div>
                        <div style="margin-left: 15px;">
                            <div style="font-weight: bold;">Рефералы 3-го уровня</div>
                            <div style="color: #aaa; font-size: 0.9rem;">Приглашенные рефералами 2-го уровня</div>
                        </div>
                    </div>
                    <div class="level-reward">2%</div>
                </div>
            </div>
        </section>

        <!-- История покупок -->
        <section class="history-section">
            <h2 class="section-title">
                <i class="fas fa-history"></i>
                История покупок
            </h2>
            
            <div class="history-list" id="purchaseHistory">
                <!-- История будет загружаться динамически -->
                <div class="history-item">
                    <div>
                        <div style="font-weight: bold;">Королевская звезда</div>
                        <div class="history-date">Сегодня, 14:30</div>
                    </div>
                    <div class="history-amount">-1,000 ★</div>
                </div>
                
                <div class="history-item">
                    <div>
                        <div style="font-weight: bold;">Реферальное вознаграждение</div>
                        <div class="history-date">Вчера, 18:15</div>
                    </div>
                    <div class="history-amount">+25 ★</div>
                </div>
                
                <div class="history-item">
                    <div>
                        <div style="font-weight: bold;">Двойная звезда</div>
                        <div class="history-date">5 марта, 10:45</div>
                    </div>
                    <div class="history-amount">-250 ★</div>
                </div>
            </div>
        </section>

        <!-- Кнопка для Telegram -->
        <button class="telegram-btn" onclick="openTelegramBot()">
            <i class="fab fa-telegram"></i> Открыть бота в Telegram
        </button>

        <!-- Футер -->
        <footer class="footer">
            <p>© 2024 MinionStarsMarket. Все звезды являются виртуальными товарами.</p>
            <p style="margin-top: 10px; font-size: 0.8rem;">
                <i class="fas fa-info-circle"></i> При поддержке Telegram Web App
            </p>
        </footer>
    </div>

    <!-- Уведомление -->
    <div class="notification" id="notification">
        <span id="notificationText">Текст уведомления</span>
    </div>

    <script>
        // Инициализация Telegram Web App
        let tg = window.Telegram.WebApp;
        
        // Инициализируем приложение
        tg.expand();
        tg.enableClosingConfirmation();
        
        // Получаем данные пользователя
        const user = tg.initDataUnsafe.user;
        
        // Обновляем информацию о пользователе
        if (user) {
            document.getElementById('userBalance').textContent = `1,250 ★`;
            // Можно использовать user.id для персонализации
        }
        
        // Данные о звездах
        const stars = [
            { id: 1, name: "Обычная звезда", price: 100, description: "Базовая звезда для начинающих коллекционеров." },
            { id: 2, name: "Двойная звезда", price: 250, description: "Пара гравитационно связанных звезд." },
            { id: 3, name: "Кристальная звезда", price: 500, description: "Звезда с кристаллической структурой." },
            { id: 4, name: "Королевская звезда", price: 1000, description: "Элитная звезда для истинных ценителей." }
        ];
        
        // Покупка звезды
        function buyStar(starId) {
            const star = stars.find(s => s.id === starId);
            
            // Показываем подтверждение
            if (confirm(`Вы хотите купить "${star.name}" за ${star.price} ★?`)) {
                // В реальном приложении здесь был бы запрос к серверу
                showNotification(`Поздравляем! Вы купили "${star.name}"!`);
                
                // Обновляем баланс (в реальном приложении сервер должен это делать)
                const balanceElement = document.getElementById('userBalance');
                let currentBalance = parseInt(balanceElement.textContent.replace(/[^0-9]/g, ''));
                currentBalance -= star.price;
                balanceElement.textContent = `${currentBalance.toLocaleString()} ★`;
                
                // Добавляем в историю
                addToHistory(star.name, -star.price);
                
                // Отправляем данные в Telegram бота
                tg.sendData(JSON.stringify({
                    action: 'buy_star',
                    star_id: starId,
                    star_name: star.name,
                    price: star.price
                }));
            }
        }
        
        // Копирование реферальной ссылки
        function copyReferralLink() {
            const linkInput = document.getElementById('referralLink');
            linkInput.select();
            linkInput.setSelectionRange(0, 99999);
            
            try {
                navigator.clipboard.writeText(linkInput.value);
                showNotification('Реферальная ссылка скопирована!');
            } catch (err) {
                // Fallback для старых браузеров
                document.execCommand('copy');
                showNotification('Реферальная ссылка скопирована!');
            }
        }
        
        // Добавление в историю
        function addToHistory(item, amount) {
            const historyList = document.getElementById('purchaseHistory');
            const now = new Date();
            
            // Форматируем дату
            const dateStr = now.toLocaleDateString('ru-RU', {
                day: 'numeric',
                month: 'long',
                hour: '2-digit',
                minute: '2-digit'
            });
            
            const historyItem = document.createElement('div');
            historyItem.className = 'history-item';
            historyItem.innerHTML = `
                <div>
                    <div style="font-weight: bold;">${item}</div>
                    <div class="history-date">${dateStr}</div>
                </div>
                <div class="history-amount" style="color: ${amount > 0 ? 'var(--success)' : '#ff6b6b'}">
                    ${amount > 0 ? '+' : ''}${amount.toLocaleString()} ★
                </div>
            `;
            
            // Добавляем в начало списка
            historyList.insertBefore(historyItem, historyList.firstChild);
        }
        
        // Показать уведомление
        function showNotification(text) {
            const notification = document.getElementById('notification');
            const notificationText = document.getElementById('notificationText');
            
            notificationText.textContent = text;
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        // Открыть бота в Telegram
        function openTelegramBot() {
            tg.openTelegramLink('https://t.me/MinionStarsMarketBot');
        }
        
        // Имитация получения реферального вознаграждения
        function simulateReferralEarning() {
            const earning = Math.floor(Math.random() * 50) + 10;
            
            // Обновляем статистику
            const refEarnedElement = document.getElementById('refEarned');
            let currentEarned = parseInt(refEarnedElement.textContent);
            currentEarned += earning;
            refEarnedElement.textContent = `${currentEarned} ★`;
            
            // Обновляем баланс
            const balanceElement = document.getElementById('userBalance');
            let currentBalance = parseInt(balanceElement.textContent.replace(/[^0-9]/g, ''));
            currentBalance += earning;
            balanceElement.textContent = `${currentBalance.toLocaleString()} ★`;
            
            // Добавляем в историю
            addToHistory('Реферальное вознаграждение', earning);
            
            showNotification(`Вы получили ${earning} ★ от реферала!`);
        }
        
        // Имитация добавления реферала
        function simulateNewReferral() {
            const refCountElement = document.getElementById('refCount');
            let currentCount = parseInt(refCountElement.textContent);
            currentCount++;
            refCountElement.textContent = currentCount;
            
            showNotification('У вас новый реферал!');
            
            // Через 3 секунды имитируем его первую покупку
            setTimeout(() => {
                simulateReferralEarning();
            }, 3000);
        }
        
        // Демонстрационные функции (в реальном приложении не нужны)
        document.addEventListener('DOMContentLoaded', function() {
            // Пример: каждые 30 секунд имитируем нового реферала (для демо)
            // setInterval(simulateNewReferral, 30000);
            
            // Генерация уникальной реферальной ссылки
            if (user) {
                const refLink = `https://t.me/MinionStarsMarketBot?start=ref_${user.id}`;
                document.getElementById('referralLink').value = refLink;
            }
        });
        
        // Обработка данных от Telegram
        tg.onEvent('viewportChanged', function() {
            console.log('Viewport changed');
        });
        
        // Основная инициализация при загрузке
        Telegram.WebApp.ready();
    </script>
</body>
</html>

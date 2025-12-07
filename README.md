<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Japan-Rundreise 8.-24. Mai 2025</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f0f1a 0%, #1a1a2e 50%, #16213e 100%);
            min-height: 100vh;
            color: #fff;
            padding: 20px;
        }
        
        .container {
            max-width: 1600px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 25px;
            background: rgba(255,255,255,0.03);
            border-radius: 20px;
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        h1 {
            font-size: 2.2rem;
            background: linear-gradient(90deg, #ff6b6b, #ffd93d, #6bcb77);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 8px;
        }
        
        .subtitle {
            color: #888;
            font-size: 1rem;
        }
        
        .stats-bar {
            display: flex;
            justify-content: center;
            gap: 50px;
            margin-top: 20px;
            flex-wrap: wrap;
        }
        
        .stat {
            text-align: center;
        }
        
        .stat-number {
            font-size: 1.8rem;
            font-weight: bold;
            background: linear-gradient(135deg, #ff6b6b, #ffd93d);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .stat-label {
            color: #666;
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        /* Main Layout */
        .main-grid {
            display: grid;
            grid-template-columns: 350px 1fr;
            gap: 25px;
            margin-bottom: 30px;
        }
        
        @media (max-width: 1100px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
        }

        /* Route Visual */
        .route-section {
            background: rgba(255,255,255,0.03);
            border-radius: 20px;
            padding: 20px;
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .section-title {
            font-size: 1.1rem;
            margin-bottom: 20px;
            color: #ffd93d;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .route-flow {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .route-stop {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 15px;
            background: rgba(255,255,255,0.03);
            border-radius: 12px;
            border-left: 4px solid;
            transition: all 0.3s ease;
        }

        .route-stop:hover {
            background: rgba(255,255,255,0.08);
            transform: translateX(5px);
        }

        .route-stop.tokio { border-color: #ff6b6b; }
        .route-stop.hakone { border-color: #4ecdc4; }
        .route-stop.kyoto { border-color: #ffd93d; }
        .route-stop.hiroshima { border-color: #f38181; }
        .route-stop.osaka { border-color: #95e1d3; }

        .stop-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            flex-shrink: 0;
        }

        .stop-icon.tokio { background: rgba(255, 107, 107, 0.2); }
        .stop-icon.hakone { background: rgba(78, 205, 196, 0.2); }
        .stop-icon.kyoto { background: rgba(255, 217, 61, 0.2); }
        .stop-icon.hiroshima { background: rgba(243, 129, 129, 0.2); }
        .stop-icon.osaka { background: rgba(149, 225, 211, 0.2); }

        .stop-info {
            flex: 1;
        }

        .stop-city {
            font-weight: bold;
            font-size: 1rem;
        }

        .stop-dates {
            font-size: 0.75rem;
            color: #888;
        }

        .stop-nights {
            background: rgba(255,255,255,0.1);
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 0.7rem;
            color: #aaa;
        }

        .route-arrow {
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 5px 0;
            color: #444;
        }

        .route-arrow svg {
            width: 20px;
            height: 20px;
        }

        /* Timeline Section */
        .timeline-section {
            background: rgba(255,255,255,0.03);
            border-radius: 20px;
            padding: 20px;
            border: 1px solid rgba(255,255,255,0.1);
        }

        .timeline-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 12px;
            max-height: 600px;
            overflow-y: auto;
            padding-right: 10px;
        }

        .timeline-grid::-webkit-scrollbar {
            width: 6px;
        }

        .timeline-grid::-webkit-scrollbar-track {
            background: rgba(255,255,255,0.05);
            border-radius: 3px;
        }

        .timeline-grid::-webkit-scrollbar-thumb {
            background: #ff6b6b;
            border-radius: 3px;
        }

        .day-card {
            background: rgba(255,255,255,0.02);
            border-radius: 12px;
            padding: 15px;
            border-left: 3px solid;
            transition: all 0.3s ease;
        }

        .day-card:hover {
            background: rgba(255,255,255,0.06);
            transform: translateY(-2px);
        }

        .day-card.tokio { border-color: #ff6b6b; }
        .day-card.hakone { border-color: #4ecdc4; }
        .day-card.kyoto { border-color: #ffd93d; }
        .day-card.hiroshima { border-color: #f38181; }
        .day-card.osaka { border-color: #95e1d3; }
        .day-card.departure { border-color: #666; }

        .day-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .day-date {
            font-size: 0.85rem;
            color: #888;
        }

        .day-city {
            font-size: 0.75rem;
            padding: 3px 10px;
            border-radius: 20px;
            font-weight: 500;
        }

        .day-city.tokio { background: rgba(255, 107, 107, 0.2); color: #ff6b6b; }
        .day-city.hakone { background: rgba(78, 205, 196, 0.2); color: #4ecdc4; }
        .day-city.kyoto { background: rgba(255, 217, 61, 0.2); color: #ffd93d; }
        .day-city.hiroshima { background: rgba(243, 129, 129, 0.2); color: #f38181; }
        .day-city.osaka { background: rgba(149, 225, 211, 0.2); color: #95e1d3; }
        .day-city.departure { background: rgba(100, 100, 100, 0.2); color: #999; }

        .day-title {
            font-weight: bold;
            font-size: 0.95rem;
            margin-bottom: 8px;
        }

        .day-highlights {
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
        }

        .highlight {
            font-size: 0.7rem;
            padding: 3px 8px;
            background: rgba(255,255,255,0.05);
            border-radius: 6px;
            color: #aaa;
        }

        .highlight.main {
            background: rgba(255, 107, 107, 0.15);
            color: #ff8a8a;
        }

        /* Hotels Section */
        .hotels-section {
            background: rgba(255,255,255,0.03);
            border-radius: 20px;
            padding: 20px;
            border: 1px solid rgba(255,255,255,0.1);
        }

        .hotels-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 15px;
        }

        .hotel-card {
            background: rgba(255,255,255,0.02);
            border-radius: 12px;
            padding: 15px;
            border-top: 3px solid;
        }

        .hotel-card.tokio { border-color: #ff6b6b; }
        .hotel-card.hakone { border-color: #4ecdc4; }
        .hotel-card.kyoto { border-color: #ffd93d; }
        .hotel-card.hiroshima { border-color: #f38181; }
        .hotel-card.osaka { border-color: #95e1d3; }

        .hotel-city {
            font-weight: bold;
            font-size: 1rem;
            margin-bottom: 3px;
        }

        .hotel-nights {
            font-size: 0.75rem;
            color: #666;
            margin-bottom: 12px;
        }

        .hotel-area {
            font-size: 0.8rem;
            color: #aaa;
            margin-bottom: 8px;
        }

        .hotel-area strong {
            color: #ddd;
        }

        .hotel-recommendations {
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
        }

        .hotel-name {
            font-size: 0.7rem;
            padding: 3px 8px;
            background: rgba(255,255,255,0.08);
            border-radius: 6px;
            color: #bbb;
        }

        /* Tips Section */
        .tips-section {
            margin-top: 25px;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }

        .tip-card {
            background: rgba(255,255,255,0.03);
            border-radius: 12px;
            padding: 18px;
            text-align: center;
            border: 1px solid rgba(255,255,255,0.05);
        }

        .tip-icon {
            font-size: 1.8rem;
            margin-bottom: 10px;
        }

        .tip-title {
            font-size: 0.75rem;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 5px;
        }

        .tip-value {
            font-size: 0.9rem;
            color: #ddd;
        }

        /* Map section */
        .map-visual {
            background: linear-gradient(180deg, #1a2a4a 0%, #2a4a6a 100%);
            border-radius: 15px;
            padding: 20px;
            margin-top: 20px;
            position: relative;
            height: 200px;
            overflow: hidden;
        }

        .map-route {
            position: absolute;
            top: 50%;
            left: 5%;
            right: 5%;
            height: 4px;
            background: linear-gradient(90deg, #ff6b6b, #4ecdc4, #ffd93d, #f38181, #95e1d3);
            border-radius: 2px;
            transform: translateY(-50%);
        }

        .map-point {
            position: absolute;
            top: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
        }

        .map-dot {
            width: 16px;
            height: 16px;
            border-radius: 50%;
            border: 3px solid #fff;
            margin: 0 auto 8px;
            box-shadow: 0 0 15px rgba(255,255,255,0.3);
        }

        .map-label {
            font-size: 0.75rem;
            color: #fff;
            white-space: nowrap;
            text-shadow: 0 2px 4px rgba(0,0,0,0.5);
        }

        .map-point:nth-child(2) { left: 5%; }
        .map-point:nth-child(3) { left: 20%; }
        .map-point:nth-child(4) { left: 40%; }
        .map-point:nth-child(5) { left: 65%; }
        .map-point:nth-child(6) { left: 85%; }

        .flight-indicator {
            position: absolute;
            font-size: 1.5rem;
            top: 50%;
            transform: translateY(-50%);
        }

        .flight-indicator.arrival {
            left: 2%;
        }

        .flight-indicator.departure {
            right: 2%;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🇯🇵 Japan-Rundreise 2025</h1>
            <p class="subtitle">8. Mai – 24. Mai • Von Tokio nach Osaka</p>
            <div class="stats-bar">
                <div class="stat">
                    <div class="stat-number">17</div>
                    <div class="stat-label">Tage</div>
                </div>
                <div class="stat">
                    <div class="stat-number">16</div>
                    <div class="stat-label">Übernachtungen</div>
                </div>
                <div class="stat">
                    <div class="stat-number">5</div>
                    <div class="stat-label">Städte</div>
                </div>
                <div class="stat">
                    <div class="stat-number">4+</div>
                    <div class="stat-label">UNESCO-Stätten</div>
                </div>
            </div>
        </header>

        <div class="main-grid">
            <!-- Route Flow -->
            <div class="route-section">
                <h2 class="section-title">🗾 Reiseroute</h2>
                
                <div class="map-visual">
                    <div class="map-route"></div>
                    <span class="flight-indicator arrival">✈️</span>
                    <div class="map-point">
                        <div class="map-dot" style="background: #ff6b6b;"></div>
                        <div class="map-label">Tokio</div>
                    </div>
                    <div class="map-point">
                        <div class="map-dot" style="background: #4ecdc4;"></div>
                        <div class="map-label">Hakone</div>
                    </div>
                    <div class="map-point">
                        <div class="map-dot" style="background: #ffd93d;"></div>
                        <div class="map-label">Kyoto</div>
                    </div>
                    <div class="map-point">
                        <div class="map-dot" style="background: #f38181;"></div>
                        <div class="map-label">Hiroshima</div>
                    </div>
                    <div class="map-point">
                        <div class="map-dot" style="background: #95e1d3;"></div>
                        <div class="map-label">Osaka</div>
                    </div>
                    <span class="flight-indicator departure">✈️</span>
                </div>

                <div class="route-flow" style="margin-top: 20px;">
                    <div class="route-stop tokio">
                        <div class="stop-icon tokio">🗼</div>
                        <div class="stop-info">
                            <div class="stop-city">Tokio</div>
                            <div class="stop-dates">8. – 14. Mai</div>
                        </div>
                        <div class="stop-nights">6 Nächte</div>
                    </div>

                    <div class="route-arrow">
                        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 16l-6-6h12z"/></svg>
                    </div>

                    <div class="route-stop hakone">
                        <div class="stop-icon hakone">🗻</div>
                        <div class="stop-info">
                            <div class="stop-city">Hakone</div>
                            <div class="stop-dates">14. Mai</div>
                        </div>
                        <div class="stop-nights">1 Nacht</div>
                    </div>

                    <div class="route-arrow">
                        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 16l-6-6h12z"/></svg>
                    </div>

                    <div class="route-stop kyoto">
                        <div class="stop-icon kyoto">⛩️</div>
                        <div class="stop-info">
                            <div class="stop-city">Kyoto</div>
                            <div class="stop-dates">15. – 18. Mai</div>
                        </div>
                        <div class="stop-nights">3 Nächte</div>
                    </div>

                    <div class="route-arrow">
                        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 16l-6-6h12z"/></svg>
                    </div>

                    <div class="route-stop hiroshima">
                        <div class="stop-icon hiroshima">🕊️</div>
                        <div class="stop-info">
                            <div class="stop-city">Hiroshima</div>
                            <div class="stop-dates">18. – 20. Mai</div>
                        </div>
                        <div class="stop-nights">2 Nächte</div>
                    </div>

                    <div class="route-arrow">
                        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 16l-6-6h12z"/></svg>
                    </div>

                    <div class="route-stop osaka">
                        <div class="stop-icon osaka">🏯</div>
                        <div class="stop-info">
                            <div class="stop-city">Osaka</div>
                            <div class="stop-dates">20. – 24. Mai</div>
                        </div>
                        <div class="stop-nights">4 Nächte</div>
                    </div>
                </div>
            </div>

            <!-- Timeline -->
            <div class="timeline-section">
                <h2 class="section-title">📅 Tagesübersicht</h2>
                <div class="timeline-grid">
                    <div class="day-card tokio">
                        <div class="day-header">
                            <span class="day-date">Do, 8. Mai</span>
                            <span class="day-city tokio">Tokio</span>
                        </div>
                        <div class="day-title">Ankunft</div>
                        <div class="day-highlights">
                            <span class="highlight main">✈️ Anreise</span>
                            <span class="highlight">Check-in</span>
                            <span class="highlight">Spaziergang</span>
                        </div>
                    </div>

                    <div class="day-card tokio">
                        <div class="day-header">
                            <span class="day-date">Fr, 9. Mai</span>
                            <span class="day-city tokio">Tokio</span>
                        </div>
                        <div class="day-title">Shinjuku & Shibuya</div>
                        <div class="day-highlights">
                            <span class="highlight main">Meiji-Schrein</span>
                            <span class="highlight">Harajuku</span>
                            <span class="highlight">Omotesandō</span>
                            <span class="highlight">Shibuya Crossing</span>
                        </div>
                    </div>

                    <div class="day-card tokio">
                        <div class="day-header">
                            <span class="day-date">Sa, 10. Mai</span>
                            <span class="day-city tokio">Tokio</span>
                        </div>
                        <div class="day-title">Asakusa & Ueno</div>
                        <div class="day-highlights">
                            <span class="highlight main">Senso-ji</span>
                            <span class="highlight">Nakamise</span>
                            <span class="highlight">Ueno-Park</span>
                            <span class="highlight">Akihabara</span>
                        </div>
                    </div>

                    <div class="day-card tokio">
                        <div class="day-header">
                            <span class="day-date">So, 11. Mai</span>
                            <span class="day-city tokio">Tokio</span>
                        </div>
                        <div class="day-title">Shinjuku & Odaiba</div>
                        <div class="day-highlights">
                            <span class="highlight">Shinjuku Gyoen</span>
                            <span class="highlight main">teamLab Planets</span>
                            <span class="highlight">Digital Art</span>
                        </div>
                    </div>

                    <div class="day-card tokio">
                        <div class="day-header">
                            <span class="day-date">Mo, 12. Mai</span>
                            <span class="day-city tokio">Tokio</span>
                        </div>
                        <div class="day-title">Tagesausflug</div>
                        <div class="day-highlights">
                            <span class="highlight main">Nikkō</span>
                            <span class="highlight">oder</span>
                            <span class="highlight main">Kamakura</span>
                        </div>
                    </div>

                    <div class="day-card tokio">
                        <div class="day-header">
                            <span class="day-date">Di, 13. Mai</span>
                            <span class="day-city tokio">Tokio</span>
                        </div>
                        <div class="day-title">Freier Tag</div>
                        <div class="day-highlights">
                            <span class="highlight">Tsukiji</span>
                            <span class="highlight">Ginza</span>
                            <span class="highlight main">Sumō-Turnier</span>
                        </div>
                    </div>

                    <div class="day-card hakone">
                        <div class="day-header">
                            <span class="day-date">Mi, 14. Mai</span>
                            <span class="day-city hakone">Hakone</span>
                        </div>
                        <div class="day-title">Hakone-Rundkurs</div>
                        <div class="day-highlights">
                            <span class="highlight main">Ashi-See</span>
                            <span class="highlight">Owakudani</span>
                            <span class="highlight">🗻 Fuji-Blick</span>
                            <span class="highlight main">Ryokan</span>
                        </div>
                    </div>

                    <div class="day-card kyoto">
                        <div class="day-header">
                            <span class="day-date">Do, 15. Mai</span>
                            <span class="day-city kyoto">Kyoto</span>
                        </div>
                        <div class="day-title">Anreise nach Kyoto</div>
                        <div class="day-highlights">
                            <span class="highlight">🚄 Shinkansen</span>
                            <span class="highlight main">Gion-Viertel</span>
                            <span class="highlight">Geisha</span>
                        </div>
                    </div>

                    <div class="day-card kyoto">
                        <div class="day-header">
                            <span class="day-date">Fr, 16. Mai</span>
                            <span class="day-city kyoto">Kyoto</span>
                        </div>
                        <div class="day-title">Tempel-Tag</div>
                        <div class="day-highlights">
                            <span class="highlight main">⛩️ Fushimi Inari</span>
                            <span class="highlight main">Kiyomizu-dera</span>
                            <span class="highlight">Ninen-Zaka</span>
                        </div>
                    </div>

                    <div class="day-card kyoto">
                        <div class="day-header">
                            <span class="day-date">Sa, 17. Mai</span>
                            <span class="day-city kyoto">Kyoto</span>
                        </div>
                        <div class="day-title">Arashiyama</div>
                        <div class="day-highlights">
                            <span class="highlight main">🎋 Bambuswald</span>
                            <span class="highlight">Tenryū-ji</span>
                            <span class="highlight main">Kinkaku-ji</span>
                            <span class="highlight">Ryoan-ji</span>
                        </div>
                    </div>

                    <div class="day-card hiroshima">
                        <div class="day-header">
                            <span class="day-date">So, 18. Mai</span>
                            <span class="day-city hiroshima">Hiroshima</span>
                        </div>
                        <div class="day-title">Peace Memorial</div>
                        <div class="day-highlights">
                            <span class="highlight">🚄 Shinkansen</span>
                            <span class="highlight main">Friedenspark</span>
                            <span class="highlight main">Genbaku Dome</span>
                            <span class="highlight">Museum</span>
                        </div>
                    </div>

                    <div class="day-card hiroshima">
                        <div class="day-header">
                            <span class="day-date">Mo, 19. Mai</span>
                            <span class="day-city hiroshima">Hiroshima</span>
                        </div>
                        <div class="day-title">Miyajima-Ausflug</div>
                        <div class="day-highlights">
                            <span class="highlight">🚢 Fähre</span>
                            <span class="highlight main">⛩️ Itsukushima</span>
                            <span class="highlight">Torii im Meer</span>
                            <span class="highlight">Mt. Misen</span>
                        </div>
                    </div>

                    <div class="day-card osaka">
                        <div class="day-header">
                            <span class="day-date">Di, 20. Mai</span>
                            <span class="day-city osaka">Osaka</span>
                        </div>
                        <div class="day-title">Ankunft Osaka</div>
                        <div class="day-highlights">
                            <span class="highlight">🚄 Shinkansen</span>
                            <span class="highlight main">Osaka Castle</span>
                            <span class="highlight">Umeda Sky</span>
                        </div>
                    </div>

                    <div class="day-card osaka">
                        <div class="day-header">
                            <span class="day-date">Mi, 21. Mai</span>
                            <span class="day-city osaka">Osaka</span>
                        </div>
                        <div class="day-title">Dōtonbori</div>
                        <div class="day-highlights">
                            <span class="highlight main">🍜 Street-Food</span>
                            <span class="highlight">Shinsaibashi</span>
                            <span class="highlight">Neonlichter</span>
                            <span class="highlight">USJ optional</span>
                        </div>
                    </div>

                    <div class="day-card osaka">
                        <div class="day-header">
                            <span class="day-date">Do, 22. Mai</span>
                            <span class="day-city osaka">Himeji</span>
                        </div>
                        <div class="day-title">Tagesausflug Himeji</div>
                        <div class="day-highlights">
                            <span class="highlight">🚄 Shinkansen</span>
                            <span class="highlight main">🏯 Himeji Castle</span>
                            <span class="highlight">UNESCO-Welterbe</span>
                        </div>
                    </div>

                    <div class="day-card osaka">
                        <div class="day-header">
                            <span class="day-date">Fr, 23. Mai</span>
                            <span class="day-city osaka">Osaka</span>
                        </div>
                        <div class="day-title">Letzter Tag</div>
                        <div class="day-highlights">
                            <span class="highlight">Kobe optional</span>
                            <span class="highlight">Nara optional</span>
                            <span class="highlight">Shopping</span>
                            <span class="highlight">Packen</span>
                        </div>
                    </div>

                    <div class="day-card departure">
                        <div class="day-header">
                            <span class="day-date">Sa, 24. Mai</span>
                            <span class="day-city departure">Abreise</span>
                        </div>
                        <div class="day-title">Heimreise</div>
                        <div class="day-highlights">
                            <span class="highlight main">✈️ Kansai Airport</span>
                            <span class="highlight">Abreise ab Osaka</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Hotels Section -->
        <div class="hotels-section">
            <h2 class="section-title">🏨 Empfohlene Unterkünfte</h2>
            <div class="hotels-grid">
                <div class="hotel-card tokio">
                    <div class="hotel-city">Tokio</div>
                    <div class="hotel-nights">6 Nächte</div>
                    <div class="hotel-area"><strong>Shinjuku:</strong> Park Hyatt, Keio Plaza</div>
                    <div class="hotel-area"><strong>Shibuya:</strong> Shibuya Excel, Cerulean Tower</div>
                    <div class="hotel-area"><strong>Asakusa:</strong> Asakusa View Hotel, Mitsui Garden</div>
                </div>

                <div class="hotel-card hakone">
                    <div class="hotel-city">Hakone</div>
                    <div class="hotel-nights">1 Nacht (Ryokan)</div>
                    <div class="hotel-area"><strong>Empfohlen:</strong> Traditionelles Ryokan mit Onsen</div>
                    <div class="hotel-recommendations">
                        <span class="hotel-name">Gora Kadan</span>
                        <span class="hotel-name">Fukuzumiro</span>
                    </div>
                </div>

                <div class="hotel-card kyoto">
                    <div class="hotel-city">Kyoto</div>
                    <div class="hotel-nights">3 Nächte</div>
                    <div class="hotel-area"><strong>Downtown:</strong> Kyoto Hotel Okura, Cross Hotel</div>
                    <div class="hotel-area"><strong>Gion:</strong> Four Seasons, Nohga Hotel</div>
                    <div class="hotel-area"><strong>Bahnhof:</strong> Hotel Granvia, Sakura Terrace</div>
                </div>

                <div class="hotel-card hiroshima">
                    <div class="hotel-city">Hiroshima</div>
                    <div class="hotel-nights">2 Nächte</div>
                    <div class="hotel-area"><strong>Downtown:</strong> Hilton, Hotel Intergate, The Knot</div>
                    <div class="hotel-area"><strong>Bahnhof:</strong> Sheraton Grand, Hotel Granvia</div>
                </div>

                <div class="hotel-card osaka">
                    <div class="hotel-city">Osaka</div>
                    <div class="hotel-nights">4 Nächte</div>
                    <div class="hotel-area"><strong>Umeda:</strong> Conrad, InterContinental, Ritz-Carlton</div>
                    <div class="hotel-area"><strong>Namba:</strong> Namba Oriental, Hotel Nikko</div>
                    <div class="hotel-area"><strong>Flughafen:</strong> Hotel Nikko Kansai Airport</div>
                </div>
            </div>
        </div>

        <!-- Tips Section -->
        <div class="tips-section">
            <div class="tip-card">
                <div class="tip-icon">🚄</div>
                <div class="tip-title">Transport</div>
                <div class="tip-value">Japan Rail Pass + Suica/Pasmo</div>
            </div>
            <div class="tip-card">
                <div class="tip-icon">🛂</div>
                <div class="tip-title">Visum</div>
                <div class="tip-value">EU: 90 Tage visafrei</div>
            </div>
            <div class="tip-card">
                <div class="tip-icon">🌸</div>
                <div class="tip-title">Wetter</div>
                <div class="tip-value">Warm, leichte Kleidung + Jacke</div>
            </div>
            <div class="tip-card">
                <div class="tip-icon">🎎</div>
                <div class="tip-title">Events</div>
                <div class="tip-value">Sumō-Turnier, Sanja-Matsuri</div>
            </div>
            <div class="tip-card">
                <div class="tip-icon">👟</div>
                <div class="tip-title">Etikette</div>
                <div class="tip-value">Schuhe aus in Tempeln</div>
            </div>
            <div class="tip-card">
                <div class="tip-icon">✈️</div>
                <div class="tip-title">Flüge</div>
                <div class="tip-value">An: Tokio → Ab: Osaka (KIX)</div>
            </div>
        </div>
    </div>
</body>
</html>

<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Japan-Reiseplaner 2025</title>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
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
        }

        /* Loading state */
        #root {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .loading {
            text-align: center;
            color: #888;
        }

        .loading-spinner {
            width: 40px;
            height: 40px;
            border: 3px solid rgba(255,255,255,0.1);
            border-top-color: #ff6b6b;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div id="root">
        <div class="loading">
            <div class="loading-spinner"></div>
            <div>Lädt...</div>
        </div>
    </div>

    <script type="text/babel">
        const { useState, useEffect } = React;

        // Initial travel data - you can modify this!
        const initialDays = [
            { id: 1, date: '8. Mai', weekday: 'Do', city: 'Tokio', title: 'Ankunft', highlights: ['✈️ Anreise', 'Check-in', 'Spaziergang'] },
            { id: 2, date: '9. Mai', weekday: 'Fr', city: 'Tokio', title: 'Shinjuku & Shibuya', highlights: ['Meiji-Schrein', 'Harajuku', 'Omotesandō', 'Shibuya Crossing'] },
            { id: 3, date: '10. Mai', weekday: 'Sa', city: 'Tokio', title: 'Asakusa & Ueno', highlights: ['Senso-ji', 'Nakamise', 'Ueno-Park', 'Akihabara'] },
            { id: 4, date: '11. Mai', weekday: 'So', city: 'Tokio', title: 'Shinjuku & Odaiba', highlights: ['Shinjuku Gyoen', 'teamLab Planets', 'Digital Art'] },
            { id: 5, date: '12. Mai', weekday: 'Mo', city: 'Tokio', title: 'Tagesausflug', highlights: ['Nikkō oder Kamakura'] },
            { id: 6, date: '13. Mai', weekday: 'Di', city: 'Tokio', title: 'Freier Tag', highlights: ['Tsukiji', 'Ginza', 'Sumō-Turnier'] },
            { id: 7, date: '14. Mai', weekday: 'Mi', city: 'Hakone', title: 'Hakone-Rundkurs', highlights: ['Ashi-See', 'Owakudani', '🗻 Fuji-Blick', 'Ryokan & Onsen'] },
            { id: 8, date: '15. Mai', weekday: 'Do', city: 'Kyoto', title: 'Anreise Kyoto', highlights: ['🚄 Shinkansen', 'Gion-Viertel', 'Geisha'] },
            { id: 9, date: '16. Mai', weekday: 'Fr', city: 'Kyoto', title: 'Tempel-Tag', highlights: ['⛩️ Fushimi Inari', 'Kiyomizu-dera', 'Ninen-Zaka'] },
            { id: 10, date: '17. Mai', weekday: 'Sa', city: 'Kyoto', title: 'Arashiyama', highlights: ['🎋 Bambuswald', 'Tenryū-ji', 'Kinkaku-ji', 'Ryoan-ji'] },
            { id: 11, date: '18. Mai', weekday: 'So', city: 'Hiroshima', title: 'Peace Memorial', highlights: ['🚄 Shinkansen', 'Friedenspark', 'Genbaku Dome', 'Museum'] },
            { id: 12, date: '19. Mai', weekday: 'Mo', city: 'Hiroshima', title: 'Miyajima-Ausflug', highlights: ['🚢 Fähre', '⛩️ Itsukushima', 'Torii im Meer', 'Mt. Misen'] },
            { id: 13, date: '20. Mai', weekday: 'Di', city: 'Osaka', title: 'Ankunft Osaka', highlights: ['🚄 Shinkansen', 'Osaka Castle', 'Umeda Sky'] },
            { id: 14, date: '21. Mai', weekday: 'Mi', city: 'Osaka', title: 'Dōtonbori', highlights: ['🍜 Street-Food', 'Shinsaibashi', 'Neonlichter'] },
            { id: 15, date: '22. Mai', weekday: 'Do', city: 'Osaka', title: 'Tagesausflug Himeji', highlights: ['🚄 Shinkansen', '🏯 Himeji Castle', 'UNESCO-Welterbe'] },
            { id: 16, date: '23. Mai', weekday: 'Fr', city: 'Osaka', title: 'Letzter Tag', highlights: ['Kobe/Nara optional', 'Shopping', 'Packen'] },
            { id: 17, date: '24. Mai', weekday: 'Sa', city: 'Abreise', title: 'Heimreise', highlights: ['✈️ Kansai Airport'] },
        ];

        const cityColors = {
            'Tokio': '#ff6b6b',
            'Hakone': '#4ecdc4',
            'Kyoto': '#ffd93d',
            'Hiroshima': '#f38181',
            'Osaka': '#95e1d3',
            'Nara': '#dda0dd',
            'Kobe': '#87ceeb',
            'Abreise': '#888888',
        };

        const cityIcons = {
            'Tokio': '🗼',
            'Hakone': '🗻',
            'Kyoto': '⛩️',
            'Hiroshima': '🕊️',
            'Osaka': '🏯',
            'Nara': '🦌',
            'Kobe': '🌉',
            'Abreise': '✈️',
        };

        // LocalStorage helpers
        const STORAGE_KEY = 'japan-reise-data';
        
        const loadFromStorage = () => {
            try {
                const saved = localStorage.getItem(STORAGE_KEY);
                if (saved) {
                    const data = JSON.parse(saved);
                    return {
                        days: data.days || initialDays,
                        title: data.title || 'Japan-Rundreise 2025'
                    };
                }
            } catch (e) {
                console.log('Could not load from storage');
            }
            return { days: initialDays, title: 'Japan-Rundreise 2025' };
        };

        const saveToStorage = (days, title) => {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify({ days, title }));
            } catch (e) {
                console.log('Could not save to storage');
            }
        };

        function JapanTravelPlanner() {
            const [days, setDays] = useState(() => loadFromStorage().days);
            const [editingDay, setEditingDay] = useState(null);
            const [editForm, setEditForm] = useState({});
            const [tripTitle, setTripTitle] = useState(() => loadFromStorage().title);
            const [editingTitle, setEditingTitle] = useState(false);
            const [showExport, setShowExport] = useState(false);

            // Save to localStorage whenever data changes
            useEffect(() => {
                saveToStorage(days, tripTitle);
            }, [days, tripTitle]);

            const handleEdit = (day) => {
                setEditingDay(day.id);
                setEditForm({
                    ...day,
                    highlightsText: day.highlights.join(', ')
                });
            };

            const handleSave = () => {
                setDays(days.map(d => 
                    d.id === editingDay 
                        ? {
                            ...editForm,
                            highlights: editForm.highlightsText.split(',').map(h => h.trim()).filter(h => h),
                        }
                        : d
                ));
                setEditingDay(null);
            };

            const handleCancel = () => {
                setEditingDay(null);
                setEditForm({});
            };

            const addNewDay = () => {
                const newId = Math.max(...days.map(d => d.id), 0) + 1;
                const newDay = {
                    id: newId,
                    date: 'Neuer Tag',
                    weekday: '?',
                    city: 'Tokio',
                    title: 'Neuer Tag',
                    highlights: ['Aktivität hinzufügen']
                };
                setDays([...days, newDay]);
                handleEdit(newDay);
            };

            const deleteDay = (id) => {
                if (confirm('Tag wirklich löschen?')) {
                    setDays(days.filter(d => d.id !== id));
                }
            };

            const moveDay = (id, direction) => {
                const index = days.findIndex(d => d.id === id);
                if ((direction === -1 && index === 0) || (direction === 1 && index === days.length - 1)) return;
                
                const newDays = [...days];
                const temp = newDays[index];
                newDays[index] = newDays[index + direction];
                newDays[index + direction] = temp;
                setDays(newDays);
            };

            const resetData = () => {
                if (confirm('Alle Änderungen zurücksetzen?')) {
                    setDays(initialDays);
                    setTripTitle('Japan-Rundreise 2025');
                }
            };

            const exportData = () => {
                const dataStr = JSON.stringify({ days, title: tripTitle }, null, 2);
                const blob = new Blob([dataStr], { type: 'application/json' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = 'japan-reise-backup.json';
                a.click();
            };

            const importData = (e) => {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = (event) => {
                        try {
                            const data = JSON.parse(event.target.result);
                            if (data.days) setDays(data.days);
                            if (data.title) setTripTitle(data.title);
                            alert('Import erfolgreich!');
                        } catch (err) {
                            alert('Fehler beim Import');
                        }
                    };
                    reader.readAsText(file);
                }
            };

            // Calculate stats
            const cities = [...new Set(days.filter(d => d.city !== 'Abreise').map(d => d.city))];
            const nights = days.length - 1;

            const getColor = (city) => cityColors[city] || '#888888';
            const getIcon = (city) => cityIcons[city] || '📍';

            const styles = {
                container: {
                    maxWidth: '1400px',
                    margin: '0 auto',
                    padding: '20px'
                },
                header: {
                    textAlign: 'center',
                    marginBottom: '30px',
                    padding: '25px',
                    background: 'rgba(255,255,255,0.03)',
                    borderRadius: '20px',
                    border: '1px solid rgba(255,255,255,0.1)'
                },
                title: {
                    fontSize: '2.2rem',
                    background: 'linear-gradient(90deg, #ff6b6b, #ffd93d, #6bcb77)',
                    WebkitBackgroundClip: 'text',
                    WebkitTextFillColor: 'transparent',
                    backgroundClip: 'text',
                    cursor: 'pointer',
                    marginBottom: '8px',
                    display: 'inline-block'
                },
                input: {
                    background: 'rgba(255,255,255,0.1)',
                    border: '1px solid rgba(255,255,255,0.2)',
                    borderRadius: '8px',
                    padding: '8px 12px',
                    color: '#fff',
                    fontSize: '0.9rem',
                    width: '100%'
                },
                button: {
                    background: 'rgba(255,255,255,0.05)',
                    border: 'none',
                    borderRadius: '6px',
                    padding: '6px 12px',
                    color: '#888',
                    cursor: 'pointer',
                    fontSize: '0.8rem'
                },
                saveButton: {
                    flex: 1,
                    background: '#4ecdc4',
                    border: 'none',
                    borderRadius: '8px',
                    padding: '10px',
                    color: '#fff',
                    cursor: 'pointer',
                    fontWeight: 'bold'
                },
                card: {
                    background: 'rgba(255,255,255,0.03)',
                    borderRadius: '15px',
                    padding: '18px',
                    transition: 'all 0.3s ease'
                }
            };

            return (
                <div style={styles.container}>
                    {/* Header */}
                    <header style={styles.header}>
                        {editingTitle ? (
                            <div style={{ display: 'flex', justifyContent: 'center', gap: '10px', alignItems: 'center', marginBottom: '10px' }}>
                                <input
                                    type="text"
                                    value={tripTitle}
                                    onChange={(e) => setTripTitle(e.target.value)}
                                    style={{
                                        ...styles.input,
                                        fontSize: '1.5rem',
                                        textAlign: 'center',
                                        maxWidth: '400px',
                                        border: '2px solid #ff6b6b'
                                    }}
                                    autoFocus
                                />
                                <button onClick={() => setEditingTitle(false)} style={{
                                    ...styles.saveButton,
                                    flex: 'none',
                                    padding: '10px 20px'
                                }}>✓</button>
                            </div>
                        ) : (
                            <h1 onClick={() => setEditingTitle(true)} style={styles.title}>
                                🇯🇵 {tripTitle}
                            </h1>
                        )}
                        
                        <p style={{ color: '#666', fontSize: '0.85rem' }}>
                            Klicke auf Elemente zum Bearbeiten • Daten werden automatisch gespeichert
                        </p>
                        
                        {/* Stats */}
                        <div style={{
                            display: 'flex',
                            justifyContent: 'center',
                            gap: '40px',
                            marginTop: '20px',
                            flexWrap: 'wrap'
                        }}>
                            {[
                                { value: days.length, label: 'TAGE', color: '#ff6b6b' },
                                { value: nights, label: 'NÄCHTE', color: '#ffd93d' },
                                { value: cities.length, label: 'STÄDTE', color: '#4ecdc4' }
                            ].map((stat, i) => (
                                <div key={i} style={{ textAlign: 'center' }}>
                                    <div style={{ fontSize: '1.8rem', fontWeight: 'bold', color: stat.color }}>{stat.value}</div>
                                    <div style={{ color: '#666', fontSize: '0.75rem' }}>{stat.label}</div>
                                </div>
                            ))}
                        </div>

                        {/* Action buttons */}
                        <div style={{ display: 'flex', justifyContent: 'center', gap: '10px', marginTop: '20px', flexWrap: 'wrap' }}>
                            <button onClick={exportData} style={{ ...styles.button, background: 'rgba(78,205,196,0.2)', color: '#4ecdc4' }}>
                                💾 Exportieren
                            </button>
                            <label style={{ ...styles.button, background: 'rgba(255,217,61,0.2)', color: '#ffd93d', cursor: 'pointer' }}>
                                📂 Importieren
                                <input type="file" accept=".json" onChange={importData} style={{ display: 'none' }} />
                            </label>
                            <button onClick={resetData} style={{ ...styles.button, background: 'rgba(255,107,107,0.2)', color: '#ff6b6b' }}>
                                🔄 Zurücksetzen
                            </button>
                        </div>
                    </header>

                    {/* Route Overview */}
                    <div style={{
                        ...styles.card,
                        marginBottom: '25px'
                    }}>
                        <h2 style={{ color: '#ffd93d', marginBottom: '15px', fontSize: '1.1rem' }}>🗾 Route</h2>
                        <div style={{
                            display: 'flex',
                            alignItems: 'center',
                            gap: '10px',
                            flexWrap: 'wrap',
                            justifyContent: 'center'
                        }}>
                            {cities.map((city, i) => (
                                <React.Fragment key={city}>
                                    <div style={{
                                        background: `${getColor(city)}22`,
                                        border: `2px solid ${getColor(city)}`,
                                        borderRadius: '12px',
                                        padding: '10px 16px',
                                        display: 'flex',
                                        alignItems: 'center',
                                        gap: '8px'
                                    }}>
                                        <span style={{ fontSize: '1.2rem' }}>{getIcon(city)}</span>
                                        <span style={{ fontWeight: 'bold', fontSize: '0.9rem' }}>{city}</span>
                                        <span style={{ 
                                            background: 'rgba(255,255,255,0.1)', 
                                            padding: '2px 8px', 
                                            borderRadius: '10px',
                                            fontSize: '0.7rem',
                                            color: '#aaa'
                                        }}>
                                            {days.filter(d => d.city === city).length}
                                        </span>
                                    </div>
                                    {i < cities.length - 1 && (
                                        <span style={{ color: '#444', fontSize: '1.3rem' }}>→</span>
                                    )}
                                </React.Fragment>
                            ))}
                        </div>
                    </div>

                    {/* Days Grid */}
                    <div style={{
                        display: 'grid',
                        gridTemplateColumns: 'repeat(auto-fill, minmax(300px, 1fr))',
                        gap: '15px',
                        marginBottom: '20px'
                    }}>
                        {days.map((day) => {
                            const color = getColor(day.city);
                            const isEditing = editingDay === day.id;
                            
                            return (
                                <div key={day.id} style={{
                                    ...styles.card,
                                    borderLeft: `4px solid ${color}`,
                                    background: isEditing ? 'rgba(255,255,255,0.08)' : 'rgba(255,255,255,0.03)',
                                    border: isEditing ? `1px solid ${color}` : '1px solid transparent',
                                    borderLeftWidth: '4px',
                                    borderLeftStyle: 'solid',
                                    borderLeftColor: color
                                }}>
                                    {isEditing ? (
                                        // Edit Mode
                                        <div style={{ display: 'flex', flexDirection: 'column', gap: '12px' }}>
                                            <div style={{ display: 'flex', gap: '10px' }}>
                                                <input
                                                    type="text"
                                                    value={editForm.date}
                                                    onChange={(e) => setEditForm({...editForm, date: e.target.value})}
                                                    placeholder="Datum"
                                                    style={{ ...styles.input, flex: 1 }}
                                                />
                                                <input
                                                    type="text"
                                                    value={editForm.weekday}
                                                    onChange={(e) => setEditForm({...editForm, weekday: e.target.value})}
                                                    placeholder="Tag"
                                                    style={{ ...styles.input, width: '60px', textAlign: 'center' }}
                                                />
                                            </div>
                                            
                                            <select
                                                value={editForm.city}
                                                onChange={(e) => setEditForm({...editForm, city: e.target.value})}
                                                style={styles.input}
                                            >
                                                {Object.keys(cityColors).map(c => (
                                                    <option key={c} value={c}>{getIcon(c)} {c}</option>
                                                ))}
                                            </select>
                                            
                                            <input
                                                type="text"
                                                value={editForm.title}
                                                onChange={(e) => setEditForm({...editForm, title: e.target.value})}
                                                placeholder="Titel"
                                                style={styles.input}
                                            />
                                            
                                            <textarea
                                                value={editForm.highlightsText}
                                                onChange={(e) => setEditForm({...editForm, highlightsText: e.target.value})}
                                                placeholder="Highlights (kommagetrennt)"
                                                rows={3}
                                                style={{ ...styles.input, resize: 'vertical' }}
                                            />
                                            
                                            <div style={{ display: 'flex', gap: '8px' }}>
                                                <button onClick={handleSave} style={styles.saveButton}>
                                                    💾 Speichern
                                                </button>
                                                <button onClick={handleCancel} style={{
                                                    ...styles.button,
                                                    padding: '10px 15px'
                                                }}>✕</button>
                                            </div>
                                        </div>
                                    ) : (
                                        // View Mode
                                        <>
                                            <div style={{
                                                display: 'flex',
                                                justifyContent: 'space-between',
                                                alignItems: 'center',
                                                marginBottom: '10px'
                                            }}>
                                                <span style={{ color: '#888', fontSize: '0.85rem' }}>
                                                    {day.weekday}, {day.date}
                                                </span>
                                                <span style={{
                                                    background: `${color}33`,
                                                    color: color,
                                                    padding: '3px 10px',
                                                    borderRadius: '20px',
                                                    fontSize: '0.75rem',
                                                    fontWeight: '500'
                                                }}>
                                                    {getIcon(day.city)} {day.city}
                                                </span>
                                            </div>
                                            
                                            <div style={{
                                                fontWeight: 'bold',
                                                fontSize: '1rem',
                                                marginBottom: '10px'
                                            }}>{day.title}</div>
                                            
                                            <div style={{
                                                display: 'flex',
                                                flexWrap: 'wrap',
                                                gap: '6px',
                                                marginBottom: '12px'
                                            }}>
                                                {day.highlights.map((h, i) => (
                                                    <span key={i} style={{
                                                        fontSize: '0.75rem',
                                                        padding: '4px 10px',
                                                        background: 'rgba(255,255,255,0.05)',
                                                        borderRadius: '6px',
                                                        color: '#aaa'
                                                    }}>{h}</span>
                                                ))}
                                            </div>
                                            
                                            <div style={{
                                                display: 'flex',
                                                gap: '5px',
                                                borderTop: '1px solid rgba(255,255,255,0.05)',
                                                paddingTop: '10px'
                                            }}>
                                                <button onClick={() => handleEdit(day)} style={{ ...styles.button, flex: 1 }}>
                                                    ✏️ Bearbeiten
                                                </button>
                                                <button onClick={() => moveDay(day.id, -1)} style={styles.button}>↑</button>
                                                <button onClick={() => moveDay(day.id, 1)} style={styles.button}>↓</button>
                                                <button onClick={() => deleteDay(day.id)} style={{
                                                    ...styles.button,
                                                    background: 'rgba(255,100,100,0.1)',
                                                    color: '#ff6b6b'
                                                }}>🗑️</button>
                                            </div>
                                        </>
                                    )}
                                </div>
                            );
                        })}
                        
                        {/* Add New Day Card */}
                        <div 
                            onClick={addNewDay}
                            style={{
                                ...styles.card,
                                border: '2px dashed rgba(255,255,255,0.1)',
                                display: 'flex',
                                alignItems: 'center',
                                justifyContent: 'center',
                                cursor: 'pointer',
                                minHeight: '200px'
                            }}
                            onMouseOver={(e) => e.currentTarget.style.borderColor = '#ff6b6b'}
                            onMouseOut={(e) => e.currentTarget.style.borderColor = 'rgba(255,255,255,0.1)'}
                        >
                            <div style={{ textAlign: 'center', color: '#666' }}>
                                <div style={{ fontSize: '2rem', marginBottom: '10px' }}>➕</div>
                                <div>Neuen Tag hinzufügen</div>
                            </div>
                        </div>
                    </div>

                    {/* Tips */}
                    <div style={{
                        display: 'grid',
                        gridTemplateColumns: 'repeat(auto-fit, minmax(150px, 1fr))',
                        gap: '12px',
                        marginTop: '25px'
                    }}>
                        {[
                            { icon: '🚄', title: 'Transport', value: 'Japan Rail Pass' },
                            { icon: '🛂', title: 'Visum', value: 'EU: 90 Tage frei' },
                            { icon: '🌸', title: 'Wetter Mai', value: 'Warm, leicht' },
                            { icon: '💴', title: 'Währung', value: 'Yen (¥)' },
                            { icon: '🔌', title: 'Strom', value: 'Typ A/B, 100V' },
                            { icon: '✈️', title: 'Route', value: 'Tokio → Osaka' },
                        ].map((tip, i) => (
                            <div key={i} style={{
                                ...styles.card,
                                textAlign: 'center',
                                padding: '15px'
                            }}>
                                <div style={{ fontSize: '1.5rem', marginBottom: '8px' }}>{tip.icon}</div>
                                <div style={{ fontSize: '0.65rem', color: '#666', textTransform: 'uppercase', letterSpacing: '1px' }}>{tip.title}</div>
                                <div style={{ fontSize: '0.8rem', color: '#ddd', marginTop: '3px' }}>{tip.value}</div>
                            </div>
                        ))}
                    </div>

                    <footer style={{
                        textAlign: 'center',
                        marginTop: '30px',
                        padding: '20px',
                        color: '#444',
                        fontSize: '0.75rem'
                    }}>
                        Japan-Reiseplaner • Daten werden im Browser gespeichert
                    </footer>
                </div>
            );
        }

        // Render the app
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<JapanTravelPlanner />);
    </script>
</body>
</html>

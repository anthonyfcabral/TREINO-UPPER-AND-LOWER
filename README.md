
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>BEYOND GENETICS 2.0 - FULL</title>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Inter:wght@400;700;900&display=swap');
        body { background-color: #000; color: #fff; font-family: 'Inter', sans-serif; -webkit-tap-highlight-color: transparent; overflow-x: hidden; }
        .font-brand { font-family: 'Orbitron', sans-serif; }
        .bg-card { background: #0a0a0a; border: 1px solid #1a1a1a; border-radius: 24px; }
        .accent { color: #ff5f00; }
        .bg-accent { background: #ff5f00; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        input[type="number"] { background: #151515; border-radius: 8px; color: #ff5f00; text-align: center; width: 55px; padding: 6px; font-weight: 900; border: 1px solid #333; outline: none; }
        .timer-panel { background: linear-gradient(to top, #000, #0a0a0a); border-top: 2px solid #ff5f00; box-shadow: 0 -20px 50px rgba(255, 95, 0, 0.3); }
        
        /* Cores solicitadas - Diferenciação sutil */
        .tag-aquec { background-color: #0e0e0e; color: #444; border: 1px solid #1a1a1a; }
        .tag-ajuste { background-color: #1a1a1a; color: #777; border: 1px solid #222; }
        .tag-trabalho { background-color: #ff5f00; color: #000; font-weight: 900; }
    </style>
</head>
<body>
    <div id="root"></div>
    <script type="text/babel">
        const { useState, useEffect } = React;

        const WORKOUT_DATA = {
            "UPPER 1": [
                { id: "u1_1", name: "Supino Inclinado (Máq/Halt)", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u1_2", name: "Voador", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u1_3", name: "Pulley Frente Aberto", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u1_4", name: "Remada Baixa Triângulo", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u1_5", name: "Elevação Lateral Sentado", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u1_6", name: "Rosca Direta Banco 45°", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u1_7", name: "Tríceps Francês Corda", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] }
            ],
            "LOWER 1": [
                { id: "l1_1", name: "Flexor Deitado", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l1_2", name: "Agachamento Hack", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l1_3", name: "Leg 45", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l1_4", name: "Extensor", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l1_5", name: "Stiff", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"AJUSTE", r:"2-4", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] }
            ],
            "UPPER 2": [
                { id: "u2_1", name: "Supino Reto Máquina", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"AJUSTE", r:"4-6", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u2_2", name: "Cross Over", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u2_3", name: "Remada Curvada", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"AJUSTE", r:"4-6", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u2_4", name: "Pulley Frente Triângulo", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u2_5", name: "Desenvolvimento Máquina", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u2_6", name: "Rosca Scott", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "u2_7", name: "Tríceps Corda", sets: [{t:"AJUSTE", r:"4-6", d:90}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] }
            ],
            "LOWER 2": [
                { id: "l2_1", name: "Flexor Sentado", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l2_2", name: "Flexor Deitado", sets: [{t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l2_3", name: "Elevação de Quadril", sets: [{t:"AQUEC", r:"10-15", d:45}, {t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l2_4", name: "Hack", sets: [{t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] },
                { id: "l2_5", name: "Leg 45", sets: [{t:"TRABALHO", r:"6-10", d:120}, {t:"TRABALHO", r:"6-10", d:120}] }
            ]
        };

        const DAYS = ["SEGUNDA", "TERÇA", "QUINTA", "SEXTA"];
        const SCHEDULE = { "SEGUNDA": "UPPER 1", "TERÇA": "LOWER 1", "QUINTA": "UPPER 2", "SEXTA": "LOWER 2" };

        function App() {
            const [view, setView] = useState("TREINO");
            const [selectedDay, setSelectedDay] = useState("SEGUNDA");
            const [completed, setCompleted] = useState(() => JSON.parse(localStorage.getItem('bg_c') || '{}'));
            const [weights, setWeights] = useState(() => JSON.parse(localStorage.getItem('bg_w') || '{}'));
            const [videoLinks, setVideoLinks] = useState(() => JSON.parse(localStorage.getItem('bg_v') || '{}'));
            const [history, setHistory] = useState(() => JSON.parse(localStorage.getItem('bg_h') || '[]'));
            
            const [timer, setTimer] = useState(0);
            const [isPaused, setIsPaused] = useState(false);

            useEffect(() => {
                localStorage.setItem('bg_c', JSON.stringify(completed));
                localStorage.setItem('bg_w', JSON.stringify(weights));
                localStorage.setItem('bg_v', JSON.stringify(videoLinks));
                localStorage.setItem('bg_h', JSON.stringify(history));
            }, [completed, weights, videoLinks, history]);

            useEffect(() => {
                let interval;
                if (timer > 0 && !isPaused) interval = setInterval(() => setTimer(t => t - 1), 1000);
                if (timer === 1 && !isPaused) falarAviso();
                return () => clearInterval(interval);
            }, [timer, isPaused]);

            const falarAviso = () => {
                if ('speechSynthesis' in window) {
                    window.speechSynthesis.cancel();
                    const msg = new SpeechSynthesisUtterance("Descanso finalizado. Boa série!");
                    msg.lang = 'pt-BR';
                    window.speechSynthesis.speak(msg);
                }
            };

            const finalizarTreino = () => {
                if (!confirm("Salvar treino no Histórico e resetar hoje?")) return;
                const entry = { id: Date.now(), date: new Date().toLocaleDateString('pt-BR'), workout: selectedDay };
                setHistory([entry, ...history]);
                setCompleted({});
                alert("Treino salvo!");
            };

            const saveLink = (id) => {
                const link = prompt("Cole o link do vídeo aqui:");
                if (link) setVideoLinks({...videoLinks, [id]: link});
            };

            const currentKey = SCHEDULE[selectedDay];

            return (
                <div className="max-w-md mx-auto min-h-screen pb-64">
                    <header className="p-6 bg-black sticky top-0 z-50 border-b border-zinc-900 shadow-2xl">
                        <div className="flex justify-between items-center mb-6">
                            <h1 className="text-xl font-brand italic accent">BEYOND 2.0</h1>
                            <div className="flex gap-2">
                                <button onClick={() => { window.speechSynthesis.speak(new SpeechSynthesisUtterance("Voz ativa")); alert("Som ativado!"); }} className="text-[9px] border border-zinc-800 px-2 py-1.5 rounded text-zinc-500 font-bold uppercase">Ativar Voz</button>
                                <button onClick={() => setView(view === "TREINO" ? "HISTORICO" : "TREINO")} className="text-[10px] bg-zinc-900 border border-zinc-800 px-3 py-2 rounded-lg font-black uppercase text-zinc-400">
                                    {view === "TREINO" ? "Histórico" : "Voltar"}
                                </button>
                            </div>
                        </div>
                        {view === "TREINO" && (
                            <div className="flex justify-between gap-1 overflow-x-auto no-scrollbar">
                                {DAYS.map(d => (
                                    <button key={d} onClick={() => setSelectedDay(d)} className={`px-4 py-2 rounded-xl text-[10px] font-black transition-all ${selectedDay === d ? 'bg-accent text-black shadow-lg shadow-orange-900/40' : 'bg-zinc-900 text-zinc-600'}`}>{d}</button>
                                ))}
                            </div>
                        )}
                    </header>

                    <main className="p-4">
                        {view === "HISTORICO" ? (
                            <div className="space-y-4">
                                <h2 className="font-brand text-orange-500 text-xl mb-6 uppercase">Histórico</h2>
                                {history.length === 0 && <p className="text-zinc-600 italic">Nenhum treino salvo.</p>}
                                {history.map(h => (
                                    <div key={h.id} className="bg-card p-4 border border-zinc-900 flex justify-between items-center">
                                        <span className="font-bold text-zinc-100 uppercase text-xs">{h.workout}</span>
                                        <span className="text-[10px] text-zinc-500 font-bold tracking-widest">{h.date}</span>
                                    </div>
                                ))}
                                <button onClick={() => { if(confirm("Limpar histórico?")) setHistory([]) }} className="w-full py-4 text-zinc-800 text-[10px] font-bold uppercase mt-10">Limpar Tudo</button>
                            </div>
                        ) : (
                            <div className="space-y-6">
                                <h2 className="text-zinc-700 font-black italic text-[10px] uppercase tracking-[0.3em] ml-2">{currentKey}</h2>
                                {WORKOUT_DATA[currentKey].map((ex) => (
                                    <div key={ex.id} className="bg-card p-5 border border-zinc-800/50">
                                        <div className="flex justify-between items-center mb-6">
                                            <h3 className="font-black uppercase italic text-xs leading-tight w-2/3 tracking-tight">{ex.name}</h3>
                                            <div className="flex gap-2">
                                                <button onClick={() => saveLink(ex.id)} className="p-2 bg-zinc-900 rounded-lg text-zinc-700 border border-zinc-800">
                                                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="3"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path></svg>
                                                </button>
                                                <button onClick={() => window.open(videoLinks[ex.id] || `https://www.youtube.com/results?search_query=pacholok+${ex.name}`, '_blank')} className="bg-accent text-black text-[9px] font-black px-4 py-2 rounded-xl uppercase italic shadow-lg">Vídeo</button>
                                            </div>
                                        </div>
                                        <div className="space-y-3">
                                            {ex.sets.map((set, sIdx) => {
                                                const id = `${selectedDay}-${ex.id}-${sIdx}`;
                                                const isDone = completed[id];
                                                const tagClass = set.t === "AQUEC" ? "tag-aquec" : set.t === "AJUSTE" ? "tag-ajuste" : "tag-trabalho";
                                                return (
                                                    <div key={sIdx} className={`flex items-center justify-between p-4 rounded-2xl border transition-all ${isDone ? 'border-orange-500 bg-orange-500/10 shadow-[0_0_10px_rgba(255,95,0,0.1)]' : 'border-zinc-900 bg-zinc-900/10'}`}>
                                                        <div className="flex flex-col">
                                                            <div className="flex items-center gap-2 mb-1">
                                                                <span className={`px-2 py-0.5 rounded text-[8px] font-black uppercase tracking-tighter ${tagClass}`}>{set.t}</span>
                                                                <span className="text-[8px] text-zinc-700 font-bold">{set.d}s</span>
                                                            </div>
                                                            <span className="text-sm font-black italic">{set.r} REPS</span>
                                                        </div>
                                                        <div className="flex items-center gap-3">
                                                            <input type="number" placeholder="kg" value={weights[id] || ''} onChange={(e) => setWeights({...weights, [id]: e.target.value})} />
                                                            <button onClick={() => { setCompleted({...completed, [id]: !isDone}); if(!isDone) { setTimer(set.d); setIsPaused(false); } }} className={`w-12 h-12 rounded-xl flex items-center justify-center transition-all ${isDone ? 'bg-accent text-black shadow-lg shadow-orange-900/30' : 'bg-zinc-800 text-zinc-700'}`}>
                                                                {isDone ? <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="4"><polyline points="20 6 9 17 4 12"/></svg> : <div className="w-1.5 h-1.5 rounded-full bg-zinc-700"></div>}
                                                            </button>
                                                        </div>
                                                    </div>
                                                );
                                            })}
                                        </div>
                                    </div>
                                ))}
                                <button onClick={finalizarTreino} className="w-full py-6 mt-10 bg-zinc-900 rounded-3xl font-brand accent text-lg border border-orange-500/20 active:scale-95">FINALIZAR TREINO</button>
                            </div>
                        )}
                    </main>

                    {timer > 0 && (
                        <div className="fixed bottom-0 left-0 w-full timer-panel p-6 z-[60] animate-in slide-in-from-bottom">
                            <div className="max-w-md mx-auto flex items-center justify-between">
                                <div className="flex flex-col">
                                    <span className="text-[10px] font-black uppercase text-orange-500 tracking-widest mb-1">Descanso Ativo</span>
                                    <span className="text-7xl font-brand italic accent leading-none tabular-nums">{timer}s</span>
                                </div>
                                <div className="flex flex-col gap-2">
                                    <button onClick={() => setTimer(t => t + 30)} className="w-14 h-10 rounded-xl bg-zinc-900 border border-zinc-800 font-bold text-xs">+30s</button>
                                    <button onClick={() => setIsPaused(!isPaused)} className="px-6 h-10 rounded-xl bg-white text-black font-black uppercase text-[10px] italic">{isPaused ? 'Play' : 'Pause'}</button>
                                    <button onClick={() => setTimer(0)} className="w-14 h-10 rounded-xl bg-zinc-900 text-zinc-500 font-bold text-xs">X</button>
                                </div>
                            </div>
                        </div>
                    )}
                </div>
            );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>

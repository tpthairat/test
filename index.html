import React, { useState, useEffect, useRef } from 'react';
import { 
  BookOpen, Info, ArrowRight, Clock, CheckCircle, XCircle, 
  Lightbulb, Trophy, Frown, RotateCcw, Home, Settings, 
  ArrowLeft, UploadCloud, Save, Database, AlertCircle,
  Briefcase, GraduationCap, Star, ChevronRight, Loader2, RefreshCw
} from 'lucide-react';
import { initializeApp } from 'firebase/app';
import { 
  getAuth, 
  signInAnonymously, 
  onAuthStateChanged,
  signInWithCustomToken
} from 'firebase/auth';
import { 
  getFirestore, 
  collection, 
  addDoc, 
  onSnapshot,
  query,
  writeBatch
} from 'firebase/firestore';

// --- Firebase Initialization ---
let firebaseConfig;
let appId;

try {
  // พยายามใช้ค่า Config จาก Environment ก่อน
  if (typeof __firebase_config !== 'undefined') {
    firebaseConfig = JSON.parse(__firebase_config);
    appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
  } else {
    throw new Error('No environment config');
  }
} catch (e) {
  // Fallback Config (หากรันใน Local หรือไม่มี Env)
  firebaseConfig = {
    apiKey: "AIzaSyAa1BBpDBC88rmmrxoQ1FzaevgXjlbOZJ8",
    authDomain: "local-68-68d5c.firebaseapp.com",
    databaseURL: "https://local-68-68d5c-default-rtdb.firebaseio.com",
    projectId: "local-68-68d5c",
    storageBucket: "local-68-68d5c.firebasestorage.app",
    messagingSenderId: "478841571906",
    appId: "1:478841571906:web:6cc77709f37b1b0274fbdb",
    measurementId: "G-JBDWTML70S"
  };
  // ใช้ค่า default สำหรับ Local testing เพื่อให้ Path ถูกต้องตามกฎ
  appId = 'local-exam-app-v1'; 
}

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// --- Mock Data สำหรับการ Seed ข้อมูลเบื้องต้น ---
const INITIAL_QUESTIONS = [
    // ภาค ก
    {
        part: 'A',
        category: "ความสามารถทั่วไป (คณิตศาสตร์)",
        question: "จงหาตัวเลขถัดไปของอนุกรม: 2, 5, 10, 17, ...",
        options: ["24", "25", "26", "27"],
        correctAnswer: 2, 
        explanation: "ผลต่างชั้นที่ 1 คือ 3, 5, 7 ... ซึ่งเพิ่มทีละ 2 ดังนั้นตัวถัดไปต้องบวกด้วย 9 (17 + 9 = 26)",
        createdAt: Date.now()
    },
    {
        part: 'A',
        category: "ภาษาไทย (คำราชาศัพท์)",
        question: "คำว่า 'พระอัยกา' หมายถึงข้อใด?",
        options: ["พ่อ", "ปู่ หรือ ตา", "ลุง", "พี่ชาย"],
        correctAnswer: 1,
        explanation: "พระอัยกา หมายถึง ปู่ หรือ ตา ส่วน พระอัยกี หมายถึง ย่า หรือ ยาย",
        createdAt: Date.now() + 1
    },
    {
        part: 'A',
        category: "ภาษาอังกฤษ (Grammar)",
        question: "She _______ to the market yesterday.",
        options: ["go", "goes", "went", "gone"],
        correctAnswer: 2,
        explanation: "ประโยคมีคำว่า 'yesterday' เป็นอดีต (Past Simple Tense) กริยาช่อง 2 ของ go คือ went",
        createdAt: Date.now() + 2
    },
    // ภาค ข
    {
        part: 'B',
        category: "ระเบียบงานสารบรรณ",
        question: "หนังสือราชการมีกี่ชนิด?",
        options: ["4 ชนิด", "5 ชนิด", "6 ชนิด", "7 ชนิด"],
        correctAnswer: 2,
        explanation: "หนังสือราชการมี 6 ชนิด ได้แก่ หนังสือภายนอก, ภายใน, ประทับตรา, สั่งการ, ประชาสัมพันธ์, และหนังสือที่เจ้าหน้าที่ทำขึ้นหรือรับไว้เป็นหลักฐาน",
        createdAt: Date.now() + 3
    },
    {
        part: 'B',
        category: "พ.ร.บ. ข้อมูลข่าวสาร",
        question: "ข้อมูลข่าวสารของราชการที่ลงพิมพ์ในราชกิจจานุเบกษาแล้ว ให้ถือว่า?",
        options: ["เป็นความลับ", "ทุกคนรับทราบแล้ว", "ใช้บังคับได้ทันที", "ไม่ต้องเผยแพร่ซ้ำ"],
        correctAnswer: 1,
        explanation: "เมื่อลงพิมพ์ในราชกิจจานุเบกษาแล้ว ให้ถือว่าทุกคนได้รับทราบข้อมูลข่าวสารนั้นแล้ว",
        createdAt: Date.now() + 4
    }
];

// --- Helper Function: CSV Parser ---
const parseCSV = (text) => {
    const lines = text.split('\n');
    const result = [];
    
    // ตรวจสอบ Header
    const startRow = lines[0].toLowerCase().includes('question') ? 1 : 0;

    for (let i = startRow; i < lines.length; i++) {
        const line = lines[i].trim();
        if (!line) continue;

        const parts = line.split(/,(?=(?:(?:[^"]*"){2})*[^"]*$)/); 
        const clean = (str) => str ? str.replace(/^"|"$/g, '').trim() : "";

        if (parts.length === 7) {
             result.push({
                part: 'A', 
                category: 'ทั่วไป', 
                question: clean(parts[0]),
                options: [clean(parts[1]), clean(parts[2]), clean(parts[3]), clean(parts[4])],
                correctAnswer: parseInt(clean(parts[5])) - 1, 
                explanation: clean(parts[6]),
                createdAt: Date.now() + i
            });
        }
        else if (parts.length >= 9) {
            result.push({
                part: clean(parts[0]).toUpperCase(), 
                category: clean(parts[1]),
                question: clean(parts[2]),
                options: [clean(parts[3]), clean(parts[4]), clean(parts[5]), clean(parts[6])],
                correctAnswer: parseInt(clean(parts[7])) - 1,
                explanation: clean(parts[8]),
                createdAt: Date.now() + i
            });
        }
    }
    return result;
};

// --- Components ---

// 1. Welcome Screen (Optimized for Mobile)
const WelcomeScreen = ({ onSelectPart, goToAdmin, questionCounts, isLoading, authError }) => (
    <div className="flex flex-col items-center justify-center min-h-screen p-4 md:p-6 text-center fade-in relative overflow-hidden">
        {/* Admin Button - Adjusted position for safe area */}
        <button 
            onClick={goToAdmin}
            className="absolute top-4 right-4 md:top-6 md:right-6 p-2 md:p-3 bg-white/50 backdrop-blur-md text-slate-600 hover:bg-white/80 rounded-full transition-all shadow-lg border border-white/40 z-20 active:scale-95"
            title="เข้าสู่ระบบจัดการข้อสอบ"
        >
            <Settings size={20} className="md:w-6 md:h-6" />
        </button>

        <div className="max-w-5xl w-full z-10 flex flex-col justify-center min-h-[80vh]">
            <div className="mb-8 md:mb-12 animate-slide-up">
                <div className="inline-flex items-center justify-center p-4 md:p-6 bg-gradient-to-br from-blue-600 to-indigo-700 rounded-3xl shadow-xl mb-4 md:mb-6 ring-4 ring-blue-100">
                    <BookOpen size={48} className="text-white drop-shadow-md md:w-16 md:h-16" />
                </div>
                <h1 className="text-4xl sm:text-5xl md:text-6xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-slate-800 to-slate-600 mb-2 md:mb-4 tracking-tight drop-shadow-sm">
                    คลังข้อสอบราชการ
                </h1>
                <p className="text-slate-600 text-base sm:text-lg md:text-xl font-light tracking-wide max-w-2xl mx-auto px-4">
                    แพลตฟอร์มจำลองสนามสอบเสมือนจริง<br className="hidden sm:block"/> เตรียมความพร้อมสู่ความสำเร็จ
                </p>
            </div>

            {isLoading ? (
                <div className="flex flex-col items-center justify-center h-48 md:h-64 text-slate-500 animate-pulse">
                    <Loader2 size={40} className="animate-spin mb-4 text-blue-500 md:w-12 md:h-12" />
                    <p className="text-sm md:text-base">กำลังเชื่อมต่อฐานข้อมูล...</p>
                </div>
            ) : authError ? (
                <div className="mx-4 flex flex-col items-center justify-center text-red-500 bg-red-50 rounded-3xl p-6 border border-red-200 shadow-sm">
                    <AlertCircle size={40} className="mb-3 md:w-12 md:h-12" />
                    <h3 className="text-base md:text-lg font-bold">เกิดข้อผิดพลาดในการเชื่อมต่อ</h3>
                    <p className="text-xs md:text-sm mb-2">{authError}</p>
                    <p className="text-xs text-slate-500 mt-2">
                        ระบบกำลังพยายามเชื่อมต่อใหม่...
                    </p>
                </div>
            ) : (
                <div className="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-8 max-w-3xl mx-auto w-full px-2 sm:px-4">
                    {/* Card Part A */}
                    <button 
                        onClick={() => onSelectPart('A')}
                        className="group relative bg-white/80 backdrop-blur-xl p-6 md:p-8 rounded-[1.5rem] md:rounded-[2rem] shadow-lg hover:shadow-2xl hover:shadow-blue-500/20 transition-all duration-300 transform active:scale-[0.98] md:hover:-translate-y-2 text-left border border-white/50 overflow-hidden"
                    >
                        <div className="absolute top-0 right-0 w-24 h-24 md:w-32 md:h-32 bg-gradient-to-br from-blue-400/20 to-purple-400/20 rounded-bl-[3rem] md:rounded-bl-[4rem] -mr-6 -mt-6 transition-all group-hover:scale-110"></div>
                        
                        <div className="relative z-10">
                            <div className="flex items-start justify-between mb-4 md:mb-6">
                                <div className="p-3 md:p-4 bg-gradient-to-br from-blue-500 to-indigo-600 rounded-xl md:rounded-2xl shadow-lg text-white group-hover:scale-110 transition-transform duration-300">
                                    <GraduationCap size={24} className="md:w-8 md:h-8" />
                                </div>
                                <div className="flex items-center gap-1 bg-blue-50 text-blue-700 px-2 py-1 md:px-3 rounded-full text-xs font-bold shadow-inner">
                                    <Star size={10} fill="currentColor" className="md:w-3 md:h-3" /> {questionCounts.A || 0} ข้อ
                                </div>
                            </div>
                            
                            <h2 className="text-xl md:text-2xl font-bold text-gray-800 mb-1 md:mb-2 group-hover:text-blue-700 transition-colors">ภาค ก</h2>
                            <p className="text-gray-500 text-xs md:text-sm mb-4 md:mb-6 line-clamp-1">ความรู้ความสามารถทั่วไป (คณิต, ไทย, อังกฤษ)</p>
                            
                            <div className="flex items-center text-blue-600 font-semibold text-sm md:text-base group-hover:translate-x-2 transition-transform">
                                เริ่มทดสอบ <ChevronRight size={16} className="md:w-5 md:h-5 ml-1" />
                            </div>
                        </div>
                    </button>

                    {/* Card Part B */}
                    <button 
                        onClick={() => onSelectPart('B')}
                        className="group relative bg-white/80 backdrop-blur-xl p-6 md:p-8 rounded-[1.5rem] md:rounded-[2rem] shadow-lg hover:shadow-2xl hover:shadow-purple-500/20 transition-all duration-300 transform active:scale-[0.98] md:hover:-translate-y-2 text-left border border-white/50 overflow-hidden"
                    >
                        <div className="absolute top-0 right-0 w-24 h-24 md:w-32 md:h-32 bg-gradient-to-br from-purple-400/20 to-pink-400/20 rounded-bl-[3rem] md:rounded-bl-[4rem] -mr-6 -mt-6 transition-all group-hover:scale-110"></div>

                        <div className="relative z-10">
                            <div className="flex items-start justify-between mb-4 md:mb-6">
                                <div className="p-3 md:p-4 bg-gradient-to-br from-purple-500 to-fuchsia-600 rounded-xl md:rounded-2xl shadow-lg text-white group-hover:scale-110 transition-transform duration-300">
                                    <Briefcase size={24} className="md:w-8 md:h-8" />
                                </div>
                                <div className="flex items-center gap-1 bg-purple-50 text-purple-700 px-2 py-1 md:px-3 rounded-full text-xs font-bold shadow-inner">
                                    <Star size={10} fill="currentColor" className="md:w-3 md:h-3" /> {questionCounts.B || 0} ข้อ
                                </div>
                            </div>
                            
                            <h2 className="text-xl md:text-2xl font-bold text-gray-800 mb-1 md:mb-2 group-hover:text-purple-700 transition-colors">ภาค ข</h2>
                            <p className="text-gray-500 text-xs md:text-sm mb-4 md:mb-6 line-clamp-1">ความรู้ความสามารถเฉพาะตำแหน่ง (กฎหมาย)</p>
                            
                            <div className="flex items-center text-purple-600 font-semibold text-sm md:text-base group-hover:translate-x-2 transition-transform">
                                เริ่มทดสอบ <ChevronRight size={16} className="md:w-5 md:h-5 ml-1" />
                            </div>
                        </div>
                    </button>
                </div>
            )}

            <div className="mt-8 md:mt-16 text-slate-500 text-xs md:text-sm flex items-center justify-center gap-2 font-medium pb-4">
                <Info size={14} className="md:w-4 md:h-4" />
                <span>เกณฑ์การผ่าน 60% ในแต่ละชุดวิชา</span>
            </div>
        </div>
    </div>
);

// 2. Quiz Screen (Optimized for Mobile)
const QuizScreen = ({ questions, finishQuiz, partName }) => {
    const [currentQuestionIndex, setCurrentQuestionIndex] = useState(0);
    const [selectedOption, setSelectedOption] = useState(null);
    const [score, setScore] = useState(0);
    const [showExplanation, setShowExplanation] = useState(false);
    const [timeLeft, setTimeLeft] = useState(60 * questions.length); 

    useEffect(() => {
        setCurrentQuestionIndex(0);
        setSelectedOption(null);
        setScore(0);
        setShowExplanation(false);
        setTimeLeft(60 * questions.length);
    }, [questions]);

    useEffect(() => {
        const timer = setInterval(() => {
            setTimeLeft((prev) => {
                if (prev <= 1) {
                    clearInterval(timer);
                    finishQuiz(score);
                    return 0;
                }
                return prev - 1;
            });
        }, 1000);
        return () => clearInterval(timer);
    }, [score, finishQuiz, questions.length]);

    const handleOptionClick = (index) => {
        if (selectedOption !== null) return;
        setSelectedOption(index);
        const isCorrect = index === questions[currentQuestionIndex].correctAnswer;
        if (isCorrect) setScore((prev) => prev + 1);
        setShowExplanation(true);
    };

    const nextQuestion = () => {
        const nextIndex = currentQuestionIndex + 1;
        if (nextIndex < questions.length) {
            setCurrentQuestionIndex(nextIndex);
            setSelectedOption(null);
            setShowExplanation(false);
        } else {
            finishQuiz(score);
        }
    };

    const formatTime = (seconds) => {
        const mins = Math.floor(seconds / 60);
        const secs = seconds % 60;
        return `${mins}:${secs < 10 ? '0' : ''}${secs}`;
    };

    if (questions.length === 0) return <div className="min-h-screen flex items-center justify-center text-slate-500 font-bold text-xl">ไม่พบข้อสอบในระบบ</div>;

    const currentQ = questions[currentQuestionIndex];
    const progress = ((currentQuestionIndex + 1) / questions.length) * 100;

    return (
        <div className="min-h-screen p-3 md:p-4 flex flex-col items-center justify-start pt-4 md:pt-8 pb-8">
            {/* Glass Header - More compact on mobile */}
            <div className="w-full max-w-3xl bg-white/90 backdrop-blur-xl p-3 md:p-4 rounded-2xl md:rounded-3xl shadow-lg mb-4 md:mb-8 flex justify-between items-center border border-white/50 z-10 sticky top-2 md:top-4">
                <div className="flex items-center gap-2 md:gap-3">
                    <span className="hidden sm:inline-block bg-gradient-to-r from-slate-800 to-slate-900 text-white px-3 py-1 md:px-4 md:py-1.5 rounded-full text-[10px] md:text-xs font-bold shadow-md tracking-wide">
                        {partName}
                    </span>
                    <span className="text-slate-600 font-semibold text-xs md:text-sm">
                        ข้อที่ <span className="text-blue-600 text-base md:text-lg">{currentQuestionIndex + 1}</span> <span className="text-gray-400">/ {questions.length}</span>
                    </span>
                </div>
                <div className={`flex items-center gap-1 md:gap-2 font-mono text-base md:text-xl font-bold px-3 py-1 md:px-4 rounded-xl ${timeLeft < 60 ? 'bg-red-50 text-red-500 animate-pulse border border-red-100' : 'bg-slate-50 text-slate-700 border border-slate-100'}`}>
                    <Clock size={16} className="md:w-5 md:h-5" />
                    {formatTime(timeLeft)}
                </div>
            </div>

            {/* Question Card */}
            <div className="w-full max-w-3xl bg-white/95 backdrop-blur-xl p-6 md:p-10 rounded-[1.5rem] md:rounded-[2.5rem] shadow-2xl relative overflow-hidden z-10 border border-white/60 animate-fade-in-up">
                <div className="absolute top-0 left-0 w-full h-1.5 md:h-2 bg-gray-100">
                    <div className="bg-gradient-to-r from-blue-500 to-indigo-600 h-full transition-all duration-700 ease-out shadow-[0_0_10px_rgba(59,130,246,0.5)]" style={{ width: `${progress}%` }}></div>
                </div>

                <div className="mb-6 md:mb-8 mt-2 md:mt-4">
                    <span className="inline-block text-[10px] md:text-xs font-bold tracking-wider text-indigo-500 bg-indigo-50 px-2 py-1 md:px-3 rounded-lg uppercase mb-2 md:mb-4 border border-indigo-100">
                        {currentQ.category}
                    </span>
                    <h2 className="text-lg sm:text-xl md:text-3xl font-bold text-gray-800 leading-relaxed">
                        {currentQ.question}
                    </h2>
                </div>

                <div className="space-y-3 md:space-y-4">
                    {currentQ.options.map((option, idx) => {
                        let btnClass = "w-full text-left p-4 md:p-5 rounded-xl md:rounded-2xl border-2 transition-all duration-300 relative group text-base md:text-lg font-medium active:scale-[0.99] ";
                        
                        if (selectedOption === null) {
                            btnClass += "border-transparent bg-slate-50 hover:bg-white hover:border-blue-300 hover:shadow-lg hover:-translate-y-1 text-slate-600";
                        } else {
                            if (idx === currentQ.correctAnswer) {
                                btnClass += "border-green-400 bg-green-50/50 text-green-800 shadow-md";
                            } else if (idx === selectedOption) {
                                btnClass += "border-red-400 bg-red-50/50 text-red-800";
                            } else {
                                btnClass += "border-transparent bg-slate-50 text-slate-300 opacity-60 grayscale";
                            }
                        }

                        return (
                            <button
                                key={idx}
                                onClick={() => handleOptionClick(idx)}
                                disabled={selectedOption !== null}
                                className={btnClass}
                            >
                                <span className="flex items-center justify-between">
                                    <span>{idx + 1}. {option}</span>
                                    {selectedOption !== null && idx === currentQ.correctAnswer && (
                                        <CheckCircle className="text-green-500 drop-shadow-sm flex-shrink-0" size={20} />
                                    )}
                                    {selectedOption === idx && idx !== currentQ.correctAnswer && (
                                        <XCircle className="text-red-500 drop-shadow-sm flex-shrink-0" size={20} />
                                    )}
                                </span>
                            </button>
                        );
                    })}
                </div>

                {showExplanation && (
                    <div className="mt-6 md:mt-8 overflow-hidden rounded-xl md:rounded-2xl bg-gradient-to-br from-blue-50 to-indigo-50 border border-blue-100 animate-fade-in-up">
                        <div className="p-4 md:p-6">
                            <h3 className="font-bold text-blue-800 mb-2 flex items-center gap-2 text-base md:text-lg">
                                <Lightbulb size={20} className="text-yellow-500 md:w-6 md:h-6" /> คำอธิบาย
                            </h3>
                            <p className="text-slate-700 text-sm md:text-base leading-relaxed pl-7 md:pl-8">{currentQ.explanation}</p>
                        </div>
                        <div className="bg-blue-100/50 p-3 md:p-4 flex justify-end border-t border-blue-100">
                            <button 
                                onClick={nextQuestion}
                                className="bg-gradient-to-r from-blue-600 to-indigo-700 text-white px-6 py-2 md:px-8 md:py-3 rounded-lg md:rounded-xl font-bold hover:shadow-lg hover:scale-105 active:scale-95 transition-all flex items-center gap-2 shadow-blue-500/30 text-sm md:text-base"
                            >
                                ข้อถัดไป <ArrowRight size={18} className="md:w-5 md:h-5" />
                            </button>
                        </div>
                    </div>
                )}
            </div>
        </div>
    );
};

// 3. Result Screen (Optimized for Mobile)
const ResultScreen = ({ score, total, restartQuiz, goHome, partName }) => {
    const percentage = total > 0 ? (score / total) * 100 : 0;
    const isPassed = percentage >= 60;

    return (
        <div className="min-h-screen flex items-center justify-center p-4 fade-in">
            <div className="bg-white/95 backdrop-blur-2xl p-6 md:p-12 rounded-[2rem] md:rounded-[3rem] shadow-2xl max-w-lg w-full text-center relative overflow-hidden border border-white/60 animate-pop-in">
                <div className={`absolute top-0 left-0 w-full h-1.5 md:h-2 bg-gradient-to-r ${isPassed ? 'from-green-400 to-emerald-500' : 'from-red-400 to-orange-500'}`}></div>
                <div className={`absolute -top-20 -right-20 w-64 h-64 rounded-full opacity-10 blur-3xl ${isPassed ? 'bg-green-500' : 'bg-red-500'}`}></div>
                <div className={`absolute -bottom-20 -left-20 w-64 h-64 rounded-full opacity-10 blur-3xl ${isPassed ? 'bg-emerald-500' : 'bg-orange-500'}`}></div>

                <div className="relative mb-4 md:mb-6">
                    <div className={`w-24 h-24 md:w-32 md:h-32 mx-auto rounded-full bg-gradient-to-br ${isPassed ? 'from-green-100 to-emerald-50 border-4 border-green-200' : 'from-red-100 to-orange-50 border-4 border-red-200'} shadow-xl flex items-center justify-center`}>
                        {isPassed ? 
                            <Trophy size={48} className="text-green-600 drop-shadow-sm md:w-16 md:h-16" /> : 
                            <Frown size={48} className="text-red-500 drop-shadow-sm md:w-16 md:h-16" />
                        }
                    </div>
                    {isPassed && <div className="absolute top-0 right-1/4 animate-bounce"><Star size={20} className="text-yellow-400 fill-current md:w-6 md:h-6" /></div>}
                </div>

                <span className="inline-block px-3 py-1 bg-slate-100 text-slate-500 rounded-full text-[10px] md:text-xs font-bold uppercase tracking-wider mb-2 md:mb-4 border border-slate-200">
                    {partName}
                </span>

                <h2 className={`text-2xl md:text-3xl font-extrabold mb-1 md:mb-2 ${isPassed ? 'text-green-700' : 'text-red-600'}`}>
                    {isPassed ? "สอบผ่าน!" : "สอบไม่ผ่าน"}
                </h2>
                <p className="text-slate-500 mb-6 md:mb-8 font-medium text-sm md:text-base">
                    {isPassed ? "ยินดีด้วย คุณมีความพร้อมสำหรับการสอบจริง" : "ไม่ต้องเสียใจ ลองทบทวนเนื้อหาและสอบใหม่อีกครั้ง"}
                </p>

                <div className="flex justify-center gap-3 md:gap-4 mb-8 md:mb-10">
                    <div className="bg-slate-50 p-3 md:p-5 rounded-2xl md:rounded-3xl border border-slate-100 w-24 md:w-32 shadow-sm">
                        <span className="block text-slate-400 text-[10px] md:text-xs font-bold mb-1">คะแนนที่ได้</span>
                        <span className="block text-2xl md:text-4xl font-black text-slate-800">{score}</span>
                    </div>
                    <div className="bg-slate-50 p-3 md:p-5 rounded-2xl md:rounded-3xl border border-slate-100 w-24 md:w-32 shadow-sm">
                        <span className="block text-slate-400 text-[10px] md:text-xs font-bold mb-1">จากเต็ม</span>
                        <span className="block text-2xl md:text-4xl font-black text-slate-400">{total}</span>
                    </div>
                </div>

                <div className="space-y-3 relative z-10">
                    <button 
                        onClick={restartQuiz}
                        className="w-full bg-slate-800 text-white font-bold py-3 md:py-4 rounded-xl md:rounded-2xl hover:bg-slate-900 active:scale-[0.98] transition-all flex items-center justify-center gap-2 text-sm md:text-base"
                    >
                        <RotateCcw size={18} className="md:w-5 md:h-5" /> ทำข้อสอบใหม่อีกครั้ง
                    </button>
                    <button 
                        onClick={goHome}
                        className="w-full bg-white border-2 border-slate-200 text-slate-600 font-bold py-3 md:py-4 rounded-xl md:rounded-2xl hover:bg-slate-50 active:scale-[0.98] transition-all flex items-center justify-center gap-2 text-sm md:text-base"
                    >
                        <Home size={18} className="md:w-5 md:h-5" /> กลับหน้าหลัก
                    </button>
                </div>
            </div>
        </div>
    );
};

// 4. Admin Screen (Optimized for Mobile)
const AdminScreen = ({ goBack, onAddQuestions, currentCount, onSeedData, isSaving }) => {
    const [previewData, setPreviewData] = useState([]);
    const [errorMsg, setErrorMsg] = useState("");
    const fileInputRef = useRef(null);

    const handleFileChange = (e) => {
        const file = e.target.files[0];
        if (!file) return;

        const reader = new FileReader();
        reader.onload = (event) => {
            try {
                const parsed = parseCSV(event.target.result);
                if (parsed.length === 0) {
                    setErrorMsg("ไม่พบข้อมูล หรือรูปแบบไฟล์ไม่ถูกต้อง");
                    setPreviewData([]);
                } else {
                    setPreviewData(parsed);
                    setErrorMsg("");
                }
            } catch (err) {
                setErrorMsg("เกิดข้อผิดพลาดในการอ่านไฟล์");
            }
        };
        reader.readAsText(file);
    };

    const handleSave = async () => {
        if (previewData.length > 0) {
            await onAddQuestions(previewData);
            setPreviewData([]);
            if(fileInputRef.current) fileInputRef.current.value = "";
        }
    };

    const exampleCSV = `"โจทย์คำถาม...","ตัวเลือก 1","ตัวเลือก 2","ตัวเลือก 3","ตัวเลือก 4","1","คำอธิบายเฉลย..."
"1 + 1 เท่ากับเท่าไหร่","1","2","3","4","2","เพราะ 1+1 = 2"`;

    return (
        <div className="min-h-screen p-4 fade-in overflow-y-auto">
            <div className="max-w-5xl mx-auto bg-white/95 backdrop-blur-xl rounded-[1.5rem] md:rounded-[2.5rem] shadow-2xl p-4 md:p-8 border border-white/60 min-h-[90vh]">
                <div className="flex flex-col sm:flex-row items-center justify-between mb-6 md:mb-8 pb-4 border-b border-slate-100 gap-4">
                    <h2 className="text-2xl md:text-3xl font-bold text-slate-800 flex items-center gap-3">
                        <div className="bg-blue-100 p-2 rounded-xl text-blue-600">
                            <Settings size={24} className="md:w-7 md:h-7" />
                        </div>
                        ระบบจัดการ
                    </h2>
                    <button onClick={goBack} className="text-slate-500 hover:text-slate-800 hover:bg-slate-100 px-4 py-2 rounded-xl transition-all flex items-center gap-2 font-medium text-sm md:text-base w-full sm:w-auto justify-center">
                        <ArrowLeft size={18} className="md:w-5 md:h-5" /> กลับหน้าหลัก
                    </button>
                </div>

                <div className="grid grid-cols-1 md:grid-cols-3 gap-4 md:gap-6 mb-6 md:mb-8">
                    {/* Stats Card */}
                    <div className="bg-gradient-to-br from-blue-600 to-indigo-700 text-white p-6 rounded-3xl shadow-lg shadow-blue-500/30 flex flex-col items-center justify-center text-center col-span-1">
                        <Database size={32} className="mb-2 md:mb-4 opacity-80 md:w-10 md:h-10" />
                        <h3 className="text-blue-100 font-medium mb-1 text-sm md:text-base">ข้อสอบทั้งหมด</h3>
                        <p className="text-4xl md:text-5xl font-bold">{currentCount}</p>
                        <span className="text-xs bg-white/20 px-2 py-1 rounded-full mt-2">Real-time DB</span>
                    </div>

                    {/* Upload Card */}
                    <div className="bg-slate-50 p-4 md:p-6 rounded-3xl border-2 border-dashed border-slate-300 hover:border-blue-400 transition-colors col-span-1 md:col-span-2 flex flex-col justify-center relative">
                        {isSaving && (
                            <div className="absolute inset-0 bg-white/80 flex items-center justify-center rounded-3xl z-10">
                                <div className="flex flex-col items-center text-blue-600">
                                    <Loader2 size={32} className="animate-spin mb-2" />
                                    <span className="font-bold">กำลังบันทึกข้อมูล...</span>
                                </div>
                            </div>
                        )}
                        <h3 className="font-bold text-base md:text-lg mb-4 flex items-center gap-2 text-slate-700">
                            <UploadCloud size={20} className="text-blue-500 md:w-6 md:h-6" /> นำเข้าข้อสอบ (CSV)
                        </h3>
                        
                        <div className="relative group mb-4">
                            <input 
                                type="file" 
                                accept=".csv"
                                onChange={handleFileChange}
                                ref={fileInputRef}
                                className="block w-full text-xs md:text-sm text-slate-500
                                    file:mr-4 file:py-2 md:file:py-3 file:px-4 md:file:px-6
                                    file:rounded-xl file:border-0
                                    file:text-xs md:file:text-sm file:font-bold
                                    file:bg-blue-100 file:text-blue-700
                                    hover:file:bg-blue-200 cursor-pointer
                                "
                            />
                        </div>
                        
                        {/* Seed Button */}
                        {currentCount === 0 && (
                             <button 
                                onClick={onSeedData}
                                className="w-full py-2 bg-slate-200 hover:bg-slate-300 text-slate-600 rounded-xl font-medium text-xs md:text-sm flex items-center justify-center gap-2 transition-colors active:scale-95"
                             >
                                <RefreshCw size={14} /> โหลดข้อมูลตัวอย่าง (Seed Data)
                             </button>
                        )}

                        <div className="mt-4 text-[10px] md:text-xs text-slate-400 flex gap-2 items-center">
                            <Info size={14} /> รองรับไฟล์ CSV Encoding UTF-8 เท่านั้น
                        </div>
                    </div>
                </div>

                {/* Example CSV */}
                <div className="mb-6 md:mb-8 bg-slate-50 p-4 rounded-2xl border border-slate-200">
                    <p className="font-bold text-xs md:text-sm text-slate-600 mb-2">ตัวอย่างรูปแบบไฟล์ CSV (มี " " ครอบทุกช่อง):</p>
                    <pre className="bg-slate-800 text-slate-300 p-3 md:p-4 rounded-xl text-[10px] md:text-xs overflow-x-auto font-mono leading-relaxed shadow-inner whitespace-pre-wrap">
                        {exampleCSV}
                    </pre>
                    <div className="mt-2 text-[10px] md:text-xs text-red-500">
                        * ห้ามมีบรรทัดว่าง<br/>
                        * ห้ามมีคอมม่าเกินจำเป็น<br/>
                        * ข้อความต้องอยู่ในเครื่องหมาย " "<br/>
                        * นำเข้าเป็น: ภาค ก / หมวดทั่วไป
                    </div>
                </div>

                {/* Preview Section */}
                {previewData.length > 0 && (
                    <div className="animate-fade-in-up">
                        <div className="flex flex-col sm:flex-row justify-between items-center mb-4 gap-4">
                            <h3 className="font-bold text-lg md:text-xl text-slate-700 flex items-center gap-2">
                                <span className="w-2 h-6 md:h-8 bg-green-500 rounded-full inline-block"></span>
                                ตัวอย่างข้อมูล ({previewData.length})
                            </h3>
                            <button 
                                onClick={handleSave}
                                disabled={isSaving}
                                className="w-full sm:w-auto bg-green-500 text-white px-6 py-2 md:py-3 rounded-xl font-bold hover:bg-green-600 shadow-lg shadow-green-500/30 flex items-center justify-center gap-2 active:scale-95 transition-transform disabled:opacity-50 disabled:cursor-not-allowed text-sm md:text-base"
                            >
                                {isSaving ? <Loader2 size={18} className="animate-spin md:w-5 md:h-5" /> : <Save size={18} className="md:w-5 md:h-5" />}
                                {isSaving ? 'กำลังบันทึก...' : 'ยืนยันการบันทึก'}
                            </button>
                        </div>

                        <div className="bg-white rounded-2xl md:rounded-3xl shadow-sm overflow-hidden border border-slate-200">
                            <div className="overflow-x-auto max-h-[300px] md:max-h-[400px]">
                                <table className="w-full text-xs md:text-sm text-left text-slate-600">
                                    <thead className="text-[10px] md:text-xs text-slate-500 uppercase bg-slate-50 sticky top-0 z-10 shadow-sm">
                                        <tr>
                                            <th className="px-4 py-3 md:px-6 md:py-4">ส่วน</th>
                                            <th className="px-4 py-3 md:px-6 md:py-4">หมวดหมู่</th>
                                            <th className="px-4 py-3 md:px-6 md:py-4 min-w-[200px]">คำถาม</th>
                                            <th className="px-4 py-3 md:px-6 md:py-4 text-center">เฉลย</th>
                                        </tr>
                                    </thead>
                                    <tbody className="divide-y divide-slate-100">
                                        {previewData.map((row, idx) => (
                                            <tr key={idx} className="bg-white hover:bg-blue-50/50 transition-colors">
                                                <td className="px-4 py-3 md:px-6 md:py-4 font-bold">
                                                    <span className={`px-2 py-1 rounded text-[10px] md:text-xs ${row.part === 'A' ? 'bg-blue-100 text-blue-700' : 'bg-purple-100 text-purple-700'}`}>
                                                        {row.part}
                                                    </span>
                                                </td>
                                                <td className="px-4 py-3 md:px-6 md:py-4 font-medium text-slate-700">{row.category}</td>
                                                <td className="px-4 py-3 md:px-6 md:py-4">{row.question}</td>
                                                <td className="px-4 py-3 md:px-6 md:py-4 text-center font-bold text-green-600">{row.correctAnswer + 1}</td>
                                            </tr>
                                        ))}
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                )}
                
                {errorMsg && (
                    <div className="bg-red-50 text-red-600 p-4 rounded-xl mb-4 border border-red-200 flex items-center gap-3 animate-shake text-sm">
                        <AlertCircle size={20} /> {errorMsg}
                    </div>
                )}
            </div>
        </div>
    );
};

// Main App Component
export default function App() {
    const [gameState, setGameState] = useState('welcome'); 
    const [score, setScore] = useState(0);
    const [questions, setQuestions] = useState([]); 
    const [selectedPart, setSelectedPart] = useState(null); 
    const [activeQuestions, setActiveQuestions] = useState([]);
    
    // Auth & Loading State
    const [user, setUser] = useState(null);
    const [isLoading, setIsLoading] = useState(true);
    const [isSaving, setIsSaving] = useState(false);
    const [authError, setAuthError] = useState(null);

    // --- 1. Authentication ---
    useEffect(() => {
        const initAuth = async () => {
            try {
                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }
            } catch (error) {
                console.error("Auth initialization error:", error);
                setAuthError(error.message);
                setIsLoading(false);
            }
        };
        initAuth();

        const unsubscribe = onAuthStateChanged(auth, (currentUser) => {
            setUser(currentUser);
            if (currentUser) {
                setAuthError(null);
            }
        });
        return () => unsubscribe();
    }, []);

    // --- 2. Data Fetching (Real-time) ---
    useEffect(() => {
        if (!user) return;

        // Use standard 'public' path for shared questions
        const questionsPath = collection(db, 'artifacts', appId, 'public', 'data', 'questions');
        const userQuestionsQuery = query(questionsPath);
        
        const unsubscribe = onSnapshot(userQuestionsQuery, (snapshot) => {
            const loadedQuestions = snapshot.docs.map(doc => ({
                id: doc.id,
                ...doc.data()
            }));
            
            // Client-side sorting by creation time to avoid index requirements
            loadedQuestions.sort((a, b) => (b.createdAt || 0) - (a.createdAt || 0));
            
            setQuestions(loadedQuestions);
            setIsLoading(false);
        }, (error) => {
            console.error("Error fetching questions:", error);
            if (error.code === 'permission-denied') {
                setAuthError("Permission denied: ไม่สามารถเข้าถึงฐานข้อมูลได้");
            }
            setIsLoading(false);
        });

        return () => unsubscribe();
    }, [user]);

    const handleSelectPart = (part) => {
        const filtered = questions.filter(q => q.part === part);
        if(filtered.length === 0) {
            alert("ยังไม่มีข้อสอบในหมวดนี้ กรุณาแจ้งแอดมินหรือเพิ่มข้อสอบ");
            return;
        }
        setSelectedPart(part);
        setActiveQuestions(filtered);
        setScore(0);
        setGameState('quiz');
    };

    const finishQuiz = (finalScore) => {
        setScore(finalScore);
        setGameState('result');
    };

    const restartQuiz = () => {
        setScore(0);
        setGameState('quiz');
    };

    const goHome = () => {
        setGameState('welcome');
        setSelectedPart(null);
    };

    const goAdmin = () => {
        setGameState('admin');
    };

    // --- Add Data to Firestore ---
    const addQuestionsToDB = async (newQuestions) => {
        if (!user) {
            alert("กรุณารอการเชื่อมต่อสักครู่");
            return;
        }
        setIsSaving(true);
        try {
            // Write to the strictly allowed path
            const questionsCol = collection(db, 'artifacts', appId, 'public', 'data', 'questions');
            // Write sequentially to ensure order and avoid batch limits in loop
            for (const q of newQuestions) {
                await addDoc(questionsCol, q);
            }
            
            alert(`บันทึกข้อสอบ ${newQuestions.length} ข้อ เรียบร้อยแล้ว`);
        } catch (error) {
            console.error("Error adding document: ", error);
            alert("เกิดข้อผิดพลาดในการบันทึกข้อมูล (Permission Denied)");
        } finally {
            setIsSaving(false);
        }
    };

    const handleSeedData = async () => {
        if(confirm("ต้องการโหลดข้อมูลตัวอย่างลงฐานข้อมูลหรือไม่?")) {
            await addQuestionsToDB(INITIAL_QUESTIONS);
        }
    };

    const questionCounts = {
        A: questions.filter(q => q.part === 'A').length,
        B: questions.filter(q => q.part === 'B').length
    };

    const getPartName = (part) => {
        return part === 'A' ? "ภาค ก (ความรู้ทั่วไป)" : "ภาค ข (ความรู้เฉพาะตำแหน่ง)";
    };

    return (
        <div className="antialiased text-slate-800 min-h-screen relative overflow-x-hidden font-sarabun selection:bg-blue-200 selection:text-blue-900">
            {/* Background Layers */}
            <div className="fixed inset-0 bg-slate-50 -z-20"></div>
            <div className="fixed inset-0 bg-[radial-gradient(ellipse_at_top_right,_var(--tw-gradient-stops))] from-blue-200/40 via-purple-200/40 to-transparent -z-10 animate-pulse-slow"></div>
            <div className="fixed inset-0 bg-[radial-gradient(ellipse_at_bottom_left,_var(--tw-gradient-stops))] from-indigo-200/40 via-cyan-200/40 to-transparent -z-10 animate-pulse-slow delay-1000"></div>

            <style>{`
                @import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;600;700;800&display=swap');
                
                body {
                    font-family: 'Sarabun', sans-serif;
                }
                
                /* Animation Keyframes */
                @keyframes slideUp {
                    from { opacity: 0; transform: translateY(20px); }
                    to { opacity: 1; transform: translateY(0); }
                }
                @keyframes popIn {
                    0% { opacity: 0; transform: scale(0.9); }
                    100% { opacity: 1; transform: scale(1); }
                }
                @keyframes pulseSlow {
                    0%, 100% { opacity: 0.5; }
                    50% { opacity: 0.8; }
                }
                @keyframes shake {
                    0%, 100% { transform: translateX(0); }
                    25% { transform: translateX(-5px); }
                    75% { transform: translateX(5px); }
                }
                
                .animate-slide-up { animation: slideUp 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
                .animate-pop-in { animation: popIn 0.5s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
                .animate-fade-in-up { animation: slideUp 0.4s ease-out forwards; }
                .animate-pulse-slow { animation: pulseSlow 8s ease-in-out infinite; }
                .animate-shake { animation: shake 0.3s ease-in-out; }
                
                /* Custom Scrollbar */
                ::-webkit-scrollbar { width: 10px; }
                ::-webkit-scrollbar-track { background: transparent; }
                ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 5px; border: 2px solid #f1f5f9; }
                ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
            `}</style>
            
            {gameState === 'welcome' && (
                <WelcomeScreen 
                    onSelectPart={handleSelectPart} 
                    goToAdmin={goAdmin} 
                    questionCounts={questionCounts}
                    isLoading={isLoading}
                    authError={authError}
                />
            )}
            {gameState === 'quiz' && (
                <QuizScreen 
                    questions={activeQuestions} 
                    finishQuiz={finishQuiz} 
                    partName={getPartName(selectedPart)}
                />
            )}
            {gameState === 'result' && (
                <ResultScreen 
                    score={score} 
                    total={activeQuestions.length} 
                    restartQuiz={restartQuiz} 
                    goHome={goHome}
                    partName={getPartName(selectedPart)}
                />
            )}
            {gameState === 'admin' && (
                <AdminScreen 
                    goBack={goHome} 
                    onAddQuestions={addQuestionsToDB} 
                    currentCount={questions.length}
                    onSeedData={handleSeedData}
                    isSaving={isSaving}
                />
            )}
        </div>
    );
}

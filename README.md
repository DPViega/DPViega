import React, { useState, useEffect } from 'react';
import { Github, Linkedin, Mail, Code, Database, Shield, Brain, BarChart3, Zap, Target, Heart, Smile, Trophy, TrendingUp } from 'lucide-react';

export default function ViegaDashboard() {
  const [activeTab, setActiveTab] = useState('overview');
  const [animatedStats, setAnimatedStats] = useState({ projects: 0, commits: 0, stars: 0, rank: 0 });

  useEffect(() => {
    const intervals = [
      { key: 'projects', target: 24, duration: 2000 },
      { key: 'commits', target: 847, duration: 2500 },
      { key: 'stars', target: 156, duration: 2200 },
      { key: 'rank', target: 200, duration: 3000 }
    ];

    intervals.forEach(({ key, target, duration }) => {
      const steps = 60;
      const increment = target / steps;
      const stepDuration = duration / steps;
      
      let current = 0;
      const interval = setInterval(() => {
        current += increment;
        if (current >= target) {
          current = target;
          clearInterval(interval);
        }
        setAnimatedStats(prev => ({ ...prev, [key]: Math.floor(current) }));
      }, stepDuration);
    });
  }, []);

  const skills = {
    frontend: [
      { name: 'React', level: 85, icon: '⚛️' },
      { name: 'JavaScript', level: 88, icon: '🟨' },
      { name: 'HTML/CSS', level: 90, icon: '🎨' }
    ],
    backend: [
      { name: 'Python', level: 92, icon: '🐍' },
      { name: 'SQL', level: 87, icon: '🗄️' },
      { name: 'Node.js', level: 78, icon: '🟩' }
    ],
    data: [
      { name: 'Power BI', level: 85, icon: '📊' },
      { name: 'Machine Learning', level: 80, icon: '🤖' },
      { name: 'Data Analysis', level: 88, icon: '📈' }
    ],
    other: [
      { name: 'Cybersecurity', level: 82, icon: '🔐' },
      { name: 'Prompt Engineering', level: 90, icon: '🧠' },
      { name: 'Git/GitHub', level: 86, icon: '📦' }
    ]
  };

  const softSkills = [
    { name: 'Carisma', value: 95, color: 'bg-pink-500' },
    { name: 'Simpatia', value: 92, color: 'bg-yellow-500' },
    { name: 'Disciplina', value: 98, color: 'bg-blue-500' },
    { name: 'Resiliência', value: 96, color: 'bg-green-500' }
  ];

  const achievements = [
    { title: '🏆 Top 200 de 18.000', desc: 'Geração Caldeira', highlight: true },
    { title: '🎓 IA & Dados', desc: 'Cursando com excelência', highlight: false },
    { title: '💻 Full Stack Dev', desc: 'Multi-tecnologia', highlight: false },
    { title: '🔒 Security First', desc: 'Cybersecurity focus', highlight: false }
  ];

  const StatCard = ({ icon: Icon, label, value, trend }) => (
    <div className="bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl p-6 border border-cyan-500/20 hover:border-cyan-500/50 transition-all duration-300 hover:scale-105">
      <div className="flex items-center justify-between mb-4">
        <Icon className="text-cyan-400" size={32} />
        {trend && <TrendingUp className="text-green-400" size={20} />}
      </div>
      <div className="text-3xl font-bold text-white mb-1">{value}</div>
      <div className="text-gray-400 text-sm">{label}</div>
    </div>
  );

  const SkillBar = ({ name, level, icon }) => (
    <div className="mb-4">
      <div className="flex justify-between mb-2">
        <span className="text-gray-300 font-medium">{icon} {name}</span>
        <span className="text-cyan-400 font-bold">{level}%</span>
      </div>
      <div className="w-full bg-gray-700 rounded-full h-3 overflow-hidden">
        <div 
          className="bg-gradient-to-r from-cyan-500 to-blue-500 h-full rounded-full transition-all duration-1000 ease-out"
          style={{ width: `${level}%` }}
        />
      </div>
    </div>
  );

  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900 text-white p-8">
      {/* Header */}
      <div className="max-w-7xl mx-auto mb-8">
        <div className="bg-gradient-to-r from-cyan-500/10 to-blue-500/10 rounded-2xl p-8 border border-cyan-500/30 backdrop-blur-sm">
          <div className="flex items-center gap-6">
            <div className="w-24 h-24 bg-gradient-to-br from-cyan-500 to-blue-600 rounded-full flex items-center justify-center text-4xl font-bold shadow-lg shadow-cyan-500/50">
              VG
            </div>
            <div className="flex-1">
              <h1 className="text-4xl font-bold mb-2 bg-gradient-to-r from-cyan-400 to-blue-400 bg-clip-text text-transparent">
                Filipe Gabriel Veiga de Paula
              </h1>
              <p className="text-xl text-gray-300 mb-3">@Viega • Desenvolvedor Full Stack & IA Enthusiast</p>
              <div className="flex gap-3">
                <button className="bg-cyan-500 hover:bg-cyan-600 text-black px-4 py-2 rounded-lg font-semibold transition-all flex items-center gap-2">
                  <Github size={18} /> GitHub
                </button>
                <button className="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg font-semibold transition-all flex items-center gap-2">
                  <Linkedin size={18} /> LinkedIn
                </button>
                <button className="bg-gray-700 hover:bg-gray-600 text-white px-4 py-2 rounded-lg font-semibold transition-all flex items-center gap-2">
                  <Mail size={18} /> Contact
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>

      {/* Stats Cards */}
      <div className="max-w-7xl mx-auto mb-8 grid grid-cols-1 md:grid-cols-4 gap-6">
        <StatCard icon={Code} label="Projetos Ativos" value={animatedStats.projects} trend />
        <StatCard icon={Zap} label="Commits Este Ano" value={animatedStats.commits} trend />
        <StatCard icon={Trophy} label="Stars Recebidas" value={animatedStats.stars} />
        <StatCard icon={Target} label="Top de 18.000" value={animatedStats.rank} />
      </div>

      {/* Tabs */}
      <div className="max-w-7xl mx-auto mb-6">
        <div className="flex gap-2 bg-gray-800/50 p-2 rounded-xl border border-gray-700">
          {['overview', 'skills', 'achievements'].map((tab) => (
            <button
              key={tab}
              onClick={() => setActiveTab(tab)}
              className={`flex-1 py-3 px-6 rounded-lg font-semibold transition-all ${
                activeTab === tab
                  ? 'bg-cyan-500 text-black'
                  : 'text-gray-400 hover:text-white hover:bg-gray-700'
              }`}
            >
              {tab.charAt(0).toUpperCase() + tab.slice(1)}
            </button>
          ))}
        </div>
      </div>

      {/* Content */}
      <div className="max-w-7xl mx-auto">
        {activeTab === 'overview' && (
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <div className="bg-gray-800/50 rounded-xl p-6 border border-gray-700">
              <h3 className="text-2xl font-bold mb-4 flex items-center gap-2">
                <Brain className="text-cyan-400" />
                Sobre Mim
              </h3>
              <p className="text-gray-300 leading-relaxed mb-4">
                Nascido em 2006, sou um dos <span className="text-cyan-400 font-bold">200 selecionados entre 18.000 candidatos</span> no programa Geração Caldeira, onde estudo Inteligência Artificial e Dados.
              </p>
              <p className="text-gray-300 leading-relaxed mb-4">
                Apaixonado por tecnologia, cybersecurity e desenvolvimento full stack. Minha missão é criar soluções inovadoras que façam diferença.
              </p>
              <div className="bg-gray-900/50 p-4 rounded-lg border border-cyan-500/30">
                <code className="text-cyan-400 text-sm">
                  <span className="text-purple-400">const</span> viega = &#123;<br/>
                  &nbsp;&nbsp;role: <span className="text-green-400">"Full Stack Developer"</span>,<br/>
                  &nbsp;&nbsp;focus: <span className="text-green-400">"IA & Data Science"</span>,<br/>
                  &nbsp;&nbsp;status: <span className="text-green-400">"Ready to innovate 🚀"</span><br/>
                  &#125;;
                </code>
              </div>
            </div>

            <div className="bg-gray-800/50 rounded-xl p-6 border border-gray-700">
              <h3 className="text-2xl font-bold mb-4 flex items-center gap-2">
                <Heart className="text-pink-400" />
                Soft Skills
              </h3>
              <div className="space-y-4">
                {softSkills.map((skill, idx) => (
                  <div key={idx}>
                    <div className="flex justify-between mb-2">
                      <span className="text-gray-300 font-medium">{skill.name}</span>
                      <span className="text-white font-bold">{skill.value}%</span>
                    </div>
                    <div className="w-full bg-gray-700 rounded-full h-4 overflow-hidden">
                      <div 
                        className={`${skill.color} h-full rounded-full transition-all duration-1000`}
                        style={{ width: `${skill.value}%` }}
                      />
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        )}

        {activeTab === 'skills' && (
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div className="bg-gray-800/50 rounded-xl p-6 border border-gray-700">
              <h3 className="text-xl font-bold mb-4 text-cyan-400">🎨 Frontend Development</h3>
              {skills.frontend.map((skill, idx) => (
                <SkillBar key={idx} {...skill} />
              ))}
            </div>
            <div className="bg-gray-800/50 rounded-xl p-6 border border-gray-700">
              <h3 className="text-xl font-bold mb-4 text-green-400">⚙️ Backend Development</h3>
              {skills.backend.map((skill, idx) => (
                <SkillBar key={idx} {...skill} />
              ))}
            </div>
            <div className="bg-gray-800/50 rounded-xl p-6 border border-gray-700">
              <h3 className="text-xl font-bold mb-4 text-purple-400">📊 Data & Analytics</h3>
              {skills.data.map((skill, idx) => (
                <SkillBar key={idx} {...skill} />
              ))}
            </div>
            <div className="bg-gray-800/50 rounded-xl p-6 border border-gray-700">
              <h3 className="text-xl font-bold mb-4 text-red-400">🔒 Security & Tools</h3>
              {skills.other.map((skill, idx) => (
                <SkillBar key={idx} {...skill} />
              ))}
            </div>
          </div>
        )}

        {activeTab === 'achievements' && (
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            {achievements.map((achievement, idx) => (
              <div
                key={idx}
                className={`rounded-xl p-6 border transition-all duration-300 hover:scale-105 ${
                  achievement.highlight
                    ? 'bg-gradient-to-br from-cyan-500/20 to-blue-500/20 border-cyan-500'
                    : 'bg-gray-800/50 border-gray-700'
                }`}
              >
                <h3 className="text-2xl font-bold mb-2">{achievement.title}</h3>
                <p className="text-gray-400">{achievement.desc}</p>
              </div>
            ))}
          </div>
        )}
      </div>

      {/* Footer */}
      <div className="max-w-7xl mx-auto mt-12 text-center text-gray-500">
        <p>Feito com ❤️ e muito ☕ por Viega • 2025</p>
      </div>
    </div>
  );
}

import React, { useEffect, useState } from "react";
import { motion } from "framer-motion";
import { Sun, Moon, GitHub, Mail } from "lucide-react";
export default function InteractiveProfile() {
  const [profile, setProfile] = useState(null);
  const [repos, setRepos] = useState([]);
  const [dark, setDark] = useState(false);
  useEffect(() => {
    const user = "YOUR_GITHUB_USERNAME";
    fetch(`https://api.github.com/users/${user}`)
      .then((r) => r.json())
      .then((data) => setProfile(data));
    fetch(`https://api.github.com/users/${user}/repos?per_page=100&sort=updated`)
      .then((r) => r.json())
      .then((list) => setRepos(list.slice(0, 8)));
  }, []);
  const custom = {
    role: "CSE Student — Data Science Major",
    university: "Lovely Professional University",
    skills: [
      "Python",
      "NumPy",
      "Pandas",
      "Matplotlib",
      "Seaborn",
      "SciPy",
      "Regression Algorithms",
      "Advanced Excel",
      "Power BI",
      "Machine Learning (AI/ML)"
    ],
    highlights: [
      "Built Excel dashboard (advanced Excel)",
      "Power BI visualizations and reports",
      "Summer internship in AI/ML with Python — CSE Pathshala",
      "Completed projects using scikit-learn and pandas",
      "Experience building data pipelines and exploratory analysis"
    ],
    projects: [
      { name: "Excel Dashboard — Social Media Analytics", link: "#" },
      { name: "ML Model: Regression for Sales Forecasting", link: "#" },
      { name: "Power BI: Interactive Student Dashboard", link: "#" }
    ]
  };
  return (
    <div className={"min-h-screen p-6 md:p-12 transition-colors " + (dark ? "bg-slate-900 text-slate-100" : "bg-white text-slate-900") }>
      <div className="max-w-4xl mx-auto">
        <header className="flex items-center justify-between mb-6">
          <motion.div initial={{ x: -50, opacity: 0 }} animate={{ x: 0, opacity: 1 }} transition={{ duration: 0.6 }} className="flex items-center gap-4">
            <motion.img layoutId="avatar" src={profile?.avatar_url} alt="avatar" className="w-24 h-24 rounded-full ring-4 ring-indigo-400/30" />
            <div>
              <motion.h1 initial={{ y: 8, opacity: 0 }} animate={{ y: 0, opacity: 1 }} transition={{ delay: 0.15 }} className="text-2xl md:text-3xl font-bold">
                {profile?.name || "Dharmendra Singh"}
              </motion.h1>
              <motion.p initial={{ y: 8, opacity: 0 }} animate={{ y: 0, opacity: 1 }} transition={{ delay: 0.25 }} className="text-sm opacity-80">
                {custom.role} — {custom.university}
              </motion.p>
              <motion.p initial={{ y: 8, opacity: 0 }} animate={{ y: 0, opacity: 1 }} transition={{ delay: 0.35 }} className="text-sm opacity-70 mt-2 max-w-xl">
                Passionate about turning data into insights. Focused on Python + ML toolchain (NumPy, Pandas, Matplotlib, Seaborn, SciPy), building dashboards (Advanced Excel, Power BI) and applied ML through internships and projects.
              </motion.p>
            </div>
          </motion.div>
          <div className="flex items-center gap-3">
            <button onClick={() => setDark(!dark)} className="p-2 rounded-lg border">
              {dark ? <Sun size={18} /> : <Moon size={18} />}
            </button>
            <a href={profile?.html_url} target="_blank" rel="noreferrer" className="p-2 rounded-lg border flex items-center gap-2">
              <GitHub size={16} /> View
            </a>
          </div>
        </header>
        <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.2 }} className="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
          <div className="col-span-2 p-6 rounded-2xl shadow-md">
            <h3 className="font-semibold mb-3">Pinned / Recent Repositories</h3>
            <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
              {repos.map((r) => (
                <motion.a key={r.id} whileHover={{ y: -6 }} className="p-4 rounded-lg border hover:shadow-lg transition-shadow" href={r.html_url} target="_blank" rel="noreferrer">
                  <div className="flex items-start justify-between gap-2">
                    <div>
                      <h4 className="font-medium">{r.name}</h4>
                      <p className="text-xs opacity-70 truncate max-w-sm">{r.description || custom.projects.find(p => p.name.toLowerCase().includes(r.name.toLowerCase()))?.name}</p>
                    </div>
                    <div className="text-xs opacity-60 text-right">
                      <div>{r.language}</div>
                      <div className="text-[11px] mt-1">★ {r.stargazers_count}</div>
                    </div>
                  </div>
                </motion.a>
              ))}
            </div>
          </div>
          <div className="p-6 rounded-2xl shadow-md">
            <h3 className="font-semibold mb-3">Quick Stats</h3>
            <div className="space-y-3">
              <div className="flex items-center justify-between text-sm"><span>Followers</span><span>{profile?.followers ?? "—"}</span></div>
              <div className="flex items-center justify-between text-sm"><span>Following</span><span>{profile?.following ?? "—"}</span></div>
              <div className="flex items-center justify-between text-sm"><span>Public repos</span><span>{profile?.public_repos ?? "—"}</span></div>
              <motion.div initial={{ scaleX: 0 }} animate={{ scaleX: 1 }} transition={{ duration: 0.6 }} className="origin-left bg-gradient-to-r from-indigo-400 to-pink-400 h-2 rounded-full mt-4" />
            </div>
          </div>
        </motion.section>
        <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.35 }} className="p-6 rounded-2xl shadow-md mb-6">
          <h3 className="font-semibold mb-4">Skills & Tools</h3>
          <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
            {custom.skills.map((s) => (
              <motion.div key={s} whileHover={{ scale: 1.03 }} className="flex items-center gap-3 p-3 border rounded-lg">
                <div className="font-medium">{s}</div>
                <div className="text-xs opacity-60 ml-auto">{s === 'Python' ? 'proficient' : 'working knowledge'}</div>
              </motion.div>
            ))}
          </div>
        </motion.section>
        <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.45 }} className="p-6 rounded-2xl shadow-md mb-6">
          <h3 className="font-semibold mb-3">Projects & Highlights</h3>
          <div className="grid grid-cols-1 gap-3">
            {custom.highlights.map((h, i) => (
              <motion.div key={i} initial={{ x: -8, opacity: 0 }} animate={{ x: 0, opacity: 1 }} transition={{ delay: 0.05 * i }} className="p-3 rounded-lg border flex items-start justify-between">
                <div className="text-sm">{h}</div>
                <div className="text-xs opacity-60">{i < custom.projects.length ? custom.projects[i].name : ''}</div>
              </motion.div>
            ))}
          </div>
        </motion.section>
        <motion.footer initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.5 }} className="p-6 rounded-2xl shadow-md flex items-center justify-between gap-4">
          <div>
            <div className="font-medium">Experience</div>
            <div className="text-sm opacity-80">Summer Internship: AI/ML with Python — CSE Pathshala</div>
            <div className="text-sm opacity-70 mt-1">Open for more internships and collaborative projects.</div>
          </div>
          <div className="flex gap-3">
            <a href={`mailto:${profile?.email || "your.email@example.com"}`} className="px-4 py-2 rounded-lg border flex items-center gap-2"><Mail size={16} /> Email</a>
            <a href={profile?.html_url} target="_blank" rel="noreferrer" className="px-4 py-2 rounded-lg border flex items-center gap-2"><GitHub size={16} /> GitHub</a>
          </div>
        </motion.footer>
      </div>
    </div>
  );
}

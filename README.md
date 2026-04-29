import React, { useEffect, useState } from "react";
import { motion } from "framer-motion";

export default function GitHubProfile() {
  const [commits, setCommits] = useState([]);
  const [stats, setStats] = useState(null);

  const username = "oasamaheles";

  useEffect(() => {
    // Mock GitHub stats (replace with GitHub API or GraphQL)
    setStats({
      repos: 42,
      commits: 1284,
      prs: 97,
      issues: 31,
    });

    // Simulated real-time commits feed
    const interval = setInterval(() => {
      setCommits((prev) => [
        {
          id: Date.now(),
          msg: "Updated CI/CD pipeline",
          repo: "sezon-app",
          time: new Date().toLocaleTimeString(),
        },
        ...prev.slice(0, 4),
      ]);
    }, 4000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="min-h-screen bg-black text-white p-6">
      {/* HEADER */}
      <div className="text-center mb-10">
        <h1 className="text-4xl font-bold text-cyan-400">Osama Hillis</h1>
        <p className="text-gray-400">
          Mobile Architect | QA Engineer | DevOps Thinker
        </p>
      </div>

      {/* GLASS STATS */}
      <div className="grid grid-cols-2 md:grid-cols-4 gap-4 mb-10">
        {stats && Object.entries(stats).map(([key, value]) => (
          <motion.div
            key={key}
            whileHover={{ scale: 1.05 }}
            className="backdrop-blur-xl bg-white/10 border border-white/20 p-4 rounded-2xl text-center"
          >
            <h2 className="text-cyan-300 text-xl font-bold">{value}</h2>
            <p className="text-gray-400 capitalize">{key}</p>
          </motion.div>
        ))}
      </div>

      {/* 3D CARDS */}
      <div className="grid md:grid-cols-2 gap-6 mb-10">
        {[
          {
            title: "Emergency Tracking System",
            desc: "Real-time GPS + Firebase + Life-critical reliability",
          },
          {
            title: "SEZON E-Commerce",
            desc: "Scalable Flutter + Clean Architecture",
          },
        ].map((project, i) => (
          <motion.div
            key={i}
            whileHover={{ rotateY: 10, scale: 1.03 }}
            className="bg-gradient-to-br from-cyan-900/40 to-black p-6 rounded-2xl border border-cyan-500/20 shadow-xl"
          >
            <h3 className="text-xl font-bold text-cyan-300">
              {project.title}
            </h3>
            <p className="text-gray-400 mt-2">{project.desc}</p>
          </motion.div>
        ))}
      </div>

      {/* LIVE COMMITS */}
      <div className="backdrop-blur-xl bg-white/5 border border-white/10 p-6 rounded-2xl">
        <h2 className="text-cyan-400 text-xl mb-4">Live Commits Feed</h2>
        {commits.length === 0 && (
          <p className="text-gray-500">Waiting for activity...</p>
        )}
        <ul className="space-y-2">
          {commits.map((c) => (
            <li key={c.id} className="text-sm text-gray-300">
              <span className="text-cyan-400">{c.repo}</span> — {c.msg} ({c.time})
            </li>
          ))}
        </ul>
      </div>

      {/* FOOTER */}
      <div className="text-center mt-10 text-gray-500 text-sm">
        Enterprise React GitHub Profile Dashboard
      </div>
    </div>
  );
}

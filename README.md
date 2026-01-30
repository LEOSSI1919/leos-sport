import Head from 'next/head'

// ===== API REAL INTEGRATION (API-Football & NewsAPI) ===== // Simpan API key di .env.local // NEXT_PUBLIC_FOOTBALL_API_KEY=ISI_API_KEY // NEXT_PUBLIC_NEWS_API_KEY=ISI_API_KEY

import Head from 'next/head' import { useEffect, useState } from 'react'

export default function Home() { const [liveMatches, setLiveMatches] = useState([]) const [news, setNews] = useState([]) const [loadingLive, setLoadingLive] = useState(true) const [loadingNews, setLoadingNews] = useState(true)

// ===== LIVE SCORE REAL ===== useEffect(() => { async function fetchLive() { try { const res = await fetch('https://v3.football.api-sports.io/fixtures?live=all', { headers: { 'x-apisports-key': process.env.NEXT_PUBLIC_FOOTBALL_API_KEY } }) const data = await res.json() setLiveMatches(data.response || []) setLoadingLive(false) } catch (err) { console.error(err) } }

fetchLive()
const interval = setInterval(fetchLive, 30000)
return () => clearInterval(interval)

}, [])

// ===== NEWS REAL ===== useEffect(() => { async function fetchNews() { try { const res = await fetch(https://newsapi.org/v2/everything?q=football&sortBy=publishedAt&language=en&apiKey=${process.env.NEXT_PUBLIC_NEWS_API_KEY}) const data = await res.json() setNews(data.articles.slice(0, 6)) setLoadingNews(false) } catch (err) { console.error(err) } }

fetchNews()

}, []) () { return ( <> <Head> <title>FOOTBALL NEWS – Live Score & Berita Sepakbola</title> <meta name="description" content="Live score, berita sepakbola terbaru 2026, klasemen liga dunia." /> </Head>

<main className="min-h-screen bg-[#0f0f1a] text-white">
    <header className="sticky top-0 z-50 bg-[#6a00ff] px-6 py-4 flex justify-between items-center shadow-lg">
      <h1 className="text-xl font-bold">FOOTBALL NEWS</h1>
      <nav className="space-x-4 text-sm font-semibold">
        <a href="#">Home</a>
        <a href="#">Live</a>
        <a href="#">Berita</a>
        <a href="#">Klasemen</a>
        <a href="#">Jadwal</a>
      </nav>
    </header>

    {/* Breaking News */}
    <section className="bg-red-600 text-center py-2 text-sm font-semibold">
      🔴 BREAKING NEWS: Update Sepakbola Dunia 2026
    </section>

    {/* Live Score */}
    <section className="p-6">
      <h2 className="text-lg font-bold mb-4">Live Score</h2>
      <div className="grid md:grid-cols-3 gap-4">
        <div className="bg-[#1b1b2b] rounded-2xl p-4">
          <p className="text-sm text-gray-400">Premier League • LIVE</p>
          <p className="text-lg font-semibold">Man City 1 - 1 Liverpool</p>
          <p className="text-xs text-gray-400">Menit 67</p>
        </div>
      </div>
    </section>

    {/* News */}
    <section className="p-6">
      <h2 className="text-lg font-bold mb-4">Berita Terbaru</h2>
      <div className="grid md:grid-cols-2 gap-4">
        <article className="bg-[#1b1b2b] rounded-2xl p-4">
          <h3 className="font-semibold">Transfer Besar Mengguncang Eropa</h3>
          <p className="text-sm text-gray-400 mt-2">Bursa transfer 2026 menghadirkan kejutan besar.</p>
        </article>
        <article className="bg-[#1b1b2b] rounded-2xl p-4">
          <h3 className="font-semibold">Liga Top Dunia Memanas</h3>
          <p className="text-sm text-gray-400 mt-2">Persaingan menuju gelar juara semakin ketat.</p>
        </article>
      </div>
    </section>

    {/* Standings */}
    <section className="p-6">
      <h2 className="text-lg font-bold mb-4">Klasemen Premier League</h2>
      <div className="bg-[#1b1b2b] rounded-2xl p-4 text-sm">
        <ol className="space-y-1">
          <li>1. Man City – 78 pts</li>
          <li>2. Arsenal – 75 pts</li>
          <li>3. Liverpool – 72 pts</li>
          <li>4. Tottenham – 68 pts</li>
        </ol>
      </div>
    </section>

    <footer className="text-center text-xs text-gray-400 py-6">
      © 2026 FOOTBALL NEWS. Professional Football Media.
    </footer>
  </main>
</>

) }

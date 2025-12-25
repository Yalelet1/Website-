# Website-
Modern website 
import React, { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { 
  Search, Truck, Wind, Settings, FileText, Download, 
  ArrowRight, Phone, Mail, ShieldCheck, Box, Clock, Menu, Factory
} from "lucide-react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";

// --- DATA MOCKUPS ---
const CATEGORIES = [
  { id: 'heavy', name: 'Heavy Machinery', icon: <Truck />, img: 'https://images.unsplash.com/photo-1579401780637-8051253457a4?auto=format&fit=crop&q=80&w=800' },
  { id: 'air', name: 'Industrial Compressors', icon: <Wind />, img: 'https://images.unsplash.com/photo-1581092160607-ee22621dd758?auto=format&fit=crop&q=80&w=800' },
];

const COMPRESSOR_MODELS = [
  { id: 1, name: "Titan S-15", flow: "1.8 m³/min", pressure: "8 bar", power: "11 kW", noise: "62 dB" },
  { id: 2, name: "Titan S-30", flow: "3.6 m³/min", pressure: "10 bar", power: "22 kW", noise: "65 dB" },
  { id: 3, name: "Industrial X-50", flow: "6.2 m³/min", pressure: "13 bar", power: "37 kW", noise: "68 dB" }
];

const RESOURCES = [
  { title: "S-Series Screw Compressor Manual", type: "PDF", cat: "Manuals" },
  { title: "20-Ton Excavator CAD File", type: "DWG", cat: "Engineering" },
  { title: "ISO 9001:2025 Certification", type: "PDF", cat: "Compliance" },
];

export default function IndustrialCorporateSite() {
  const [activeCat, setActiveCat] = useState(CATEGORIES[0]);
  const [comp1, setComp1] = useState(COMPRESSOR_MODELS[0]);
  const [comp2, setComp2] = useState(COMPRESSOR_MODELS[1]);

  return (
    <div className="min-h-screen bg-white text-slate-900 scroll-smooth">
      {/* 1. HEADER */}
      <header className="sticky top-0 z-50 bg-white/95 backdrop-blur-sm border-b">
        <div className="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
          <div className="flex items-center gap-2 font-black text-2xl tracking-tighter italic">
            <Factory className="text-blue-600" /> <span className="uppercase">Titan</span>SUPPLY
          </div>
          <nav className="hidden lg:flex gap-8 font-semibold text-sm uppercase tracking-widest text-slate-600">
            {['Services', 'Products', 'About', 'News', 'Contact'].map(item => (
              <a key={item} href={`#${item.toLowerCase()}`} className="hover:text-blue-600 transition-colors">{item}</a>
            ))}
          </nav>
          <Button className="bg-blue-600 hover:bg-blue-700">Request Quote</Button>
        </div>
      </header>

      {/* 2. HERO & SEARCH */}
      <section className="relative h-[80vh] flex items-center bg-slate-900 text-white overflow-hidden">
        <div className="absolute inset-0 opacity-40 grayscale">
          <img src="https://images.unsplash.com/photo-1541625602330-2277a4c46182?auto=format&fit=crop&q=80&w=2000" alt="Heavy Industry" className="w-full h-full object-cover" />
        </div>
        <div className="relative max-w-7xl mx-auto px-6 w-full">
          <motion.h1 initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} className="text-5xl md:text-7xl font-extrabold mb-6 leading-tight">
            Industrial Strength. <br/><span className="text-blue-500 font-normal italic">Precision Engineering.</span>
          </motion.h1>
          <div className="bg-white p-2 rounded-xl shadow-2xl flex items-center gap-2 max-w-xl">
            <Search className="ml-3 text-slate-400" />
            <Input placeholder="Search models or part numbers..." className="border-none focus-visible:ring-0 text-slate-900" />
            <Button className="bg-slate-900 px-8">Search</Button>
          </div>
        </div>
      </section>

      {/* 3. DYNAMIC PRODUCT SELECTION */}
      <section id="products" className="py-24 bg-slate-50 border-b">
        <div className="max-w-7xl mx-auto px-6">
          <div className="flex flex-col md:flex-row justify-between items-end mb-12 gap-6">
            <div>
              <h2 className="text-4xl font-bold mb-4">Product Inventory</h2>
              <p className="text-slate-500">Certified machinery for factories and heavy-duty infrastructure.</p>
            </div>
            <div className="flex gap-4 p-1 bg-white border rounded-full shadow-sm">
              {CATEGORIES.map((cat) => (
                <button key={cat.id} onClick={() => setActiveCat(cat)} className={`px-6 py-2 rounded-full font-bold transition-all ${activeCat.id === cat.id ? 'bg-blue-600 text-white' : 'text-slate-500'}`}>
                  {cat.name}
                </button>
              ))}
            </div>
          </div>
          <div className="grid lg:grid-cols-2 gap-12 items-center">
            <AnimatePresence mode="wait">
              <motion.div key={activeCat.id} initial={{ opacity: 0, x: -20 }} animate={{ opacity: 1, x: 0 }} className="rounded-2xl overflow-hidden h-[400px] shadow-xl border">
                <img src={activeCat.img} className="w-full h-full object-cover" alt={activeCat.name} />
              </motion.div>
            </AnimatePresence>
            <div className="space-y-6">
              <h3 className="text-3xl font-bold">{activeCat.name} Solutions</h3>
              <p className="text-lg text-slate-600">Our {activeCat.name.toLowerCase()} are designed for 24/7 continuous operation. We provide on-site technical audits to match the right machine to your facility requirements.</p>
              <Button size="lg" className="gap-2">Technical Catalog <ArrowRight className="w-4 h-4" /></Button>
            </div>
          </div>
        </div>
      </section>

      {/* 4. TECHNICAL COMPARATOR */}
      <section className="py-24 bg-white">
        <div className="max-w-4xl mx-auto px-6 border p-12 rounded-3xl bg-white shadow-sm">
          <h3 className="text-2xl font-bold mb-8 text-center italic uppercase tracking-widest text-blue-600">Technical Comparator</h3>
          <div className="grid grid-cols-3 gap-6 mb-10">
            <div className="text-sm font-bold self-center uppercase text-slate-400">Select Models</div>
            <select onChange={(e) => setComp1(COMPRESSOR_MODELS[e.target.selectedIndex])} className="p-3 border rounded-lg font-bold">
              {COMPRESSOR_MODELS.map(m => <option key={m.id}>{m.name}</option>)}
            </select>
            <select onChange={(e) => setComp2(COMPRESSOR_MODELS[e.target.selectedIndex])} className="p-3 border rounded-lg font-bold">
              {COMPRESSOR_MODELS.map(m => <option key={m.id}>{m.name}</option>)}
            </select>
          </div>
          <div className="space-y-2">
            {[ {l: 'Air Flow', k: 'flow'}, {l: 'Max Pressure', k: 'pressure'}, {l: 'Motor Power', k: 'power'}, {l: 'Noise Level', k: 'noise'} ].map(spec => (
              <div key={spec.l} className="grid grid-cols-3 py-4 border-b hover:bg-slate-50 px-2 transition-colors">
                <div className="text-slate-500 font-semibold">{spec.l}</div>
                <div className="text-center font-bold text-slate-900">{comp1[spec.k]}</div>
                <div className="text-center font-bold text-blue-600">{comp2[spec.k]}</div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* 5. RESOURCE CENTER */}
      <section className="py-24 bg-slate-900 text-white">
        <div className="max-w-7xl mx-auto px-6">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold mb-4">Engineering Resource Center</h2>
            <p className="text-slate-400">Download blueprints, safety manuals, and compliance documentation.</p>
          </div>
          <div className="grid md:grid-cols-3 gap-8">
            {RESOURCES.map((file, i) => (
              <div key={i} className="bg-slate-800 p-8 rounded-2xl border border-slate-700 group hover:border-blue-500 transition-all">
                <FileText className="text-blue-400 mb-6 w-10 h-10" />
                <h4 className="font-bold text-xl mb-6">{file.title}</h4>
                <Button variant="outline" className="w-full border-slate-600 text-white hover:bg-blue-600 hover:border-blue-600 gap-2">
                  Download {file.type} <Download className="w-4 h-4" />
                </Button>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* 6. NEWS / BLOG */}
      <section id="news" className="py-24">
        <div className="max-w-7xl mx-auto px-6">
          <h2 className="text-3xl font-extrabold mb-12">Industrial News & Efficiency Tips</h2>
          <div className="grid lg:grid-cols-2 gap-12">
            <div className="group cursor-pointer">
              <div className="bg-slate-100 rounded-3xl h-64 mb-6 overflow-hidden">
                <img src="https://images.unsplash.com/photo-1581092160607-ee22621dd758?auto=format&fit=crop&q=80&w=800" className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700" alt="News" />
              </div>
              <span className="text-blue-600 font-bold uppercase text-xs tracking-widest">Efficiency Guide • 2025</span>
              <h3 className="text-2xl font-bold mt-2 hover:text-blue-600 transition-colors">Maximizing CFM: A Factory Manager's Guide to Compressed Air Audits</h3>
            </div>
            <div className="space-y-8">
              {[1, 2].map(i => (
                <div key={i} className="flex gap-6 border-b pb-8 hover:bg-slate-50 p-2 transition-all rounded-lg">
                  <div className="w-24 h-24 bg-slate-100 rounded-xl shrink-0" />
                  <div>
                    <h4 className="font-bold text-lg leading-tight mb-2">Winter Maintenance: Protecting Hydraulic Systems from Cold Weather Wear</h4>
                    <p className="text-sm text-slate-500 line-clamp-2">Learn the specific viscosity adjustments needed for heavy machinery operating in sub-zero environments...</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* 7. CONTACT & FOOTER */}
      <section id="contact" className="py-24 bg-slate-50 border-t">
        <div className="max-w-7xl mx-auto px-6 grid lg:grid-cols-2 gap-16">
          <div>
            <h2 className="text-4xl font-black italic uppercase mb-8 leading-none">Let's build <br/><span className="text-blue-600">Infrastructure.</span></h2>
            <div className="space-y-6">
              <div className="flex gap-4 items-center font-bold text-xl"><Phone className="text-blue-600" /> +1 (800) TITAN-PRO</div>
              <div className="flex gap-4 items-center font-bold text-xl"><Mail className="text-blue-600" /> support@titan-supply.com</div>
            </div>
          </div>
          <div className="bg-white p-10 rounded-3xl shadow-xl space-y-4">
            <Input placeholder="Full Name" className="h-14" />
            <Input placeholder="Company Name" className="h-14" />
            <Input type="email" placeholder="Work Email" className="h-14" />
            <textarea placeholder="Describe your project requirements..." className="w-full h-32 border p-4 rounded-xl focus:outline-blue-600" />
            <Button className="w-full h-14 text-lg bg-blue-600 font-bold">Request Technical Quote</Button>
          </div>
        </div>
      </section>

      <footer className="py-10 text-center bg-white border-t text-slate-400 text-xs font-bold uppercase tracking-widest">
        © 2025 Titan Industrial Supply Co. | ISO 9001 Certified | Built for Industrial Excellence
      </footer>
    </div>
  );
}import React, { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { 
  Search, Truck, Wind, Settings, FileText, Download, 
  ArrowRight, Phone, Mail, ShieldCheck, Box, Clock, Menu, Factory
} from "lucide-react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";

// --- DATA MOCKUPS ---
const CATEGORIES = [
  { id: 'heavy', name: 'Heavy Machinery', icon: <Truck />, img: 'https://images.unsplash.com/photo-1579401780637-8051253457a4?auto=format&fit=crop&q=80&w=800' },
  { id: 'air', name: 'Industrial Compressors', icon: <Wind />, img: 'https://images.unsplash.com/photo-1581092160607-ee22621dd758?auto=format&fit=crop&q=80&w=800' },
];

const COMPRESSOR_MODELS = [
  { id: 1, name: "Titan S-15", flow: "1.8 m³/min", pressure: "8 bar", power: "11 kW", noise: "62 dB" },
  { id: 2, name: "Titan S-30", flow: "3.6 m³/min", pressure: "10 bar", power: "22 kW", noise: "65 dB" },
  { id: 3, name: "Industrial X-50", flow: "6.2 m³/min", pressure: "13 bar", power: "37 kW", noise: "68 dB" }
];

const RESOURCES = [
  { title: "S-Series Screw Compressor Manual", type: "PDF", cat: "Manuals" },
  { title: "20-Ton Excavator CAD File", type: "DWG", cat: "Engineering" },
  { title: "ISO 9001:2025 Certification", type: "PDF", cat: "Compliance" },
];

export default function IndustrialCorporateSite() {
  const [activeCat, setActiveCat] = useState(CATEGORIES[0]);
  const [comp1, setComp1] = useState(COMPRESSOR_MODELS[0]);
  const [comp2, setComp2] = useState(COMPRESSOR_MODELS[1]);

  return (
    <div className="min-h-screen bg-white text-slate-900 scroll-smooth">
      {/* 1. HEADER */}
      <header className="sticky top-0 z-50 bg-white/95 backdrop-blur-sm border-b">
        <div className="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
          <div className="flex items-center gap-2 font-black text-2xl tracking-tighter italic">
            <Factory className="text-blue-600" /> <span className="uppercase">Titan</span>SUPPLY
          </div>
          <nav className="hidden lg:flex gap-8 font-semibold text-sm uppercase tracking-widest text-slate-600">
            {['Services', 'Products', 'About', 'News', 'Contact'].map(item => (
              <a key={item} href={`#${item.toLowerCase()}`} className="hover:text-blue-600 transition-colors">{item}</a>
            ))}
          </nav>
          <Button className="bg-blue-600 hover:bg-blue-700">Request Quote</Button>
        </div>
      </header>

      {/* 2. HERO & SEARCH */}
      <section className="relative h-[80vh] flex items-center bg-slate-900 text-white overflow-hidden">
        <div className="absolute inset-0 opacity-40 grayscale">
          <img src="https://images.unsplash.com/photo-1541625602330-2277a4c46182?auto=format&fit=crop&q=80&w=2000" alt="Heavy Industry" className="w-full h-full object-cover" />
        </div>
        <div className="relative max-w-7xl mx-auto px-6 w-full">
          <motion.h1 initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} className="text-5xl md:text-7xl font-extrabold mb-6 leading-tight">
            Industrial Strength. <br/><span className="text-blue-500 font-normal italic">Precision Engineering.</span>
          </motion.h1>
          <div className="bg-white p-2 rounded-xl shadow-2xl flex items-center gap-2 max-w-xl">
            <Search className="ml-3 text-slate-400" />
            <Input placeholder="Search models or part numbers..." className="border-none focus-visible:ring-0 text-slate-900" />
            <Button className="bg-slate-900 px-8">Search</Button>
          </div>
        </div>
      </section>

      {/* 3. DYNAMIC PRODUCT SELECTION */}
      <section id="products" className="py-24 bg-slate-50 border-b">
        <div className="max-w-7xl mx-auto px-6">
          <div className="flex flex-col md:flex-row justify-between items-end mb-12 gap-6">
            <div>
              <h2 className="text-4xl font-bold mb-4">Product Inventory</h2>
              <p className="text-slate-500">Certified machinery for factories and heavy-duty infrastructure.</p>
            </div>
            <div className="flex gap-4 p-1 bg-white border rounded-full shadow-sm">
              {CATEGORIES.map((cat) => (
                <button key={cat.id} onClick={() => setActiveCat(cat)} className={`px-6 py-2 rounded-full font-bold transition-all ${activeCat.id === cat.id ? 'bg-blue-600 text-white' : 'text-slate-500'}`}>
                  {cat.name}
                </button>
              ))}
            </div>
          </div>
          <div className="grid lg:grid-cols-2 gap-12 items-center">
            <AnimatePresence mode="wait">
              <motion.div key={activeCat.id} initial={{ opacity: 0, x: -20 }} animate={{ opacity: 1, x: 0 }} className="rounded-2xl overflow-hidden h-[400px] shadow-xl border">
                <img src={activeCat.img} className="w-full h-full object-cover" alt={activeCat.name} />
              </motion.div>
            </AnimatePresence>
            <div className="space-y-6">
              <h3 className="text-3xl font-bold">{activeCat.name} Solutions</h3>
              <p className="text-lg text-slate-600">Our {activeCat.name.toLowerCase()} are designed for 24/7 continuous operation. We provide on-site technical audits to match the right machine to your facility requirements.</p>
              <Button size="lg" className="gap-2">Technical Catalog <ArrowRight className="w-4 h-4" /></Button>
            </div>
          </div>
        </div>
      </section>

      {/* 4. TECHNICAL COMPARATOR */}
      <section className="py-24 bg-white">
        <div className="max-w-4xl mx-auto px-6 border p-12 rounded-3xl bg-white shadow-sm">
          <h3 className="text-2xl font-bold mb-8 text-center italic uppercase tracking-widest text-blue-600">Technical Comparator</h3>
          <div className="grid grid-cols-3 gap-6 mb-10">
            <div className="text-sm font-bold self-center uppercase text-slate-400">Select Models</div>
            <select onChange={(e) => setComp1(COMPRESSOR_MODELS[e.target.selectedIndex])} className="p-3 border rounded-lg font-bold">
              {COMPRESSOR_MODELS.map(m => <option key={m.id}>{m.name}</option>)}
            </select>
            <select onChange={(e) => setComp2(COMPRESSOR_MODELS[e.target.selectedIndex])} className="p-3 border rounded-lg font-bold">
              {COMPRESSOR_MODELS.map(m => <option key={m.id}>{m.name}</option>)}
            </select>
          </div>
          <div className="space-y-2">
            {[ {l: 'Air Flow', k: 'flow'}, {l: 'Max Pressure', k: 'pressure'}, {l: 'Motor Power', k: 'power'}, {l: 'Noise Level', k: 'noise'} ].map(spec => (
              <div key={spec.l} className="grid grid-cols-3 py-4 border-b hover:bg-slate-50 px-2 transition-colors">
                <div className="text-slate-500 font-semibold">{spec.l}</div>
                <div className="text-center font-bold text-slate-900">{comp1[spec.k]}</div>
                <div className="text-center font-bold text-blue-600">{comp2[spec.k]}</div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* 5. RESOURCE CENTER */}
      <section className="py-24 bg-slate-900 text-white">
        <div className="max-w-7xl mx-auto px-6">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold mb-4">Engineering Resource Center</h2>
            <p className="text-slate-400">Download blueprints, safety manuals, and compliance documentation.</p>
          </div>
          <div className="grid md:grid-cols-3 gap-8">
            {RESOURCES.map((file, i) => (
              <div key={i} className="bg-slate-800 p-8 rounded-2xl border border-slate-700 group hover:border-blue-500 transition-all">
                <FileText className="text-blue-400 mb-6 w-10 h-10" />
                <h4 className="font-bold text-xl mb-6">{file.title}</h4>
                <Button variant="outline" className="w-full border-slate-600 text-white hover:bg-blue-600 hover:border-blue-600 gap-2">
                  Download {file.type} <Download className="w-4 h-4" />
                </Button>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* 6. NEWS / BLOG */}
      <section id="news" className="py-24">
        <div className="max-w-7xl mx-auto px-6">
          <h2 className="text-3xl font-extrabold mb-12">Industrial News & Efficiency Tips</h2>
          <div className="grid lg:grid-cols-2 gap-12">
            <div className="group cursor-pointer">
              <div className="bg-slate-100 rounded-3xl h-64 mb-6 overflow-hidden">
                <img src="https://images.unsplash.com/photo-1581092160607-ee22621dd758?auto=format&fit=crop&q=80&w=800" className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700" alt="News" />
              </div>
              <span className="text-blue-600 font-bold uppercase text-xs tracking-widest">Efficiency Guide • 2025</span>
              <h3 className="text-2xl font-bold mt-2 hover:text-blue-600 transition-colors">Maximizing CFM: A Factory Manager's Guide to Compressed Air Audits</h3>
            </div>
            <div className="space-y-8">
              {[1, 2].map(i => (
                <div key={i} className="flex gap-6 border-b pb-8 hover:bg-slate-50 p-2 transition-all rounded-lg">
                  <div className="w-24 h-24 bg-slate-100 rounded-xl shrink-0" />
                  <div>
                    <h4 className="font-bold text-lg leading-tight mb-2">Winter Maintenance: Protecting Hydraulic Systems from Cold Weather Wear</h4>
                    <p className="text-sm text-slate-500 line-clamp-2">Learn the specific viscosity adjustments needed for heavy machinery operating in sub-zero environments...</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* 7. CONTACT & FOOTER */}
      <section id="contact" className="py-24 bg-slate-50 border-t">
        <div className="max-w-7xl mx-auto px-6 grid lg:grid-cols-2 gap-16">
          <div>
            <h2 className="text-4xl font-black italic uppercase mb-8 leading-none">Let's build <br/><span className="text-blue-600">Infrastructure.</span></h2>
            <div className="space-y-6">
              <div className="flex gap-4 items-center font-bold text-xl"><Phone className="text-blue-600" /> +1 (800) TITAN-PRO</div>
              <div className="flex gap-4 items-center font-bold text-xl"><Mail className="text-blue-600" /> support@titan-supply.com</div>
            </div>
          </div>
          <div className="bg-white p-10 rounded-3xl shadow-xl space-y-4">
            <Input placeholder="Full Name" className="h-14" />
            <Input placeholder="Company Name" className="h-14" />
            <Input type="email" placeholder="Work Email" className="h-14" />
            <textarea placeholder="Describe your project requirements..." className="w-full h-32 border p-4 rounded-xl focus:outline-blue-600" />
            <Button className="w-full h-14 text-lg bg-blue-600 font-bold">Request Technical Quote</Button>
          </div>
        </div>
      </section>

      <footer className="py-10 text-center bg-white border-t text-slate-400 text-xs font-bold uppercase tracking-widest">
        © 2025 Titan Industrial Supply Co. | ISO 9001 Certified | Built for Industrial Excellence
      </footer>
    </div>
  );
}

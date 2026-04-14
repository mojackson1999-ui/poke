const typeColors = {
  fire:"#D85A30",water:"#378ADD",grass:"#639922",electric:"#BA7517",
  psychic:"#D4537E",ice:"#1D9E75",dragon:"#534AB7",dark:"#444441",
  normal:"#888780",fighting:"#993C1D",poison:"#72243E",ground:"#854F0B",
  flying:"#185FA5",bug:"#3B6D11",rock:"#5F5E5A",ghost:"#3C3489",
  steel:"#0F6E56",fairy:"#993556"
};

const ALL_POKEMON = [
  {id:1,name:"Bulbasaur",emoji:"🌱",types:["grass","poison"],hp:45,atk:49,def:49,spa:65,spd:65,spe:45,height:"0.7m",weight:"6.9kg",gen:"Gen I",cat:"Starter"},
  {id:4,name:"Charmander",emoji:"🔥",types:["fire"],hp:39,atk:52,def:43,spa:60,spd:50,spe:65,height:"0.6m",weight:"8.5kg",gen:"Gen I",cat:"Starter"},
  {id:7,name:"Squirtle",emoji:"🐢",types:["water"],hp:44,atk:48,def:65,spa:50,spd:64,spe:43,height:"0.5m",weight:"9.0kg",gen:"Gen I",cat:"Starter"},
  {id:25,name:"Pikachu",emoji:"⚡",types:["electric"],hp:35,atk:55,def:40,spa:50,spd:50,spe:90,height:"0.4m",weight:"6.0kg",gen:"Gen I",cat:"Iconic"},
  {id:39,name:"Jigglypuff",emoji:"🎵",types:["normal","fairy"],hp:115,atk:45,def:20,spa:45,spd:25,spe:20,height:"0.5m",weight:"5.5kg",gen:"Gen I",cat:"Normal"},
  {id:94,name:"Gengar",emoji:"👻",types:["ghost","poison"],hp:60,atk:65,def:60,spa:130,spd:75,spe:110,height:"1.5m",weight:"40.5kg",gen:"Gen I",cat:"Ghost"},
  {id:131,name:"Lapras",emoji:"🦕",types:["water","ice"],hp:130,atk:85,def:80,spa:85,spd:95,spe:60,height:"2.5m",weight:"220kg",gen:"Gen I",cat:"Rare"},
  {id:143,name:"Snorlax",emoji:"😴",types:["normal"],hp:160,atk:110,def:65,spa:65,spd:110,spe:30,height:"2.1m",weight:"460kg",gen:"Gen I",cat:"Normal"},
  {id:149,name:"Dragonite",emoji:"🐉",types:["dragon","flying"],hp:91,atk:134,def:95,spa:100,spd:100,spe:80,height:"2.2m",weight:"210kg",gen:"Gen I",cat:"Dragon"},
  {id:150,name:"Mewtwo",emoji:"🔮",types:["psychic"],hp:106,atk:110,def:90,spa:154,spd:90,spe:130,height:"2.0m",weight:"122kg",gen:"Gen I",cat:"Legendary"},
  {id:152,name:"Chikorita",emoji:"🍃",types:["grass"],hp:45,atk:49,def:65,spa:49,spd:65,spe:45,height:"0.9m",weight:"6.4kg",gen:"Gen II",cat:"Starter"},
  {id:175,name:"Togepi",emoji:"🥚",types:["fairy"],hp:35,atk:20,def:65,spa:40,spd:65,spe:20,height:"0.3m",weight:"1.5kg",gen:"Gen II",cat:"Cute"},
  {id:196,name:"Espeon",emoji:"☀️",types:["psychic"],hp:65,atk:65,def:60,spa:130,spd:95,spe:110,height:"0.9m",weight:"26.5kg",gen:"Gen II",cat:"Eeveelution"},
  {id:197,name:"Umbreon",emoji:"🌙",types:["dark"],hp:95,atk:65,def:110,spa:60,spd:130,spe:65,height:"1.0m",weight:"27.0kg",gen:"Gen II",cat:"Eeveelution"},
  {id:249,name:"Lugia",emoji:"🕊️",types:["psychic","flying"],hp:106,atk:90,def:130,spa:90,spd:154,spe:110,height:"5.2m",weight:"216kg",gen:"Gen II",cat:"Legendary"},
  {id:282,name:"Gardevoir",emoji:"💫",types:["psychic","fairy"],hp:68,atk:65,def:65,spa:125,spd:115,spe:80,height:"1.6m",weight:"48.4kg",gen:"Gen III",cat:"Humanoid"},
  {id:350,name:"Milotic",emoji:"🐟",types:["water"],hp:95,atk:60,def:79,spa:100,spd:125,spe:81,height:"6.2m",weight:"162kg",gen:"Gen III",cat:"Rare"},
  {id:384,name:"Rayquaza",emoji:"🌪️",types:["dragon","flying"],hp:105,atk:150,def:90,spa:150,spd:90,spe:95,height:"7.0m",weight:"206.5kg",gen:"Gen III",cat:"Legendary"},
  {id:448,name:"Lucario",emoji:"💎",types:["fighting","steel"],hp:70,atk:110,def:70,spa:115,spd:70,spe:90,height:"1.2m",weight:"54.0kg",gen:"Gen IV",cat:"Fighting"},
  {id:493,name:"Arceus",emoji:"✨",types:["normal"],hp:120,atk:120,def:120,spa:120,spd:120,spe:120,height:"3.2m",weight:"320kg",gen:"Gen IV",cat:"Legendary"},
  {id:571,name:"Zoroark",emoji:"🦊",types:["dark"],hp:60,atk:105,def:60,spa:105,spd:60,spe:105,height:"1.6m",weight:"81.1kg",gen:"Gen V",cat:"Dark"},
  {id:644,name:"Zekrom",emoji:"⚫",types:["dragon","electric"],hp:100,atk:150,def:120,spa:120,spd:100,spe:90,height:"2.9m",weight:"345kg",gen:"Gen V",cat:"Legendary"},
  {id:681,name:"Aegislash",emoji:"⚔️",types:["steel","ghost"],hp:60,atk:50,def:140,spa:50,spd:140,spe:60,height:"1.7m",weight:"53kg",gen:"Gen VI",cat:"Ghost"},
  {id:700,name:"Sylveon",emoji:"🎀",types:["fairy"],hp:95,atk:65,def:65,spa:110,spd:130,spe:60,height:"1.0m",weight:"23.5kg",gen:"Gen VI",cat:"Eeveelution"},
  {id:778,name:"Mimikyu",emoji:"🎭",types:["ghost","fairy"],hp:55,atk:90,def:80,spa:50,spd:105,spe:96,height:"0.2m",weight:"0.7kg",gen:"Gen VII",cat:"Ghost"},
  {id:888,name:"Zacian",emoji:"🐺",types:["fairy"],hp:92,atk:130,def:115,spa:80,spd:115,spe:138,height:"2.8m",weight:"110kg",gen:"Gen VIII",cat:"Legendary"},
  {id:906,name:"Sprigatito",emoji:"🐈",types:["grass"],hp:40,atk:61,def:54,spa:45,spd:45,spe:65,height:"0.4m",weight:"4.1kg",gen:"Gen IX",cat:"Starter"},
];

const FILTER_TYPES = ["All","Fire","Water","Grass","Electric","Psychic","Ghost","Dragon","Fairy","Dark","Normal","Legendary","Starter","Eeveelution"];

function TypeBadge({ type }) {
  const c = typeColors[type] || "#888";
  return (
    <span style={{
      fontSize:11,padding:"3px 10px",borderRadius:20,fontWeight:500,textTransform:"capitalize",
      background:`${c}22`,color:c,border:`1px solid ${c}44`,display:"inline-block"
    }}>{type}</span>
  );
}

function StatBar({ label, val }) {
  const pct = Math.min(100, Math.round(val / 160 * 100));
  return (
    <div style={{display:"flex",alignItems:"center",gap:10,marginBottom:10}}>
      <span style={{width:70,fontSize:12,color:"#888",flexShrink:0}}>{label}</span>
      <span style={{width:30,fontSize:12,fontWeight:500,textAlign:"right",flexShrink:0}}>{val}</span>
      <div style={{flex:1,height:6,background:"#f0f0f0",borderRadius:3,overflow:"hidden"}}>
        <div style={{height:"100%",width:`${pct}%`,background:"#E24B4A",borderRadius:3,transition:"width .6s ease"}}/>
      </div>
    </div>
  );
}

export default function PokemonHub() {
  const [search, setSearch] = useState("");
  const [filter, setFilter] = useState("All");
  const [selected, setSelected] = useState(ALL_POKEMON[8]); // Dragonite
  const [favorites, setFavorites] = useState(new Set());
  const [heroFloat, setHeroFloat] = useState(false);

  useEffect(() => {
    const t = setInterval(() => setHeroFloat(f => !f), 1500);
    return () => clearInterval(t);
  }, []);

  const filtered = ALL_POKEMON.filter(p => {
    const ms = p.name.toLowerCase().includes(search.toLowerCase());
    const mf = filter === "All" ||
      p.types.includes(filter.toLowerCase()) ||
      p.cat === filter;
    return ms && mf;
  });

  const toggleFav = (id, e) => {
    e.stopPropagation();
    setFavorites(prev => {
      const next = new Set(prev);
      next.has(id) ? next.delete(id) : next.add(id);
      return next;
    });
  };

  const typeCounts = {};
  ALL_POKEMON.forEach(p => p.types.forEach(t => { typeCounts[t] = (typeCounts[t]||0)+1; }));
  const sortedTypes = Object.entries(typeCounts).sort((a,b)=>b[1]-a[1]);
  const maxCount = sortedTypes[0]?.[1] || 1;

  const stats = [
    {label:"HP",val:selected.hp},{label:"Attack",val:selected.atk},
    {label:"Defense",val:selected.def},{label:"Sp. Atk",val:selected.spa},
    {label:"Sp. Def",val:selected.spd},{label:"Speed",val:selected.spe},
  ];

  const features = [
    {icon:"⚔️",title:"Type Matchups",desc:"Instantly see what's super effective, resistant, or immune for every Pokémon type combination."},
    {icon:"📊",title:"Stat Comparisons",desc:"Visualize base stats with interactive bars. Filter by legendary, starter, or any generation."},
    {icon:"🏆",title:"Team Builder",desc:"Build a squad of 6. Automatic coverage gap and synergy analysis included."},
    {icon:"🔍",title:"Advanced Search",desc:"Filter by type, generation, stat ranges, abilities, egg groups, and 30+ other criteria."},
    {icon:"✨",title:"Shiny Gallery",desc:"Toggle shiny versions for every Pokémon. Explore the full palette of alternate colorations."},
    {icon:"🗺️",title:"Location Guide",desc:"Find where to catch each Pokémon in every game, with encounter rates and conditions."},
  ];

  return (
    <div style={{fontFamily:"system-ui,sans-serif",maxWidth:1100,margin:"0 auto",padding:"0 1rem 3rem",color:"#1a1a1a"}}>

      {/* NAV */}
      <nav style={{display:"flex",alignItems:"center",justifyContent:"space-between",padding:"1rem 0",borderBottom:"0.5px solid #e0e0e0",marginBottom:"2rem"}}>
        <div style={{display:"flex",alignItems:"center",gap:10,fontSize:20,fontWeight:500}}>
          <div style={{width:28,height:28,borderRadius:"50%",background:"linear-gradient(180deg,#E24B4A 50%,white 50%)",border:"2px solid #333",display:"flex",alignItems:"center",justifyContent:"center"}}>
            <div style={{width:8,height:8,background:"white",borderRadius:"50%",border:"2px solid #333"}}/>
          </div>
          PokéHub
        </div>
        <div style={{display:"flex",gap:24,fontSize:14,color:"#666"}}>
          {["Pokédex","Types","Moves","Teams"].map(l => (
            <span key={l} style={{cursor:"pointer"}}>{l}</span>
          ))}
        </div>
        <button style={{background:"#E24B4A",color:"white",border:"none",padding:"8px 18px",borderRadius:8,fontSize:14,cursor:"pointer",fontWeight:500}}>
          Start Journey
        </button>
      </nav>

      {/* HERO */}
      <section style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:"2rem",alignItems:"center",padding:"2rem 0 3rem"}}>
        <div>
          <div style={{display:"inline-flex",alignItems:"center",gap:6,background:"#EBF5FF",color:"#185FA5",fontSize:12,padding:"4px 12px",borderRadius:20,marginBottom:"1rem"}}>
            ⚡ Gen I–IX Complete
          </div>
          <h1 style={{fontSize:42,fontWeight:500,lineHeight:1.2,marginBottom:"1rem"}}>
            The Ultimate<br/><span style={{color:"#E24B4A"}}>Pokédex</span><br/>Experience
          </h1>
          <p style={{fontSize:16,color:"#666",lineHeight:1.7,marginBottom:"1.5rem"}}>
            Explore, search, and master every Pokémon across all nine generations. Compare stats, discover type matchups, and build your perfect team.
          </p>
          <div style={{display:"flex",gap:12,marginBottom:"2rem"}}>
            <button style={{background:"#E24B4A",color:"white",border:"none",padding:"12px 24px",borderRadius:8,fontSize:15,cursor:"pointer",fontWeight:500}}>
              Open Pokédex
            </button>
            <button style={{background:"transparent",color:"#1a1a1a",border:"0.5px solid #ccc",padding:"12px 24px",borderRadius:8,fontSize:15,cursor:"pointer"}}>
              Build a Team
            </button>
          </div>
          <div style={{display:"grid",gridTemplateColumns:"repeat(3,1fr)",gap:12}}>
            {[["1,025","Pokémon"],["18","Types"],["956","Moves"]].map(([n,l]) => (
              <div key={l} style={{background:"#f5f5f5",borderRadius:8,padding:"1rem",textAlign:"center"}}>
                <div style={{fontSize:22,fontWeight:500}}>{n}</div>
                <div style={{fontSize:12,color:"#888",marginTop:2}}>{l}</div>
              </div>
            ))}
          </div>
        </div>
        <div style={{background:"#f8f8f8",border:"0.5px solid #e0e0e0",borderRadius:12,padding:"2rem",display:"flex",flexDirection:"column",alignItems:"center",justifyContent:"center",minHeight:280}}>
          <div style={{fontSize:90,lineHeight:1,marginBottom:8,transform:heroFloat?"translateY(-10px)":"translateY(0)",transition:"transform 1.5s ease-in-out"}}>
            {selected.emoji}
          </div>
          <div style={{fontSize:18,fontWeight:500,marginBottom:8}}>{selected.name}</div>
          <div style={{display:"flex",gap:8,flexWrap:"wrap",justifyContent:"center"}}>
            {selected.types.map(t => <TypeBadge key={t} type={t}/>)}
          </div>
        </div>
      </section>

      {/* SEARCH */}
      <section id="dex">
        <h2 style={{fontSize:22,fontWeight:500,marginBottom:"1.25rem"}}>Pokédex</h2>
        <div style={{background:"white",border:"0.5px solid #e0e0e0",borderRadius:12,padding:"1.5rem",marginBottom:"1.5rem"}}>
          <div style={{display:"flex",gap:10,marginBottom:"1rem"}}>
            <input
              type="text" placeholder="Search Pokémon by name…" value={search}
              onChange={e=>setSearch(e.target.value)}
              style={{flex:1,padding:"10px 14px",border:"0.5px solid #ccc",borderRadius:8,background:"#f8f8f8",fontSize:14,fontFamily:"inherit",outline:"none"}}
            />
            <button style={{background:"#E24B4A",color:"white",border:"none",padding:"10px 18px",borderRadius:8,fontSize:14,cursor:"pointer",fontWeight:500}}>
              Search
            </button>
          </div>
          <div style={{display:"flex",gap:8,flexWrap:"wrap"}}>
            {FILTER_TYPES.map(t => (
              <button key={t} onClick={()=>setFilter(t)}
                style={{padding:"6px 14px",borderRadius:20,border:filter===t?"1px solid #E24B4A":"0.5px solid #ddd",
                  background:filter===t?"#FCEBEB":"transparent",
                  color:filter===t?"#E24B4A":"#666",fontSize:13,cursor:"pointer",transition:"all .2s"}}>
                {t}
              </button>
            ))}
          </div>
        </div>
      </section>

      {/* DETAIL PANEL */}
      {selected && (
        <div style={{display:"grid",gridTemplateColumns:"1fr 2fr",gap:"1.5rem",background:"white",border:"0.5px solid #e0e0e0",borderRadius:12,padding:"1.5rem",marginBottom:"1.5rem"}}>
          <div style={{textAlign:"center"}}>
            <div style={{fontSize:88,lineHeight:1,marginBottom:8,display:"inline-block",transform:heroFloat?"translateY(-8px)":"translateY(0)",transition:"transform 1.5s ease-in-out"}}>
              {selected.emoji}
            </div>
            <div style={{fontSize:13,color:"#888",marginBottom:4}}>#{String(selected.id).padStart(3,"0")}</div>
            <div style={{fontSize:24,fontWeight:500,textTransform:"capitalize",marginBottom:10}}>{selected.name}</div>
            <div style={{display:"flex",justifyContent:"center",gap:6,marginBottom:"1rem",flexWrap:"wrap"}}>
              {selected.types.map(t=><TypeBadge key={t} type={t}/>)}
            </div>
            <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:8}}>
              {[["Height",selected.height],["Weight",selected.weight],["Generation",selected.gen],["Category",selected.cat]].map(([l,v])=>(
                <div key={l} style={{background:"#f5f5f5",borderRadius:8,padding:"8px 10px"}}>
                  <div style={{fontSize:11,color:"#888"}}>{l}</div>
                  <div style={{fontSize:14,fontWeight:500}}>{v}</div>
                </div>
              ))}
            </div>
          </div>
          <div>
            <h3 style={{fontSize:16,fontWeight:500,marginBottom:"1rem",color:"#888"}}>Base Stats</h3>
            {stats.map(s=><StatBar key={s.label} label={s.label} val={s.val}/>)}
          </div>
        </div>
      )}

      {/* POKEMON GRID */}
      <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fill,minmax(160px,1fr))",gap:14,marginBottom:"2.5rem"}}>
        {filtered.length === 0 ? (
          <div style={{gridColumn:"1/-1",textAlign:"center",padding:"3rem",color:"#888"}}>
            No Pokémon found. Try a different search!
          </div>
        ) : filtered.map(p => (
          <div key={p.id} onClick={()=>setSelected(p)}
            style={{background:"white",border:selected?.id===p.id?"2px solid #E24B4A":"0.5px solid #e0e0e0",
              borderRadius:12,padding:"1.25rem 1rem",textAlign:"center",cursor:"pointer",
              transition:"all .2s",position:"relative",
              transform:selected?.id===p.id?"translateY(-2px)":"none"}}>
            <button onClick={e=>toggleFav(p.id,e)}
              style={{position:"absolute",top:8,right:8,background:"none",border:"none",cursor:"pointer",fontSize:16,opacity:favorites.has(p.id)?1:.35}}>
              {favorites.has(p.id)?"❤️":"🤍"}
            </button>
            <span style={{fontSize:46,display:"block",marginBottom:8}}>{p.emoji}</span>
            <div style={{fontSize:11,color:"#aaa",marginBottom:3}}>#{String(p.id).padStart(3,"0")}</div>
            <div style={{fontSize:14,fontWeight:500,textTransform:"capitalize",marginBottom:8}}>{p.name}</div>
            <div style={{display:"flex",justifyContent:"center",gap:4,flexWrap:"wrap"}}>
              {p.types.map(t=><TypeBadge key={t} type={t}/>)}
            </div>
          </div>
        ))}
      </div>

      {/* TYPE CHART */}
      <section style={{marginBottom:"2.5rem"}}>
        <h2 style={{fontSize:22,fontWeight:500,marginBottom:"1.25rem"}}>Type Distribution</h2>
        <div style={{background:"white",border:"0.5px solid #e0e0e0",borderRadius:12,padding:"1.5rem"}}>
          {sortedTypes.map(([type,count]) => (
            <div key={type} style={{display:"flex",alignItems:"center",gap:12,marginBottom:10}}>
              <span style={{width:72,fontSize:13,fontWeight:500,textTransform:"capitalize",flexShrink:0}}>{type}</span>
              <div style={{flex:1,height:22,background:"#f0f0f0",borderRadius:4,overflow:"hidden"}}>
                <div style={{
                  height:"100%",width:`${Math.round(count/maxCount*100)}%`,
                  background:typeColors[type]||"#888",borderRadius:4,
                  display:"flex",alignItems:"center",paddingLeft:8,
                  fontSize:11,color:"white",fontWeight:500,transition:"width .8s ease"
                }}>{count}</div>
              </div>
              <span style={{fontSize:12,color:"#888",width:28,flexShrink:0}}>{count}</span>
            </div>
          ))}
        </div>
      </section>

      {/* FEATURES */}
      <section>
        <h2 style={{fontSize:22,fontWeight:500,marginBottom:"1.25rem"}}>Everything You Need</h2>
        <div style={{display:"grid",gridTemplateColumns:"repeat(3,1fr)",gap:14}}>
          {features.map(f=>(
            <div key={f.title} style={{background:"white",border:"0.5px solid #e0e0e0",borderRadius:12,padding:"1.25rem"}}>
              <div style={{fontSize:24,marginBottom:"0.75rem"}}>{f.icon}</div>
              <h3 style={{fontSize:15,fontWeight:500,marginBottom:6}}>{f.title}</h3>
              <p style={{fontSize:13,color:"#666",lineHeight:1.6}}>{f.desc}</p>
            </div>
          ))}
        </div>
      </section>

    </div>
  );
}

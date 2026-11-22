# PbLb
Public Leaderboards

1. Open the world Code Editor
2. Click on the very top lime plus on the left side of your screen
3. Name the file PbLb.ts

paste this in PbLb.ts to have the Variant that is better but redirects the players:
```ts
export function strToArr(s:String) { return (s || "").split(",").filter(p => p).map(p => { let [a, b] = p.split(" "); return { player: a, value: +b }; }); }
export function arrToStr(a:[]) { return a.map(x => x.player + " " + x.value + ",").join(""); }
export function getLb() { return strToArr(api.getLobbyDbValue("LB")); }
export function updLb(id:String, p?:Number) {let a = strToArr(api.getPlayerDbValue(id, "LB")), b = strToArr(api.getLobbyDbValue("LB")), v = [...new Map((p ? [...b, ...a] : [...a, ...b]).map(x => [x.player, x])).values()];v.push({ player: "empty", value: 0 }, { player: "empty", value: 0 }, { player: "empty", value: 0 }); v.sort((x, y) => y.value - x.value); v.length = 3; let s = arrToStr(v); api.setLobbyDbValue("LB", s); for (let q of api.getPlayerIds()) api.setPlayerDbValue(q, "LB", s);if(api.getLobbyName()!=="111"){if(api.getVariation()!=="done"){api.matchmakePlayer(id,undefined,"111")}}else {api.matchmakeToVariation(id,"done")} return v;}
export function setup(id:String) { updLb(id); }
export function rankPlayer(id:String, value:Number) { api.setPlayerDbValue(id, "LB", arrToStr([...strToArr(api.getPlayerDbValue(id, "LB")), { player: api.getEntityName(id), value }])); return updLb(id, 1); }
```

paste this in PbLb.ts to have the Variant that doesn't redirect the players:
```ts
export function strToArr(s:String) { return (s || "").split(",").filter(p => p).map(p => { let [a, b] = p.split(" "); return { player: a, value: +b }; }); }
export function arrToStr(a:[]) { return a.map(x => x.player + " " + x.value + ",").join(""); }
export function getLb() { return strToArr(api.getLobbyDbValue("LB")); }
export function updLb(id:String, p?:Number) {let a = strToArr(api.getPlayerDbValue(id, "LB")), b = strToArr(api.getLobbyDbValue("LB")), v = [...new Map((p ? [...b, ...a] : [...a, ...b]).map(x => [x.player, x])).values()];v.push({ player: "empty", value: 0 }, { player: "empty", value: 0 }, { player: "empty", value: 0 }); v.sort((x, y) => y.value - x.value); v.length = 3; let s = arrToStr(v); api.setLobbyDbValue("LB", s); for (let q of api.getPlayerIds()) api.setPlayerDbValue(q, "LB", s); return v;}
export function setup(id:String) { updLb(id); }
export function rankPlayer(id:String, value:Number) { api.setPlayerDbValue(id, "LB", arrToStr([...strToArr(api.getPlayerDbValue(id, "LB")), { player: api.getEntityName(id), value }])); return updLb(id, 1); }
```

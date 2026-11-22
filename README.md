# PbLb
Public Leaderboards

paste this in file PbLb.ts:
```ts
export function strToArr(s) { return (s || "").split(",").filter(p => p).map(p => { let [a, b] = p.split(" "); return { player: a, value: +b }; }); }
export function arrToStr(a) { return a.map(x => x.player + " " + x.value + ",").join(""); }
export function getLb() { return strToArr(api.getLobbyDbValue("LB")); }
export function updLb(id, p?) {let a = strToArr(api.getPlayerDbValue(id, "LB")), b = strToArr(api.getLobbyDbValue("LB")), v = [...new Map((p ? [...b, ...a] : [...a, ...b]).map(x => [x.player, x])).values()];v.push({ player: "empty", value: 0 }, { player: "empty", value: 0 }, { player: "empty", value: 0 }); v.sort((x, y) => y.value - x.value); v.length = 3; let s = arrToStr(v); api.setLobbyDbValue("LB", s); for (let q of api.getPlayerIds()) api.setPlayerDbValue(q, "LB", s);if(api.getLobbyName()!=="111"){if(api.getVariation()!=="done"){api.matchmakePlayer(id,undefined,"111")}}else {api.matchmakeToVariation(id,"done")} return v;}
export function setup(id) { updLb(id); }
export function rankPlayer(id, value) { api.setPlayerDbValue(id, "LB", arrToStr([...strToArr(api.getPlayerDbValue(id, "LB")), { player: api.getEntityName(id), value }])); return updLb(id, 1); }
```

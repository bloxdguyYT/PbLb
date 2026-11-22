1. Rank by Gold Coins
  ```js
  import * as pl from "./PbLb.ts";
  const ents = [];
  for (let i = 0; i < 3; i++) {
      ents[i] = api.attemptCreateMeshEntity("BloxdBlock", { blockName: "Invisible Solid", size: [1, 1, 1] }, "");
      api.setPosition(ents[i], 0, 10 - i, 0);
  }
  
  onPlayerJoin = (id) => {
      pl.updLb(id);
      api.setClientOptions(id, {
          lobbyLeaderboardInfo: {
              Name: { displayName: "Name", sortPriority: 1 },
              Coins: { displayName: "Coins", sortPriority: 0 },
          }
      });
  };
  
  tick = () => {
      for (const id of api.getPlayerIds()) {
          const amt = api.getInventoryItemAmount(id, "Gold Coin");
          pl.rankPlayer(id, amt);
          api.setTargetedPlayerSettingForEveryone(id, "lobbyLeaderboardValues", {
              Name: api.getEntityName(id),
              Coins: amt,
          }, true);
      }
      const lb = pl.getLb();
      for (let i = 0; i < 3; i++) {
          api.setTargetedPlayerSettingForEveryone(ents[i], "nameTagInfo", { content: [lb[i].player + "   " + lb[i].value], backgroundColor:"black",border:{colour:"cyan",style:"glow"} }, true);
      }
  };
  ```

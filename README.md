# WurstMMD
A w3mmd library for WC3 Wurst maps. Learn more here https://wc3stats.com/docs/about

## Usage
### flagPlayer
Sets a flag for a player.
```wurst
import MMD

MMD.flagPlayer(players[0], PlayerFlag.Winner);
MMD.flagPlayer(players[1], PlayerFlag.Loser);
```

### defineEvent
Defines a w3mmd event. The second argument is the format, where the nth
argument (0-indexed) is formatted `{n}`.

Returns a callback used to log an instance of the event.
```wurst
import MMD
import RegisterEvents

let killEvent = MMD.defineEvent("kill", "{0} killed {1}", "killer", "victim");

registerPlayerUnitEvent(EVENT_PLAYER_UNIT_DEATH) () ->
  killEvent.raise(
    GetKillingUnit().getOwner().getName(),
    GetDyingUnit().getOwner().getName())
```

### define[String/Real/Int]Value
Defines a string, real or int value. Values can be updated throughout the game.

Returns a callback to set the value.
```wurst
import MMD

let heroValue = MMD.defineStringValue("hero");

heroValue.set(players[0], "Archmage");
heroValue.set(players[1], "Mountain King");

let heroLevelValue = MMD.defineIntValue("heroLvl");

heroLevelValue.set(players[0], 1);
heroLevelValue.add(players[0], 1);
heroLevelValue.sub(players[0], 1);
```

### logCustom
Emits some custom w3mmd data. This would be used by a specialized parser.
```wurst
import MMD

MMD.logCustom("build", "v1.2.3")
```

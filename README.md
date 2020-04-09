# ttt2mg
The TTT2 Minigames gamemode. It adds custom minigames into TTT2. It fully supports TTT2 ULX.

# Customization
## TTT2 ULX
You can modify or force a gamemode with the help of TTT2 ULX

## ConVars
If you don't wanna use TTT2 ULX, you can modify these ConVars on your own:

ConVar | Utilization | Realm
--- | --- | ---
`ttt2_minigames` | Toggle whether the `Minigame`s gamemode is enabled | `server`
`ttt2_minigames_autostart` | Toggle whether a random `Minigame` should start on every round begin | `server`
`ttt2_minigames_show_popup` | Toggle whether the `Minigame`'s name and the description should be displayed on start | `client`

# Developer section
## How to create a custom `Minigame`?

1. Create a folder with the add-on name you prefere (need to be an unique folder name). Pay attention to keep the name lowercase.
2. Create a `lua` folder in this new created folder
3. Create a `minigames` folder in the `lua` folder
4. Create another `minigames` folder in the previously created `minigames` folder. Yea, seems to be redundant, but it isn't.
5. Create a .lua file with the name of your new minigame (need to be an unique name!), e.g. `sh_my_unique_cool_minigame.lua`, in the folder `lua/minigames/minigames/`.
6. Modify the following code as you prefere:

```lua
MINIGAME.author = "TheNameNobodyIsInterestedInAndNobodyGonnaGiveALook" -- author
MINIGAME.contact = "NobodyWritesMe@mail.cry" -- contact to the author

---
-- Called if the @{MINIGAME} activates
-- @hook
-- @realm shared
function MINIGAME:OnActivation()

end

---
-- Called if the @{MINIGAME} deactivates
-- @hook
-- @realm shared
function MINIGAME:OnDeactivation()

end
```

Here is an easy example of a `Minigame`: [Hardcore Minigame](https://github.com/TTT-2/ttt2mg/tree/master/lua/minigames/minigames)

## How to customize and interact with this TTT2 gamemode?

### MINIGAME
#### Hooks (**`shared`**)
Hook | Utilization
--- | ---
`MINIGAME:OnActivation` | Called if the `Minigame` is activated
`MINIGAME:OnDeactivation` | Called if the `Minigame` is deactivated

#### Functions
Function | Utilization | Realm
--- | --- | ---
`MINIGAME:Activate` | Activates the `Minigame`. By default, this is done autimatically (internally) | `shared`
`MINIGAME:Deactivate` | Deactivates the `Minigame`. By default, this is done autimatically (internally) | `shared`
`MINIGAME:IsActive` | Returns whether the `Minigame` is active | `shared`
`MINIGAME:IsSelectable` | Returns whether the `Minigame` is selectable (and take place in the `minigame`s selection) | `server`

### `minigames` module
#### Functions
Function | Utilization | Realm
--- | --- | ---
`minigames.IsBasedOn` | Checks if name is based on base | `shared`
`minigames.GetStored` | Gets the real `Minigame` table (not a copy) | `shared`
`minigames.GetList` | Get a list (copy) of all registered `Minigame`s, that can be displayed (no abstract `Minigame`s) | `shared`
`minigames.GetRealList`| Get an indexed list of all the registered `Minigame`s including abstract `Minigame`s | `shared`
`minigames.GetActiveList`| Returns a list of active `Minigame`s | `shared`
`minigames.GetByIndex` | Get the `Minigame` table by the `Minigame` id | `shared`
`minigames.ForceNextMinigame` | Forces the next `Minigame` | `server`
`minigames.GetForcedNextMinigame`| Returns the next forced `Minigame` | `server`
`minigames.Select`| Selects a `Minigame` based on the current available `Minigame`s | `server`

### global functions (**`shared`**)
Function | Utilization
--- | ---
`ActivateMinigame` | Activates a `Minigame`. If called on `server`, the sync with the `client`s will be run. If called on `client`, a popup will be displayed for 12 seconds
`DeactivateMinigame` | Deactivates a `Minigame`. If called on `server`, the sync with the `client`s will be run.

### `GAMEMODE` hooks (**`shared`**)
Hook | Utilization
--- | ---
`TTT2MGPreActivate`| Called right before the `Minigame` activates
`TTT2MGActivate` | Called if the `Minigame` activates
`TTT2MGPostActivate` | Called after the `Minigame` was activated
`TTT2MGPreDeactivate`| Called right before the `Minigame` deactivates
`TTT2MGDeactivate` | Called if the `Minigame` deactivates
`TTT2MGPostDeactivate` | Called after the `Minigame` was deactivated

### Multilanguage support
Here is an example how to add language support to your `Minigame`:

```lua
MINIGAME.lang = {
	lang = {
		name = {
			English = "Example Minigame"
		},
		desc = {
			English = "Some interesting facts about or something similar."
		}
	}
}
```
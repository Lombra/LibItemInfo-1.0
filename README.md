# LibItemInfo-1.0

Caches requested item info, allowing much quicker access on subsequent requests than `GetItemInfo`. Caches return values from `GetItemInfo` and are localised wherever applicable.

Callbacks when items get cached.

Simply get a reference to the library and then use it as a table, accessing item info using either item ID or item string.

If the item is cached, will return a table:

```
items[13262] = {
	name = "Ashbringer",
	quality = Enum.ItemQuality.Legendary,
	itemLevel = 76,
	requiredLevel = 60,
	class = "Weapon",
	classID = Enum.ItemClass.Weapon,
	subClass = "Two-Handed Swords",
	subClassID = Enum.ItemWeaponSubclass.Sword2H,
	invType = "INVTYPE_2HWEAPON",
	bindType = Enum.ItemBind.OnAcquire,
	stackSize = 1,
	expansionID = LE_EXPANSION_CLASSIC,
}
```

This table is taken directly from the library database and must not be modified.

If not cached, will return nil and be queued for caching. A callback will fire when the item gets cached.

##### Callbacks

```
OnItemInfoReceivedBatch()
```

Fires once per frame update after all queued items that were cached were entered into the database.

##### Example usage:

```
local ItemInfo = LibStub("LibItemInfo-1.0")

local myAddon = {}

ItemInfo.RegisterCallback(myAddon, "OnItemInfoReceivedBatch", function(event)
	if ItemInfo[42] then
		print("Received item info")
	end
end)

local item = ItemInfo[42]

if item then
	print(item.name)
end
```

# PUID[^1]
## Table of Contents
- [Structure](#structure)
  - [Variants](#variants)
  - [Categories](#categories)
- [The list of reserved PUIDs](#the-list-of-reserved-puids)

## Structure
All PUIDs consist of two parts: the first byte is the metadata and the next 15 bytes are the data itself.

The first byte is made up of the [variant](#variants) and [category](#categories):
```py
# variant and category - number between 0 and 15
metadata = variant << 4 | category
```

And the whole PUID is made up like this:
```py
# metadata compiled earlier
puid = metadata.to_bytes(1, "big")

# value - PUID value (15 bytes)
puid += value
```

### Variants
![variants](images/variants.svg)

#### "Unknown" variant (`00`)
> ![unknown variant](images/unknown_variant.svg)<br>
> `V` - variant (`0`); `x` - the part (4 bits) of value

The value of the PUID of this variant is a complete copy of the value of the UUID from which the PUID was formed. Instead of a category, this variant has 4 more data bits (otherwise the UUID of the 4th variant would not fit)

#### "Random" variant (`01`)
> ![random variant](images/rr_variant.svg)<br>
> `V` - variant (`1`); `C` - [category](#categories); `x` - the part (4 bits) of value

This PUID has a value of 15 random bytes

#### "Reversed" variant (`02`)
> ![reversed variant](images/rr_variant.svg)<br>
> `V` - variant (`2`); `C` - [category](#categories); `x` - the part (4 bits) of value

The value of the reserved PUID is a sequence number from `0` to `2¹²⁰-1`

#### Time-based variant (`03`)
> ![time-based variant](images/time_variant.svg)<br>
> `V` - variant (`2`); `C` - [category](#categories); `t` - the part (4 bits) of PUID creation time; `x` - the part (4 bits) of random value

The first 8 bytes of the value are the time in timestamp64 format. The next 7 bytes are a random number from `0` to `2⁵⁶-1`.

### Categories
![categories](images/categories.svg)

## The list of reserved PUIDs
PUID                                   | Type               | Description/Preview
-------------------------------------- | ------------------ | ------------------------------------------------------------
`20000000-0000-0000-0000-000000000000` |                    | Points to the end in lists where the key is a PUID
`21000000-0000-0000-0000-000000000000` | Group              | Recycle bin
`21000000-0000-0000-0000-000000000001` | Group              | Template group
`23000000-0000-0000-0000-000000000000` | Default icon       | ![key](/assets/icons/groups/key.svg)
`23000000-0000-0000-0000-000000000001` | Default icon       | ![world](/assets/icons/groups/world.svg)
`23000000-0000-0000-0000-000000000002` | Default icon       | ![server](/assets/icons/groups/server.svg)
`23000000-0000-0000-0000-000000000003` | Default icon       | ![windows](/assets/icons/groups/windows.svg)
`23000000-0000-0000-0000-000000000000` | Default icon       | ![linux](/assets/icons/groups/linux.svg)
`23000000-0000-0000-0000-000000000005` | Default icon       | ![android](/assets/icons/groups/android.svg)
`23000000-0000-0000-0000-000000000006` | Default icon       | ![apple](/assets/icons/groups/apple.svg)
`23000000-0000-0000-0000-000000000007` | Default icon       | ![clipboard-list](/assets/icons/groups/clipboard-list.svg)
`23000000-0000-0000-0000-000000000008` | Default icon       | ![clipboard-check](/assets/icons/groups/clipboard-check.svg)
`23000000-0000-0000-0000-000000000009` | Default icon       | ![user](/assets/icons/groups/user.svg)
`23000000-0000-0000-0000-00000000000A` | Default icon       | ![cogs](/assets/icons/groups/cogs.svg)
`23000000-0000-0000-0000-00000000000B` | Default icon       | ![passport](/assets/icons/groups/passport.svg)
`23000000-0000-0000-0000-00000000000C` | Default icon       | ![camera](/assets/icons/groups/camera.svg)
`23000000-0000-0000-0000-00000000000D` | Default icon       | ![floppy](/assets/icons/groups/floppy.svg)
`23000000-0000-0000-0000-00000000000E` | Default icon       | ![compact-disc](/assets/icons/groups/compact-disc.svg)
`23000000-0000-0000-0000-00000000000F` | Default icon       | ![bolt](/assets/icons/groups/bolt.svg)
`23000000-0000-0000-0000-000000000010` | Default icon       | ![tools](/assets/icons/groups/tools.svg)
`23000000-0000-0000-0000-000000000011` | Default icon       | ![wrench](/assets/icons/groups/wrench.svg)
`23000000-0000-0000-0000-000000000012` | Default icon       | ![folder](/assets/icons/groups/folder.svg)
`23000000-0000-0000-0000-000000000013` | Default icon       | ![file](/assets/icons/groups/file.svg)
`23000000-0000-0000-0000-000000000014` | Default icon       | ![note](/assets/icons/groups/note.svg)
`23000000-0000-0000-0000-000000000015` | Default icon       | ![history](/assets/icons/groups/history.svg)
`23000000-0000-0000-0000-000000000016` | Default icon       | ![address-book](/assets/icons/groups/address-book.svg)
`23000000-0000-0000-0000-000000000017` | Default icon       | ![certification](/assets/icons/groups/certification.svg)
`23000000-0000-0000-0000-000000000018` | Default icon       | ![vault](/assets/icons/groups/vault.svg)
`23000000-0000-0000-0000-000000000019` | Default icon       | ![percentage](/assets/icons/groups/percentage.svg)
`23000000-0000-0000-0000-00000000001A` | Default icon       | ![wallet](/assets/icons/groups/wallet.svg)
`23000000-0000-0000-0000-00000000001B` | Default icon       | ![bitcoin](/assets/icons/groups/bitcoin.svg)
`23000000-0000-0000-0000-00000000001C` | Default icon       | ![landmark](/assets/icons/groups/landmark.svg)
`23000000-0000-0000-0000-00000000001D` | Default icon       | ![credit-card](/assets/icons/groups/credit-card.svg)
`23000000-0000-0000-0000-00000000001E` | Default icon       | ![coins](/assets/icons/groups/coins.svg)
`23000000-0000-0000-0000-00000000001F` | Default icon       | ![bookmark](/assets/icons/groups/bookmark.svg)
`23000000-0000-0000-0000-000000000020` | Default icon       | ![box](/assets/icons/groups/box.svg)
`23000000-0000-0000-0000-000000000021` | Default icon       | ![wifi](/assets/icons/groups/wifi.svg)

[^1]: PUID - **P**iema **U**nique **Id**entifier - A little (a lot) redesigned UUID

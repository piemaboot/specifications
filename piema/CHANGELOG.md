#### `v2.1`
- Removed `template` flag
> Not needed for the same reason that the `templates` flag isn't needed.

- Removed `templates` flag
> Groups with templates have their own PUID, just like the recycle bin. Therefore, this flag is not needed.

- Removed `recyle_bin` parameter from metadata
> The PUID is reserved for the recycle bin, so a separate parameter is not needed.

- Removed `is_empty` database header
> Extremely useless headline

- Added `puid` header to databases
> This is needed to identify databases, e.g. in keys

- `UUID` replaced by `PUID`
> PUID is tailored specifically for Piema formats and is more suitable for them.

#### `v2.0`
- Added `is_empty` header
> It indicates whether the database is empty or not. If it is, it has the value `01`, otherwise `00`

- Added `out_of_sync` flag to groups and entries
> This flag indicates that this group (or entry) doesn't need to be synchronized. Synchronization means transferring database data to another device.

- Added `comment` field to attributes

- Added `custom` field to custom icons

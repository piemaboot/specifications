# Types of Piema log entries
Type      | Data                                       | Description
--------- | ------------------------------------------ | ---------------------------------
`end`     | —                                          | End of journal entries
`created` | UTF-8 string (initiator[^1]) + `\x00`      | Item (entry/group/icon) created
`update`  | Full copy of item data before modification | Item (entry/group/icon) updated
`deleted` | [Below](#data-of-the-deleted-type)         | Item (entry/group/icon) deleted
`copied`  | PUID of entry copy                         | Item (entry/group/icon) copied
`getted`  | [Below](#data-of-the-getted-type)          | Item (entry/group/icon) requested
`moved`   | [Below](#data-of-the-moved-type)           | Item (entry/group/icon) moved

## Data of the `deleted` type
The first field - initiator[^1] - is a UTF-8 string ending in `\0`. 

This is followed by the PUID of the group, which occupies 16 bytes, from which the item was deleted.

## Data of the `getted` type
![logs[getted] data structure](images/logs_getted.svg)

The first field - initiator[^1] - is a UTF-8 string ending with `\0`. 

This is followed by the PUID of the requested element, which occupies 16 bytes.

Then comes the requested attributes. They are stored [in the same way as the entry.](README.md#attributes)
> Fields such as `name`, `comment`, `tags`, etc. are written as attributes with the following names:
> Name (bytes) | Field
> ------------ | --------------
> `01 01`      | **template**
> `01 02`      | **name**      
> `01 03`      | **comment**   
> `01 04`      | **icon**      
> `01 05`      | **created**   
> `01 06`      | **modified**  
> `01 07`      | **expiry**    
> `01 08`      | **flags**     
> `01 09`      | **background**
> `01 0A`      | **foreground**
> `01 0B`      | **tags**      
> `01 0C`      | **custom**

The last field, attachments, is also stored [as a entry.](README.md#attachments)

## Data of the `moved` type
The first field - initiator[^1] - is a UTF-8 string ending with `\0`. 

This is followed by the PUID of the group, which occupies 16 bytes, from which the item was moved.

[^1]: Initiator - the object that triggered this action<br>
      **Special Values:** `system` - caused by the system<br>
      `generator` - caused by the file generator

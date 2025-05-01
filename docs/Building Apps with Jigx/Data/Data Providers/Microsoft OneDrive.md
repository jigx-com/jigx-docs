---
title: Microsoft OneDrive
slug: ew-X-onedrive
description: Learn how to integrate Microsoft OneDrive with Jigx app solutions in this comprehensive document. Find detailed instructions on authorization requirements and necessary permissions for accessing and managing files in OneDrive. Discover various integration
createdAt: Thu May 25 2023 15:27:26 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Nov 23 2023 07:36:14 GMT+0000 (Coordinated Universal Time)
---

Microsoft OneDrive connects you to all your files by storing and protecting your files, sharing them with others, and getting to them from all your devices. Jigx app solutions integrate with OneDrive allowing you to interact with your existing files or add new files. No files are stored in the Jigx cloud as they are routed to OneDrive.

## **Authorization requirements**&#x20;

A Graph OAuth token is required for a solution to integrate with OneDrive. Set the Graph OAuth token in the [Credentials](./../../../Administration/Solutions/Credentials.md) tab in Jigx Management. The Graph OAuth token must have the following permissions:

- Files.ReadWrite.All (My Files)
- Sites.ReadWrite.All (Shared Folders)

&#x20;The *Shared* folder operations rely on permissions granted by the person who shared the folder.

## Integration support includes:

- **Folder sync** - syncs metadata and not file contents
- **Location paths** - shared and my files (root)&#x20;
- **Methods **- create, update, save, delete, and download
- **Download to documents folder** (private to Jigx app) - depends on the device's operating system. See [device storage location ]()for the exact location

## Specifying the file path

When working with the OneDrive data provider use `entity` to specify the file path, for example, `entity: myfiles/Finance/Invoices`. The specified file path with the folders must already exist in OneDrive.&#x20;

There are two supported base entities myfiles and shared.&#x20;

1. `entity: myfiles`, and `myfiles` with additional paths e.g. `entity: myfiles/Finance/Invoices`
2. `entity: shared/path`, a `shared` entity always requires a path e.g. `entity: shared/HR/Global/Forms`

## Supported methods:

- [Create]()
- [Update]()
- **Save** - Using the `method: save` will create a new file if the filename does not exist, otherwise, the save will function as an update method.
- [Delete]()
- [List]()
- [Download]()

## Properties :&#x20;

- `file` - reference the physical file&#x20;
- `fileName` - add the file name with the extension, e.g. Invoice.pdf&#x20;
- `tokenType` - OAuth token credentials name
- `method` - the CRUD method to use&#x20;

## Examples and code snippets

The following examples with code snippets are provided

- [Create a file]()
- [Update/Save a file]()
- [Delete a file]()
- [List files]()
- [Download a file]()


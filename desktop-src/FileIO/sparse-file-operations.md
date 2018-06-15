---
Description: Determine whether a file system supports sparse files by calling the GetVolumeInformation function.
ms.assetid: a08f6bbc-c139-4396-8964-4aa63285f3f5
title: Sparse File Operations
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Sparse File Operations

To determine whether a file system supports sparse files, call the [**GetVolumeInformation**](/windows/desktop/api/FileAPI/nf-fileapi-getvolumeinformationa) function and examine the **FILE\_SUPPORTS\_SPARSE\_FILES** bit flag returned through the *lpFileSystemFlags* parameter.

Most applications are not aware of sparse files and will not create sparse files. The fact that an application is reading a sparse file is transparent to the application. An application that is aware of sparse-files should determine whether its data set is suitable to be kept in a sparse file. After that determination is made, the application must explicitly declare a file as sparse, using the [**FSCTL\_SET\_SPARSE**](https://msdn.microsoft.com/en-us/library/Aa364596(v=VS.85).aspx) control code.

After an application has set a file to be sparse, the application can use the [**FSCTL\_SET\_ZERO\_DATA**](https://msdn.microsoft.com/en-us/library/Aa364597(v=VS.85).aspx) control code to set a region of the file to zero. In addition, the application can use the [**FSCTL\_QUERY\_ALLOCATED\_RANGES**](https://msdn.microsoft.com/en-us/library/Aa364582(v=VS.85).aspx) control code to speed searches for nonzero data in the sparse file.

When you perform a write operation (with a function or operation other than [**FSCTL\_SET\_ZERO\_DATA**](https://msdn.microsoft.com/en-us/library/Aa364597(v=VS.85).aspx)) whose data consists of nothing but zeros, zeros will be written to the disk for the entire length of the write. To zero out a range of the file and maintain sparseness, use **FSCTL\_SET\_ZERO\_DATA**.

A sparseness-aware application may also set an existing file to be sparse. If an application sets an existing file to be sparse, it should then scan the file for regions which contain zeros, and use [**FSCTL\_SET\_ZERO\_DATA**](https://msdn.microsoft.com/en-us/library/Aa364597(v=VS.85).aspx) to reset those regions, thereby possibly deallocating some physical disk storage. An application upgraded to sparse file awareness should perform this conversion.

When you perform a read operation from a zeroed-out portion of a sparse file, the operating system may not read from the hard disk drive. Instead, the system recognizes that the portion of the file to be read contains zeros, and it returns a buffer full of zeros without actually reading from the disk.

As with any other file, the system can write data to or read data from any position in a sparse file. Nonzero data being written to a previously zeroed portion of the file may result in allocation of disk space. Zeros being written over nonzero data (only with [**FSCTL\_SET\_ZERO\_DATA**](https://msdn.microsoft.com/en-us/library/Aa364597(v=VS.85).aspx)) may result in a deallocation of disk space.

> [!Note]  
> It is up to the application to maintain sparseness by writing zeros with [**FSCTL\_SET\_ZERO\_DATA**](https://msdn.microsoft.com/en-us/library/Aa364597(v=VS.85).aspx).

 

Defragmentation tools that handle compressed files on NTFS file systems will correctly handle sparse files on NTFS file system volumes. Large and highly fragmented sparse files can exceed the NTFS limitation on disk extents before available space is used. For more information, see [Extending a File may fail with "Disk Full" Error even though Volume has Free Space](Http://go.microsoft.com/fwlink/p/?linkid=128908).

 

 



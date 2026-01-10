---
created: 2024-09-01
aliases: 
tags:
  - type/note
topic:
  - "[[Docker]]"
source: "[[Containers for Developers]]"
---
An overlay filesystem is a union mount filesystem (a way of combining multiple directories into one that appears to contain their whole combined content) that combines multiple underlying mount points. This results in a structure with a single directory that contains all underlying files and sub-directories from all sources. 

Overlay filesystems merge content from directories, combining the file objects (if any) yielded by different processes, with the upper filesystem taking precedence.

Container runtimes manage how these overlay folders will be included inside containers and the magic behind that. The mechanism for this is based on specific operating system drivers that implement copy-on-write filesystems. Layers are arranged one on top of the other and only files modified within them are merged on the upper layer.

>[!note]
> Copy-on-write uses small layered filesystems or folders. Files from any layer are accessible to read access, but write requires searching for the file within the underlying layers and copying this file to the upper layer to store the changes. Therefore, the I/O overhead from reading files is very small and we can keep multiple layers for better file distribution between containers. In contrast, writing requires more resources and it would be better to leave big files and those subject to many or continuous modifications out of the container layer.

---
title: JetGetIndexInfo Function
TOCTitle: JetGetIndexInfo Function
ms:assetid: c6235281-e208-4966-bc66-ec1ab27333c0
ms:mtpsurl: https://msdn.microsoft.com/library/Gg294084(v=EXCHG.10)
ms:contentKeyID: 32765699
ms.date: 04/11/2016
ms.topic: reference
api_name: 
- JetGetIndexInfoW
- JetGetIndexInfoA
- JetGetIndexInfo
topic_type: 
- apiref
- kbArticle
api_type: 
- DLLExport
- COM
api_location: 
- ESENT.DLL
ROBOTS: INDEX,FOLLOW

---

# JetGetIndexInfo Function


_**Applies to:** Windows | Windows Server_

## JetGetIndexInfo Function

The **JetGetIndexInfo** function retrieves information about an index.

```cpp
    JET_ERR JET_API JetGetIndexInfo(
      __in          JET_SESID sesid,
      __in          JET_DBID dbid,
      __in          const tchar* szTableName,
      __in          const tchar* szIndexName,
      __out         void* pvResult,
      __in          unsigned long cbResult,
      __in          unsigned long InfoLevel
    );
```

### Parameters

*sesid*

The database session context to use for the API call.

*dbid*

The database identifier to use for the API call.

*szTableName*

The name of the table containing the index with the information to retrieve.

*szIndexName*

The name of the index with the information to retrieve.

*pvResult*

Pointer to a buffer that will receive the desired information. The buffer should be aligned to hold the type required. The type of the buffer is dependent on the *InfoLevel* parameter.

*cbResult*

The size, in bytes, of the buffer passed as *pvResult*.

*InfoLevel*

The information that will be stored in *pvResult*. The following options can be used for this parameter.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Value</p></th>
<th><p>Meaning</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JET_IdxInfo</p></td>
<td><p><em>pvResult</em> is interpreted as a <a href="gg269185(v=exchg.10).md">JET_INDEXLIST</a> structure. On success, the <a href="gg269185(v=exchg.10).md">JET_INDEXLIST</a> structure receives information about the index. On failure, the contents of <em>pvBuffer</em> are undefined.</p></td>
</tr>
<tr class="even">
<td><p>JET_IdxInfoCount</p></td>
<td><p><em>pvResult</em> is interpreted as a ULONG. On success, the ULONG holds the count of indexes on the specified table. <em>szIndexName</em> is ignored. On failure, the contents of <em>pvBuffer</em> are undefined.</p></td>
</tr>
<tr class="odd">
<td><p>JET_IdxInfoIndexId</p></td>
<td><p><em>pvResult</em> is interpreted as a <a href="gg269327(v=exchg.10).md">JET_INDEXID</a>. On success, the <a href="gg269327(v=exchg.10).md">JET_INDEXID</a> structure receives information about the index. On failure, the contents of <em>pvBuffer</em> are undefined.</p></td>
</tr>
<tr class="even">
<td><p>JET_IdxInfoLangid</p></td>
<td><p>JET_IdxInfoLangid is deprecated. Use JET_IdxInfoLCID and the <a href="/windows/win32/api/winnt/nf-winnt-langidfromlcid">LANGIDFROMLCID</a> macro instead.</p></td>
</tr>
<tr class="odd">
<td><p>JET_IdxInfoLCID</p></td>
<td><p><em>pvResult</em> is interpreted as an LCID. On success, the LCID holds the Locale Identifier of the index. On failure, the contents of <em>pvBuffer</em> are undefined.</p>
<p><strong>Windows XP:  </strong>JET_IdxInfoLCID is introduced in Windows XP.</p></td>
</tr>
<tr class="even">
<td><p>JET_IdxInfoList</p></td>
<td><p><em>pvResult</em> is interpreted as a <a href="gg269185(v=exchg.10).md">JET_INDEXLIST</a> structure. On success, the <a href="gg269185(v=exchg.10).md">JET_INDEXLIST</a> structure receives information about the index. On failure, the contents of <em>pvBuffer</em> are undefined.</p></td>
</tr>
<tr class="odd">
<td><p>JET_IdxInfoOLC</p></td>
<td><p>JET_IdxInfoOLC is obsolete.</p></td>
</tr>
<tr class="even">
<td><p>JET_IdxInfoResetOLC</p></td>
<td><p>JET_IdxInfoResetOLC is obsolete.</p></td>
</tr>
<tr class="odd">
<td><p>JET_IdxInfoSpaceAlloc</p></td>
<td><p><em>pvResult</em> is interpreted as a ULONG. On success, the ULONG holds the space usage of the index. On failure, the contents of <em>pvBuffer</em> are undefined.</p></td>
</tr>
<tr class="even">
<td><p>JET_IdxInfoSysTabCursor</p></td>
<td><p>JET_IdxInfoSysTabCursor is obsolete.</p></td>
</tr>
<tr class="odd">
<td><p>JET_IdxInfoVarSegMac</p></td>
<td><p><em>pvResult</em> is interpreted as a USHORT. On success, the USHORT holds the value of <em>cbVarSegMac</em> used when the index was created. See <a href="gg269186(v=exchg.10).md">JET_INDEXCREATE</a> for a description of <em>cbVarSegMac</em>. On failure, the contents of <em>pvBuffer</em> are undefined.</p></td>
</tr>
<tr class="even">
<td><p>JET_IdxInfoKeyMost</p></td>
<td><p><em>pvResult</em> is interpreted as a USHORT. On success, the USHORT holds the value of <em>cbKeyMost</em> used when the index was created. See <a href="gg269186(v=exchg.10).md">JET_INDEXCREATE</a> for a description of <em>cbKeyMost</em>. On failure, the contents of <em>pvBuffer</em> are undefined.</p>
<p><strong>Windows Vista:  </strong>JET_IdxInfoKeyMost is introduced in Windows Vista.</p></td>
</tr>
<tr class="odd">
<td><p>JET_IdxInfoCreateIndex</p></td>
<td><p><em>pvResult</em> is interpreted as a <a href="gg269186(v=exchg.10).md">JET_INDEXCREATE</a> structure. On failure, the contents of <em>pvBuffer</em> are undefined.</p>
<p><strong>Windows 7:  </strong>JET_IdxInfoCreateIndex is introduced in Windows 7.</p></td>
</tr>
<tr class="even">
<td><p>JET_IdxInfoCreateIndex2</p></td>
<td><p><em>pvResult</em> is interpreted as a <a href="gg294082(v=exchg.10).md">JET_INDEXCREATE2</a> structure. On failure, the contents of <em>pvBuffer</em> are undefined.</p>
<p><strong>Windows 7:  </strong>JET_IdxInfoCreateIndex2 is introduced in Windows 7.</p></td>
</tr>
</tbody>
</table>


### Return Value

This function returns the [JET_ERR](gg294092\(v=exchg.10\).md) datatype with one of the following return codes. For more information about the possible ESE errors, see [Extensible Storage Engine Errors](gg269184\(v=exchg.10\).md) and [Error Handling Parameters](gg269173\(v=exchg.10\).md).

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Return code</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JET_errSuccess</p></td>
<td><p>The operation completed successfully.</p></td>
</tr>
<tr class="even">
<td><p>JET_errIndexNotFound</p></td>
<td><p>The specified index cannot be found in the specified table.</p></td>
</tr>
<tr class="odd">
<td><p>JET_wrnBufferTruncated</p></td>
<td><p>The buffer passed in as <em>pvResult</em> was too small. The contents of the buffer are undefined.</p></td>
</tr>
</tbody>
</table>


#### Remarks

**JetGetIndexInfo** and [JetGetTableIndexInfo](gg294102\(v=exchg.10\).md) retrieve identical information about an index. The difference is in how the table is specified. **JetGetIndexInfo** expects a database (*dbid*) and name of a table (*szTableName*), while [JetGetTableIndexInfo](gg294102\(v=exchg.10\).md) expects a table identifier (*tableid*).

#### Requirements

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Client</strong></p></td>
<td><p>Requires Windows Vista, Windows XP, or Windows 2000 Professional.</p></td>
</tr>
<tr class="even">
<td><p><strong>Server</strong></p></td>
<td><p>Requires Windows Server 2008, Windows Server 2003, or Windows 2000 Server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Header</strong></p></td>
<td><p>Declared in Esent.h.</p></td>
</tr>
<tr class="even">
<td><p><strong>Library</strong></p></td>
<td><p>Use ESENT.lib.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DLL</strong></p></td>
<td><p>Requires ESENT.dll.</p></td>
</tr>
<tr class="even">
<td><p><strong>Unicode</strong></p></td>
<td><p>Implemented as <strong>JetGetIndexInfoW</strong> (Unicode) and <strong>JetGetIndexInfoA</strong> (ANSI).</p></td>
</tr>
</tbody>
</table>


#### See Also

[JET_COLUMNID](gg294104\(v=exchg.10\).md)  
[JET_ERR](gg294092\(v=exchg.10\).md)  
[JET_GRBIT](gg294066\(v=exchg.10\).md)  
[JET_INDEXCREATE](gg269186\(v=exchg.10\).md)  
[JET_INDEXID](gg269327\(v=exchg.10\).md)  
[JET_SESID](gg269253\(v=exchg.10\).md)  
[JET_TABLEID](gg269182\(v=exchg.10\).md)  
[JetGetTableIndexInfo](gg294102\(v=exchg.10\).md)
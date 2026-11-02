Title: Chengdu Ceshi Technology ComputerZ.sys physical memory access
Vendor: Chengdu Ceshi Technology Co., Ltd.
Product: Zwuqi System Driver
Component: ComputerZ.sys
SHA-256: 61e7f9a91ef25529d85b22c39e830078b96f40b94d00756595dded9d1a8f6629
MD5: eaec88a63db9cf9cee53471263afe6fb
SHA-1: 5eed0ce6487d0b8d0a6989044c4fcab1bd845d9e
Size: 13352 bytes
PE timestamp: 2009-04-16 03:38:10 UTC
FileVersion: 1.1.9.416
ProductVersion: 1.1.9.416
OriginalFilename: ComputerZ.Sys
Version-resource product name: Zwuqi System Driver
Version-resource company name: Z武器
Signer: CN="Chengdu Ceshi Technology Co., Ltd.", OU=Digital ID Class 3 - Microsoft Software Validation v2, O="Chengdu Ceshi Technology Co., Ltd.", L=Chengdu, S=Sichuan, C=CN
Certificate thumbprint: 03E6097A553A63D5473CD60523B366BB91535636
Certificate not before: 2009-04-15 00:00:00 UTC
Certificate not after: 2010-04-15 23:59:59 UTC
Authenticode status: Valid
Device: \\.\ComputerZ
PDB: f:\myprojects\硬件检测\gwiopm\gwiopm\amd64\ComputerZ.pdb
CVE: 

Description:

ComputerZ.sys in Chengdu Ceshi Technology Co., Ltd. Zwuqi System Driver FileVersion 1.1.9.416 (SHA-256 61e7f9a91ef25529d85b22c39e830078b96f40b94d00756595dded9d1a8f6629) passes a caller-supplied 32-bit physical address to MmMapIoSpace on IOCTL 0xF1002504 (METHOD_BUFFERED), zero-extends that address, maps a fixed length of four bytes as non-cached, does not validate the address, and stores a caller-supplied 32-bit value there, which allows a local user to write four bytes of physical memory via \\.\ComputerZ. IOCTL 0xF1002500 reads four bytes from the same address. The Authenticode status is Valid, signed by Chengdu Ceshi Technology Co., Ltd. The version-resource CompanyName is Z武器 and the ProductName is Zwuqi System Driver. On 2026-11-02, on an isolated Windows 10 virtual machine, an administrator loaded this file and the service started. The administrator locked one of its own pages at physical address 0x2475e000, wrote 0x3C as the first byte (the next three bytes were 0x00), and did not send either IOCTL. Local account aida-low, a member of Users and not a member of Administrators, opened \\.\ComputerZ, sent IOCTL 0xF1002500, and read 0x0000003C. That account then sent IOCTL 0xF1002504, wrote 0x0000005A, and read 0x0000005A back through IOCTL 0xF1002500, then wrote 0x000000A5 and read 0x000000A5 back the same way. The administrator read the first four bytes of that physical page and saw 5A 00 00 00, then A5 00 00 00. The test did not show a crash. The device security descriptor was O:BAG:SYD:(A;;0x1201bf;;;WD)(A;;FA;;;SY)(A;;FA;;;BA)(A;;0x1200a9;;;RC)S:AI(ML;;NW;;;LW). Everyone (WD) has access mask 0x1201bf, which includes FILE_READ_DATA and FILE_WRITE_DATA.

Suggested fix: On IOCTL 0xF1002504 and IOCTL 0xF1002500, use only a physical address chosen inside the driver, and limit access to \\.\ComputerZ to Administrators and SYSTEM.

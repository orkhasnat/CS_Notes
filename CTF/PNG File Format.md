Source: [PNG Specification](https://www.w3.org/TR/2003/REC-PNG-20031110)

![[../Resources/Saved Pages/Portable Network Graphics (PNG) Specification (Second Edition).pdf|Portable Network Graphics (PNG) Specification (Second Edition)]]

PNG (portable network graphics) have 4 channels - Red, Green, Blue and Alpha.
PNG file signature is `137 80 78 71 13 10 26 10` in **decimal** or ``89 50 4e 47 0d 0a 1a 0a`` in **hex**.

# Data Stream Structure
PNG is divided into chunks. There are total 18 chunks described in the standard. Among them **4 are critical** i.e. each png file has to have these 4 chunks.
They are:
1. IHDR
2. PLTE (may not be present actually in many pngs)
3. IDAT (only one that is allowed multiple times)
4. IEND

## Chunk Layout
Each chunk consists of 3 or 4 fields.
```
| Length | Chunk Type | Chunk Data | CRC |
or,
| Length | Chunk Type | CRC |
```
- **Length** - A four-byte unsigned integer giving the number of bytes in the chunk's data field. The length counts **only** the data field, **not** itself, the chunk type, or the CRC. Zero is a valid length. Although encoders and decoders should treat the length as unsigned, its value shall not exceed 231-1 bytes.
- **Chunk Type** - Four character long chunk name e.g. `IHDR`, `tIME`, `iTXT`, `bKGD` etc 
- **Chunk Data** - The data bytes appropriate to the chunk type, if any. This field can be of zero length.
- **CRC** - A four-byte CRC (Cyclic Redundancy Code) calculated on the preceding bytes in the chunk, including the chunk type field and chunk data fields, but *not* including the length field. The CRC can be used to check for corruption of the data. The CRC is always present, even for chunks containing no data.

### `IHDR` Header
The `IHDR` chunk shall be the first chunk in the PNG datastream. It contains:

| Info| # of Bytes|
|--|--|
|Width|4 bytes|
|Height|4 bytes|
|Bit depth|1 byte|
|Colour type|1 byte|
|Compression method|1 byte|
|Filter method|1 byte|
|Interlace method|1 byte|
|**Total**|***13 byte***|

Width and height give the image dimensions in pixels. They are PNG four-byte unsigned integers. Zero is an invalid value.
Bit depth is a single-byte integer giving the number of bits per sample or per palette index (not per pixel). Valid values are 1, 2, 4, 8, and 16, although not all values are allowed for all color types.
Color type is a single-byte integer that defines the PNG image type. Valid values are 0, 2, 3, 4, and 6.
Bit depth restrictions for each color type are imposed to simplify implementations and to prohibit combinations that do not compress well.

### `IDAT` Header
The `IDAT` chunk contains the actual image data which is the output stream of the compression algorithm.

### `IEND` Header
The `IEND` chunk marks the end of the PNG data stream. The chunk's data field is empty.
# Extraction from `tEXt` Chunk 
There was a challenge in ***squareCTF22*** in misc category, where we needed to find out the flag from the `tEXt` chunk of a PNG file. The chunk contains a keyword and message separated by a  null character. The keyword has `fl_#num` and the message has 2 bytes of the flag. Our target was to extract the `tEXt` chunk, and based on the number in the keyword sort the 2 bytes of the message text and we will have the flag. It can be done by, `pngcheck -7 input.png` or  `pngcheck -t input.png` 
```bash
pngcheck -t input.png | rg fl_ -A 1 
```

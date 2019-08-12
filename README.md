### twelvemonkeys
---
https://github.com/haraldk/TwelveMonkeys

```java
BufferedImage image = ImageIO.read(file);

if (!ImageIO.write(image, format, file)) {
 //
}

ImageInputStream input = ImageIO.createImageInputStream(file);

try {
  Iterator<ImageReader> readers = ImageIO.getImageReaders(input);
  
  if (!readers.hasNext()) {
    throw new IllegalArgumentException("No reader for: " + file);
  }
  
  ImageReader reader = readers.next();
  
  try {
    reader.setInput(input);
    
    reader.addIIOReadWarningListener(...);
    reader.addIIOReadProgressListener(...);
    
    ImageReadParam param = reader.getDefaultReaderParam();
    
    param.setSourceSubsampling(...);
    param.setSourceRegion(...);
    param.setDestination(...);
    
    BufferedImage image = reader.read(0, param);
    
    int numThumbs = reader.getNumThumbnails(0);
  }
  finally {
    reader.dispose();
  }
}
finally {
  input.close();
}



```

```
```

```
```

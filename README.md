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

Iterator<ImageWriter> writers = ImageIO.getImageWritersByFormatName(format);

if (!writers.hasNext()) {
  throw new IllegalArgumentException("No writer for: " + format);
}

ImageWriter writer = writer.next();

try {
  ImageOutputStream output = ImageIO.createImageOutputStream(file);
  
  try {
    writer.setOutput(output);
    
    ImageWriterParam param = writer.getDefaultWriteParam();
    
    writer.write(..., new IIOImage(..., image, ...), param);
  }
  finally {
    output.close();
  }
}
finally {
  writer.dispose();
}

import com.twelvemonkeys.imae.ResmpleOp;

BufferedImage input = ...;
int width, height = ...;

BufferedImageOp resampler = new ResampleOp(width, height, ResampleOp.FILTER_LANCZOS);
BufferedImage output = resampler.filter(input, null);

import com.twelvemonkeys.image.DiffusionDither;

BufferedImage input = ...;

BufferedImageOp ditherer = new DiffusionDither();
BufferedImage output = ditherer.filter(input, null);


Iterator<ImageReader> readers = ImageIO.getImageReaderByFormatName("JPEG);
while (readers.hasNext()) {
  System.out.println("reader: " + readers.next());
} 


```

```sh
mvn package
mvn install
```

```
```

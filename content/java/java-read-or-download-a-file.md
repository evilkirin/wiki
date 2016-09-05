---
title: "Read or Download a File from The Internet"
date: 2016-09-05 21:14
---

最近老是和非本地的文件打交道，要不是读一个远程的资源文件的内容，就是将一个远程的资源弄到本地进行处理。这些远程资源都能够用一个URL来标示。

最稳妥功能最全面的肯定是HttpClient，但是纯粹为了这么一个基础的功能要去引入HttpClient还是有些心有不甘。特别是如果你还见过Groovy中GString的无比方便：

```groovy
def content = "http://www.xxx.com/url.html".toURL().text
```

我需要的是能够用尽量少的代码读取或者下载URL资源。Google一番之后，在一堆StackOverflow的问答中整理了一下答案。

## Download

### Java Nio

```java
URL website = new URL("http://www.website.com/information.asp");
ReadableByteChannel rbc = Channels.newChannel(website.openStream());
FileOutputStream fos = new FileOutputStream("information.html");
fos.getChannel().transferFrom(rbc, 0, Long.MAX_VALUE);
```

并非最好的方式，因为transform方法无法保证一次能成功将文件的所有内容transform到目标stream。除此之外，这个场景下，zero-copy实际上并不生效。

> A single call isn't adequate. transferFrom() isnt' specified to complete the entire transfer in a single call. That's why it returns a count. You have to loop.
> 
> URL::openStream()returns just a regular stream, meaning the entire traffic is still being copied through Java byte[] arrays instead of remaining in native buffers. Only fos.getChannel()is actually a native channel, so the overhead remains in full. That's zero gains from using NIO in this case.

### Commons io

```java
FileUtils.copyURLToFile(url, fileToBeDownloaded);

public static void copyURLToFile(URL source, File destination) throws IOException {
    InputStream input = source.openStream();
    copyInputStreamToFile(input, destination);
}

public static void copyInputStreamToFile(InputStream source, File destination) throws IOException {
    try {
        FileOutputStream output = openOutputStream(destination);
        try {
            IOUtils.copy(source, output);
            output.close(); // don't swallow close Exception if copy completes normally
        } finally {
            IOUtils.closeQuietly(output);
        }
    } finally {
        IOUtils.closeQuietly(source);
    }
}

public static int copy(InputStream input, OutputStream output) throws IOException {
    long count = copyLarge(input, output);
    if (count > Integer.MAX_VALUE) {
        return -1;
    }
    return (int) count;
}

private static final int DEFAULT_BUFFER_SIZE = 1024 * 4;

public static long copyLarge(InputStream input, OutputStream output)
        throws IOException {
    return copyLarge(input, output, new byte[DEFAULT_BUFFER_SIZE]);
}

public static long copyLarge(InputStream input, OutputStream output, byte[] buffer)
        throws IOException {
    long count = 0;
    int n = 0;
    while (EOF != (n = input.read(buffer))) {
        output.write(buffer, 0, n);
        count += n;
    }
    return count;
}
```

'The answer'.

### Java 8 

```java
URL website = new URL("http://www.website.com/information.asp");
try (InputStream in = website.openStream()) {
    Files.copy(in, target, StandardCopyOption.REPLACE_EXISTING);
}
```

Preferred in Java 8.

## Read the Content

### Java Scanner

```java
// The core part.
String out = new Scanner(new URL("http://www.google.com").openStream(), "UTF-8").useDelimiter("\\A").next();

// Complete version: http://stackoverflow.com/questions/4328711/read-url-to-string-in-few-lines-of-java-code#comment44940386_13632114
public String s(URL u) throws IOException{
    HttpURLConnection c=null;
    InputStream i=null;
    Scanner s=null;
    try{
        c=(HttpURLConnection) u.openConnection();
        // 如果要设置超时，就只能先拿HttpURLConnection，再拿InputStream了
        c.setConnectTimeout(5000);
        c.setReadTimeout(25000);
        i=c.getInputStream();
        // The regular expression \\A matches the beginning of input. This tells Scanner to tokenize the entire stream, from beginning to (illogical) next beginning. 
        s=new Scanner(i,"UTF-8").useDelimiter("\\A");
        return s.hasNext()?s.next():"";
    } finally {
        if(s!=null)
            s.close();
        if(i!=‌​null)
            try{
                i.close();
            } ‌​catch(IOException e){}
        if(c != null)
            c.disconnect();
    }
}
```

### Commons io

```java
IOUtils.toString(URL url, String encoding)

public static String toString(URL url, Charset encoding) throws IOException {
    InputStream inputStream = url.openStream();
    try {
        return toString(inputStream, encoding);
    } finally {
        inputStream.close();
    }
}

public static String toString(InputStream input, Charset encoding) throws IOException {
    StringBuilderWriter sw = new StringBuilderWriter();
    copy(input, sw, encoding);
    return sw.toString();
}

public static void copy(InputStream input, Writer output, Charset encoding) throws IOException {
    InputStreamReader in = new InputStreamReader(input, Charsets.toCharset(encoding));
    copy(in, output);
}
```

### Java 8

```java
URLConnection conn = url.openConnection();
try (BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream(), StandardCharsets.UTF_8))) {
    pageText = reader.lines().collect(Collectors.joining("\n"));
}
```

Preferred in Java 8.

## Summary

其实看下来，并没有什么特别的技巧，具体的实现基本就是标准答案。能用Commons就别再去费事儿写一遍了，除非你想练习练习基础。

不过，如果是正式项目，还是用HttpClient更稳妥一些。HttpClient还很方便地提供其他的一些功能，比如超时设置，302的支持，cookie的支持等。只要是请求涉及到http相关的一些额外处理，上边的方式都无法胜任了。

### Refs

- [How to download and save a file from Internet using Java? - Stack Overflow](http://stackoverflow.com/questions/921262/how-to-download-and-save-a-file-from-internet-using-java#comment729329_921400)
- [http - Read url to string in few lines of java code - Stack Overflow](http://stackoverflow.com/questions/4328711/read-url-to-string-in-few-lines-of-java-code)
- [How to read a text file directly from Internet using Java? - Stack Overflow](http://stackoverflow.com/questions/6259339/how-to-read-a-text-file-directly-from-internet-using-java)
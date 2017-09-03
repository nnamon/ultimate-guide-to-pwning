# Scripting for CTFs - Basic File Operations

This was originally part of the tutorial series 'Scripting for CTFs' on the
Nandy Narwhals [blog](https://nandynarwhals.org).

## Introduction

Welcome to the first of many tutorial posts written by the Dystopian Narwhals
CTF team for beginners to CTFs treating on the basics of scripting. In this
post, we will deal with simple file operations, which are used heavily when one
is required to parse data, both text and binary, locally stored in a file on the
disk.

Before we begin, for those who want to follow along at home, you can download
the following files:

1. [tangomaureen.txt](./assets/files/tangomaureen.txt)
2. [alice.jpg](./assets/files/Alice-facepalm.jpg)

## Reading from a File

```shell
$ ls tangomaureen.txt
tangomaureen.txt

$ cat tangomaureen.txt
The samples won't delay but the cable
There's another way, say something, anything
Test, one, two, three, anything but that

... snip ...

Why do we love when she's mean?
And she can be so obscene
My Maureen, the 'Tango Maureen'

$ python readfile.py
The samples won't delay but the cable
There's another way, say something, anything
Test, one, two, three, anything but that

... snip ...

Why do we love when she's mean?
And she can be so obscene
My Maureen, the 'Tango Maureen'
```

What is happening in the above snippet is that we list the files in the current
directory, and can see that the file tangomaureen.txt exists. We can view the
contents using the ‘cat’ program. Now, let’s emulate that behaviour in our own
script to demonstrate the ability to read the data from a file into something we
can manipulate (like a string object).

### Python

```python
tango = open("tangomaureen.txt")
data = tango.read()
print(data)
```
### Java

```java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class ReadFile {
    public static void main(String[] args) {
    try {
        String content = new Scanner(new File("tangomaureen.txt")).useDelimiter("\\Z").next();
        System.out.println(content);
    }
    catch (FileNotFoundException e) {
        e.printStackTrace();
    }
    }
}
```

### C

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
  char * buffer = 0;
  long length;
  FILE * fp = fopen("tangomaureen.txt", "r");

  if (fp) {
    fseek(fp, 0, SEEK_END);
    length = ftell(fp);
    fseek(fp, 0, SEEK_SET);
    buffer = malloc(length);
    if (buffer) {
    fread(buffer, 1, length, fp);
    }
    fclose(fp);
  }

  if (buffer) {
      printf("%s", buffer);
  }

}
```

### Ruby

```ruby
tango = File.open("tangomaureen.txt","r")
data = tango.read
puts data
```

No surprise it's actually that simple.

## Reading from a Binary File

Now, reading from a binary file is a little different. It has to be noted that,
in Python 2 not setting the mode to binary when opening the stream does not have
any ill side-effects but in Python 3, there are some
[complications](http://www.pythoncentral.io/encoding-and-decoding-strings-in-python-3-x/).

Now, we will be operating on the alice.jpg file provided above and printing the
word "JFIF" located between the 6th and 10th byte in the header.

```shell
$ ls alice.jpg
alice.jpg

$ file alice.jpg
alice.jpg: JPEG image data, JFIF standard 1.01

$ python readbinaryfile.py
JFIF
```

### Python

```python
alice = open("alice.jpg", "rb") # Sets the mode to 'read' in 'binary'
data = alice.read()
print data[6:10]
```

### Java

```java
import java.nio.file.FileSystems;
import java.nio.file.Files;
import java.nio.file.Path;
import java.io.IOException;

public class ReadBinary {
    public static void main(String[] args) {
    try {
        Path p = FileSystems.getDefault().getPath("", "alice.jpg");
        byte [] fileData = Files.readAllBytes(p);
        String data = "";
        for (int i = 6; i <= 10; i++) {
        data += (char) fileData[i];
        }
        System.out.println(data);
    }
    catch (IOException e) {
        e.printStackTrace();
    }
    }
}
```

### C

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
  char * buffer = 0;
  long length;
  FILE * fp = fopen("alice.jpg", "rb");

  if (fp) {
    fseek(fp, 0, SEEK_END);
    length = ftell(fp);
    fseek(fp, 0, SEEK_SET);
    buffer = malloc(length);
    if (buffer) {
    fread(buffer, 1, length, fp);
    }
    fclose(fp);
  }

  if (buffer) {
    int i;
    for (i = 6; i < 10; i++) {
      printf("%c", buffer[i]);
    }
    printf("\n");
  }

}
```

### Ruby

```ruby
alice = File.open("alice.jpg","rb")
data = alice.read
puts data[6..10]
```

## Writing to a File

Now, let's say we want to do the opposite. Instead of reading from a file, we
want to write to one. Let's pick a simple thing like: "write the numbers 1 to 7,
with each number on its own line, to a file named numbers.txt".

```shell
$ ls numbers.txt
ls: cannot access numbers.txt: No such file or directory

$ python writefile.py

$ ls numbers.txt
numbers.txt

$ cat numbers.txt
1
2
3
4
5
6
7
```

### Python

```python
numbers = open("numbers.txt", "w")
data = ""
for i in range(1, 8):
    data += "%d\n" % i
numbers.write(data)
```

### Java

```java
import java.io.PrintWriter;
import java.io.FileNotFoundException;

public class WriteFile {
    public static void main(String[] args) {
    try {
        PrintWriter writer = new PrintWriter("numbers.txt");
        for (int i = 1; i < 8; i++) {
        writer.println(String.valueOf(i));
        }
        writer.close();
    }
    catch (FileNotFoundException e) {
        e.printStackTrace();
    }
    }
}
```

### C

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
  FILE *fp = fopen("numbers.txt", "w");
  int i;
  for (i = 1; i < 8; i++) {
    fprintf(fp, "%d\n", i);
  }
  fclose(fp);
}
```

### Ruby

```ruby
numbers = File.open("numbers.txt", "w")
data = ""

for i in 1..8
  data += "%d\n" % i
end
numbers.puts data
numbers.close
```

## Exercise Challenge: Lucky Number Seven

Now that we know how to read and write to files, let's try out a sample
challenge! This challenge has the following description:

*We have received this [file](./assets/files/luckynumberseven.txt)
containing an encoded secret message. They told us to submit it in the form of
file containing the string "[flag]<decoded secret message[flag]" to a website.
Can you please create the file for me?*

Okay, so the first thing to do is to view the contents of the file to ascertain
what we must do to extract the secret message.

```shell
$ cat luckynumberseven.txt
fAAAAAAlAAAAAAaAAAAAAgAAAAAA{AAAAAASAAAAAA4AAAAAAmAAAAAApAAAAAAlAAAAAA3AAAAAA_AAAAAAFAAAAAA1AAAAAAlAAAAAA3AAAAAA_AAAAAAOAAAAAApAAAAAA5AAAAAA_AAAAAAFAAAAAAlAAAAAA4AAAAAAGAAAAAA}AAAAAA
```

Immediately, we notice that it seems that the first and every seventh letter
isn't an A. Perhaps, we can extract the secret message by taking every seventh
letter and putting them together. We could do this by hand, but we are extremely
lazy people so we'll write a short script instead. After putting them together,
we will even write the message to a file in the format requested!

```shell
$ ls decoded.txt
ls: cannot access decoded.txt: No such file or directory

$ python luckyseven.py

$ ls decoded.txt
decoded.txt

$ cat decoded.txt
[flag]flag{S4mpl3_F1l3_Op5_Fl4G}[flag]
```

### Python

```python
lucky = open("luckynumberseven.txt")  # Open a file for reading.
data = lucky.read()                   # Read the contents of the file.
message = data[::7]                   # Extract every 7th letter with slice notation.
message = "[flag]%s[flag]" % message  # Use format strings to format the message as requested.
decoded = open("decoded.txt", "w")    # Open a file for writing.
decoded.write(message)                # Write the message to the file.
```

### Java

```java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;
import java.io.PrintWriter;

public class LuckySeven {
    public static void main(String[] args) {
    try {
        String content = new Scanner(new File("luckynumberseven.txt")).useDelimiter("\\Z").next();
        String flag = "";
        for (int i = 0; i < content.length(); i++) {
        if (i % 7 == 0) {
            flag += content.charAt(i);
        }
        }
        flag = "[flag]" + flag + "[flag]";
        PrintWriter writer = new PrintWriter("decoded.txt");
        writer.println(flag);
        writer.close();
    }
    catch (FileNotFoundException e) {
        e.printStackTrace();
    }
    }
}
```

### C

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
  char * buffer = 0;
  long length;
  FILE * fp = fopen("luckynumberseven.txt", "r");

  fseek(fp, 0, SEEK_END);
  length = ftell(fp);
  fseek(fp, 0, SEEK_SET);
  buffer = malloc(length);
  fread(buffer, 1, length, fp);
  fclose(fp);

  char * flagbuffer = 0;
  int i;
  flagbuffer = malloc(length/7+1);
  memset(flagbuffer, 0, sizeof(flagbuffer));
  for (i = 0; i < length; i++) {
    if (i % 7 == 0) {
      flagbuffer[i/7] = buffer[i];
    }
  }

  FILE * flagp = fopen("decoded.txt", "w");
  fprintf(flagp, "[flag]%s[flag]\n", flagbuffer);
  fclose(flagp);
}
```

### Ruby

```ruby
lucky = File.open("luckynumberseven.txt")
data = lucky.read
message = ""
(0..data.length - 1).step(7).each do |i|
  message+= data[i]
end
message = "[flag]%s[flag]" % message
decoded = File.open("decoded.txt", "w")
decoded.puts message
```

## Conclusions

This concludes our short tutorial on Scripting for CTFs: Basic File Operations.
Do look out for our next post in this series.

Thank you for reading!


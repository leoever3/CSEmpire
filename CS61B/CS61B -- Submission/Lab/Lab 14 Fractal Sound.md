### Abstract



##### Given files

* Interface: `Generator`
* `GeneratorPlayer`: plays the samples
* `GeneratorDrawer`: Draw the graph
* GeneratorAudioVisualizer
* MultiGenerator

#### Playing

```java
		Generator generator = new SineWaveGenerator(440);
    GeneratorPlayer gp = new GeneratorPlayer(generator);
    gp.play(1000000);
```

- Creates a SineWaveGenerator that outputs **samples** corresponding to a 440 Hz sine wave.
- Creates a GeneratorPlayer that will **play** the SineWaveGenerator.
- Tells the GeneratorPlayer to **play the first one million** samples from the generator as sound.





### Bitwise operation

* `&`
  * The `&` operation generates a new integer where the ith bit is 1 if both the ith bit of two integer is 1, and 0 otherwise.

```java
    int x = 231 & 62;
    //x = 38
    
    231: 11100111
    62:  00111110

    x:   00100110
```

* `>>>`
  * The `>>>` operation moves all bits in the number n bits to the right, filling in any top digits with zeros

```java
    int x = 231 >>> 3;
    
    231:       11100111
    231 >>> 1: 01110011
    231 >>> 2: 00111001
    231 >>> 3: 00011100
```


### Abstract

**Write some time to figure out what is a good hashCode method.**

* Hashing

### Task

#### Overriding .equal

* Default equal method
  * Reference equal

```java
@Override
public boolean equals(Object o) {
    if (o == this) return true;
    if (o == null) return false;
    if (o.getClass() != this.getClass()) return false;
    SimpleOomage that = (SimpleOomage) o;
    return (this.red == that.red) && (this.green == that.green) && (this.blue == that.blue);
}
```

#### Overriding .hashCode

* Default hashcode
  * Also compute the **memory**

* It is generally necessary to **override** the `hashCode`method whenever the `equals` method is overridden, so as to maintain the general contract for the `hashCode` method, which states that **equal objects must have equal hash codes**.

#### Perfect hashCode

#### TestPerfect

```java
@Test
public void testHashCodePerfect() {
    final int length = (255 / 5 + 1) * (255 / 5 + 1) * (255 / 5 + 1);
    int[] red = new int[length];
    int[] green = new int[length];
    int[] blue = new int[length];
    int timer = 0;
    int collision = 0;
    for (int i = 0; i <= 255; i += 5) {
        for (int j = 0; j <= 255; j += 5) {
            for (int k = 0; k <= 255; k += 5) {
                red[timer] = i;
                green[timer] = j;
                blue[timer] = k;
                timer += 1;
            }
        }
    }
    for (int i = 0; i < length; i++) {
        SimpleOomage temp = new SimpleOomage(red[i], green[i], blue[i]);
        for (int j = i + 1; j < length; j++) {
            SimpleOomage temp2 = new SimpleOomage(red[j], green[j], blue[j]);
            if (temp.hashCode() == temp2.hashCode()) {
                collision += 1;
                if (collision == 1 || collision == 2) {
                    System.out.println(temp.hashCode());
                    System.out.println(" " + red[i] + " " + green[i] + " " + blue[i]);
                    System.out.println(temp2.hashCode());
                    System.out.println(" " + red[j] + " " + green[j] + " " + blue[j]);
                    System.out.println("i" + i + " j" + j);
                }
            }
        }
    }
    System.out.println(collision);
    assertEquals(0, collision);
}
```

Datastructure: 3 Array

#### PerfectHashCode

```java
@Override
public int hashCode() {
    if (!USE_PERFECT_HASH) {
        return red + green + blue;
    } else {
        return red + 10000 * green + 100 * blue;
    }
}
```

#### Nice Spread

```java
int bucketNum;
int[] buckets = new int[M];
int N = oomages.size();
for (Oomage o: oomages) {
    bucketNum = (o.hashCode() & 0x7FFFFFFF) % M;
    buckets[bucketNum] += 1;
}
for (int i : buckets) {
    if (i < N / 50 || i > N / 2.5) {
        return false;
    }
}
return true;
```



#### Visually

* Even though my hashcode is perfect, it’s always returning a multiple of 5. So if the busketsNum = 10, it will not distribute evenly.



#### Test Complex oomage

```java
@Test
public void testWithDeadlyParams() {
    List<Oomage> deadlyList = new ArrayList<>();

    // Your code here.
    int N = 1000;
    int cap = 8;
    List<Integer> params;
    for (int i = 0; i < N; i += 1) {
        params = new ArrayList<>(cap);
        params.add(StdRandom.uniform(0, 255));
        params.add(StdRandom.uniform(0, 255));
        for (int j = 0; j < cap - 2; j += 1) {
            params.add(3 * j);
        }
        deadlyList.add(new ComplexOomage(params));
    }
    assertTrue(OomageTestUtility.haveNiceHashCodeSpread(deadlyList, 10));
}
```



### Issues

* Not familiar with the **2-dimension array** or array of List
* Need some more **debug** techniques
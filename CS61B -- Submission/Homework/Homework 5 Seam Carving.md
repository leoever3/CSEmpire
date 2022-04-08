### Abstraction

* Seam-carving
  * a content-aware image resizing technique
  * the image is reduced in size by one pixel of height/width at a time

* Create a data type that resizes a W-by-H image using the seam-carving technique
* column x and row y
  * consistent with the Picture data type in stdlib.jar

### Task

1. Energy calculation

* calculate the energy of each pixel
* high energy pixel corresponds to a pixel where there is a sudden change in color
  *  avoids removing such pixels

2. Seam identification

* find the shortest path from anu of W pixels in the top row to any of the W pixels in the bottom row.

3. Seam removal





```java
import edu.princeton.cs.algs4.Picture;
import java.awt.Color;

public class SeamCarver {
    private Picture picture;
    private double[][] energyPoint; // calculate the energy of each pixel point
//    private int width;
//    private int height;

    public SeamCarver(Picture picture) {
        this.picture = picture;
        energyPoint = new double[height()][width()];
        for (int i = 0; i < height(); i += 1) {
            for (int j = 0; j < width(); j += 1) {
                energyPoint[i][j] = energy(j, i);
            }
        }
    }

    // current picture
    public Picture picture() {
        return new Picture(picture);
    }

    // width of current picture
    public int width() {
        return picture.width();
    }

    // height of current picture
    public int height() {
        return picture.height();
    }

    // energy of pixel at column x and row y
    public double energy(int x, int y) {
        Color leftColor, rightColor, upColor, downColor;
        if (x == 0) {
            leftColor = picture.get(width() - 1, y);
        } else {
            leftColor = picture.get(x - 1, y);
        }
        if (x == width() - 1) {
            rightColor = picture.get(0, y);
        } else {
            rightColor = picture.get(x + 1, y);
        }
        if (y == 0) {
            upColor = picture.get(x, height() - 1);
        } else {
            upColor = picture.get(x, y - 1);
        }
        if (y == height() - 1) {
            downColor = picture.get(x, 0);
        } else {
            downColor = picture.get(x, y + 1);
        }
        int dx = (leftColor.getRed() - rightColor.getRed())
                * (leftColor.getRed() - rightColor.getRed())
                + (leftColor.getGreen() - rightColor.getGreen())
                * (leftColor.getGreen() - rightColor.getGreen())
                + (leftColor.getBlue() - rightColor.getBlue())
                * (leftColor.getBlue() - rightColor.getBlue());
        int dy = (upColor.getRed() - downColor.getRed())
                * (upColor.getRed() - downColor.getRed())
                + (upColor.getGreen() - downColor.getGreen())
                * (upColor.getGreen() - downColor.getGreen())
                + (upColor.getBlue() - downColor.getBlue())
                * (upColor.getBlue() - downColor.getBlue());
        return dx + dy;
    }


    // sequence of indices for vertical seam
    public int[] findVerticalSeam() {
        // minEnergy is the minimum cost path ending at (i, j)
        double[][] minEnergy = new double[height()][width()];

        if (width() == 1) {
            return new int[]{0};
        }

        // initiate the first row of minEnergy
        for (int i = 0; i < width(); i += 1) {
            minEnergy[0][i] = energyPoint[0][i];
        }
        // initiate the rest rows of minEnergy
        for (int i = 1; i < height(); i += 1) {
            for (int j = 0; j < width(); j += 1) {
                if (j == 0) {
                    minEnergy[i][j] = energyPoint[i][j]
                            + Math.min(minEnergy[i - 1][j], minEnergy[i - 1][j + 1]);
                } else if (j == width() - 1) {
                    minEnergy[i][j] = energyPoint[i][j]
                            + Math.min(minEnergy[i - 1][j], minEnergy[i - 1][j - 1]);
                } else {
                    minEnergy[i][j] = energyPoint[i][j] + Math.min(Math.min(minEnergy[i - 1][j],
                            minEnergy[i - 1][j + 1]), minEnergy[i - 1][j - 1]);
                }
            }
        }
        // find the minimum cost in the last row
        int[] seam = new int[height()];
        int k = 0;
        for (int i = 1; i < width(); i += 1) {
            if (minEnergy[height() - 1][i] <= minEnergy[height() - 1][k]) {
                k = i;
            }
        }
        seam[height() - 1] = k;
        // find the upstairs' seams
        for (int i = height() - 2; i >= 0; i -= 1) {
            for (int j = 0; j < width(); j += 1) {
                if (minEnergy[i][j] == minEnergy[i + 1][k]
                        - energyPoint[i + 1][k] && (j - k <= 1 && j - k >= -1)) {
                    k = j;
                    seam[i] = k;
                    break;
                }
            }
        }
        return seam;
    }


    // sequence of indices for horizontal seam
    public int[] findHorizontalSeam() {
        int[] res;
        transpose();
        res = findVerticalSeam();
        transpose();
        return res;
    }

    // help method to transpose the picture to reduce redundant
    private void transpose() {
        Picture trans = new Picture(this.height(), this.width());
        for (int row = 0; row < width(); row += 1) {
            for (int col = 0; col < height(); col += 1) {
                trans.set(col, row, this.picture.get(row, col));
            }
        }
        SeamCarver newSV = new SeamCarver(trans);
        this.picture = newSV.picture;
        this.energyPoint = newSV.energyPoint;
    }


    // remove horizontal seam from picture
    public void removeHorizontalSeam(int[] seam) {
        picture = SeamRemover.removeHorizontalSeam(picture, seam);
    }

    // remove vertical seam from pic
    public void removeVerticalSeam(int[] seam) {
        picture = SeamRemover.removeVerticalSeam(picture, seam);
    }
}

```


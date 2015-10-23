### 10.11\. Solving the Problem

Because we have <a name="iddle2436"></a><a name="iddle2437"></a><a name="iddle2438"></a><a name="iddle2439"></a>determined that the reading of pixel values is taking a significant amount of time, there is yet another solution that may solve the problem. We have to start looking at how the filter runs. As it generates the new image, it repeatedly asks for the same pixel. Because the new pixel value is based on the pixels that surround it, during the course of running the filter on the image, each pixel can be accessed by each of its nine neighbors. This means that each pixel in the image will be read by each of its neighbors and, as a result, it is read at least nine times.

Because the calls to the GIMP library are expensive, we would only like to do them once for each pixel rather than nine times. It is possible to optimize access to the image by reading the entire image into a local array when the filter starts up, and then accessing this local array as the filter runs, rather than calling the GIMP library routines each time we want to access the data. This method should significantly reduce the overhead for looking up the pixel data. Instead of a couple of function calls for each data access, we just access our local array. On filter initialization, the array is allocated with <tt>malloc</tt> and filled with the pixel data. This is shown in <a name="iddle2440"></a><a name="iddle2441"></a><a name="iddle2442"></a><a name="iddle2443"></a>[Listing 10.14](ch10lev1sec11.html#ch10ex14).

<a name="ch10ex14"></a>

##### Listing 10.14\.

<pre>int g_image_width, g_image_height;

GimpRGB *g_cached_image;

void cache_image(GimpPixelRgn *src_rgn,int width,int height)

{

  static guchar data[4];

  int x,y;

  GimpRGB *current_pixel;

  g_image_width = width;

  g_image_height = height;

  g_cached_image = malloc(sizeof(GimpRGB)*width*height);

  current_pixel = g_cached_image;

  /* Malloc */

  for (y = 0; y < height; y++)

    {

      for (x = 0; x < width; x++)

        {

          gimp_pixel_rgn_get_pixel (src_rgn, data, x, y);

          gimp_rgba_set_uchar (current_pixel, data[0], data[1], data[2],

data[3]);

          current_pixel++;

        }

    }

</pre>

In addition, the <tt>peek</tt> routine has been <a name="iddle2444"></a><a name="iddle2445"></a><a name="iddle2446"></a><a name="iddle2447"></a>rewritten just to access this local array rather than call into the GIMP library functions. This is shown in [Listing 10.15](ch10lev1sec11.html#ch10ex15).

<a name="ch10ex15"></a>

##### Listing 10.15\.

<pre>static void peek (GimpPixelRgn *src_rgn,

      gint          x,

      gint          y,

      GimpRGB      *color)

{

  *color = g_cached_image[y*g_image_width + x];

}

</pre>

So, does it work? When we run the filter using the new method, runtime has decreased to 56 seconds! This is well within our goal of 2 minutes and 30 seconds, and it is a significant boost in performance.

The performance, though impressive, did not come for free. We made one of the classic trade-offs in performance engineering: We increased performance at the expense of memory usage. For example, when a 1280x1024 image is used with this filter, we require 5 additional megabytes of memory. For very big images, it may not be practical to cache this data; for reasonably sized images, however, a 5MB increase in memory usage seems like a good sacrifice for a filter that <a name="iddle2448"></a><a name="iddle2449"></a><a name="iddle2450"></a><a name="iddle2451"></a>is more than two times as fast.
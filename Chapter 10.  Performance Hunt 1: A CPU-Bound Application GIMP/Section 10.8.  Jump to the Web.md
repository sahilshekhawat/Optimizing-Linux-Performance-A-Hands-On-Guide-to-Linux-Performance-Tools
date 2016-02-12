### 10.8\. Jump to the Web

Now that we have found which GIMP functions are used for much of the time, we have to figure out exactly what these functions are and possibly optimize their use.

First, we search the Web <a name="iddle2405"></a><a name="iddle2406"></a><a name="iddle2407"></a><a name="iddle2408"></a><a name="iddle2409"></a>for <tt>pixel_rgn_get_pixel</tt> and try to determine what it does. After a few false starts, the following link and information revealed in [Listing 10.11](ch10lev1sec8.html#ch10ex11) confirm our suspicions about what <tt>pixel_rgn_get_pixel</tt> does.

<a name="ch10ex11"></a>

##### Listing 10.11\.

<pre>"There are calls for pixel_rgn_get_ pixel, row, col, and rect, which grab

data from the image and dump it into a buffer that you've pre-allocated.

And there are set calls to match. Look for "Pixel Regions" in gimp.h."

(from http://gimp-plug-ins.sourceforge.net/doc/Writing/html/sect-

image.html )

</pre>

In addition, the information in [Listing 10.12](ch10lev1sec8.html#ch10ex12) suggests that it is a good idea to avoid using <tt>pixel_rgn_get_ calls</tt>.

<a name="ch10ex12"></a>

##### Listing 10.12\.

<pre>"Note that these calls are relatively slow, they can easily be the

slowest thing in your plug-in. Do not get (or set) pixels one at a time

using pixel_rgn_[get|set]_pixel if there is any other way. " (from

http://www.home.unix-ag.org/simon/gimp/guadec2002/gimp-

plugin/html/imagedata.html)

</pre>

In addition, the Web search yields information about <a name="iddle2410"></a>the <tt>gimp_rgb_set_uchar</tt> function by simply turning up the source for the function. As shown in [Listing 10.13](ch10lev1sec8.html#ch10ex13), this call just packs the red, green, and blue values into a <tt>GimpRGB</tt> structure that represents a single color.

<a name="ch10ex13"></a>

##### Listing 10.13\.

<pre>void

gimp_rgb_set_uchar (GimpRGB *rgb,

                    guchar r,

                    guchar g,

                    guchar b)

{

  g_return_if_fail (rgb != NULL);

  rgb->r = (gdouble) r / 255.0;

  rgb->g = (gdouble) g / 255.0;

  rgb->b = (gdouble) b / 255.0;

}

</pre>

Information gleaned from the Web confirms our suspicion: The <tt>pixel_rgn_get_ pixel</tt> function is a way to extract image <a name="iddle2411"></a><a name="iddle2412"></a>data from the image, and <tt>gimp_rgba_set_uchar</tt> is just a way to take the color data returned by <tt>pixel_rgn_get_pixel</tt> and put it into the <tt>GimpRGB</tt> data structure.

Not only do we see how these functions are used, other pages also hint that they may not be the best functions to use if we want the filter to perform at its peak. One Web page ([http://www.home.unix-ag.org/simon/gimp/guadec2002/gimp-plugin/html/efficientaccess.html](http://www.home.unix-ag.org/simon/gimp/guadec2002/gimp-plugin/html/efficientaccess.html)) suggests that it may be possible to increase performance by using the GIMP image cache. Another Web site ([http://gimp-plug-ins.sourceforge.net/doc/Writing/html/sect-tiles.html](http://gimp-plug-ins.sourceforge.net/doc/Writing/html/sect-tiles.html)) suggests that it might be possible to increase performance by rewriting the filter to access the image <a name="iddle2413"></a><a name="iddle2414"></a><a name="iddle2415"></a><a name="iddle2416"></a>data more efficiently.
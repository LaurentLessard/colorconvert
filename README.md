# colorconvert
### A Matlab function for converting between different color coordinate systems

The purpose of the `colorconvert` function is to provide a simple way to convert between different color coordinate systems, using either a standard whitepoint such as D65 or a user-specified whitepoint. Although Matlab's image-processing toolbox provides much of this functionality already, the `colorconvert` function is much simpler to use. The basic syntax is:
```matlab
out = colorconvert(color,colorspace,ref);
```
- `color` is an Nx3 array where each row is a different color (specified by its 3 coordinates).
- `colorspace` is a string indicating the color space in which `color` is specified. Valid options currently include
  - `'XYZ'`: CIE 1931 XYZ color space (X,Y,Z)
  - `'xyY'`: CIE 1931 xyY color space (x,y,Y)
  - `'Lab'`: CIE 1976 L\*a\*b\* color space (L,a,b)
  - `'Luv'`: CIE 1976 L\*u\*v\* (CIELUV) color space (L,u,v)
  - `'LChab'`: cylindrical representation of CIELAB space with the hue angle hab specified in degrees (L,Cab,hab)
  - `'LChuv'`: cylindrical representation of CIELUV space with the hue angle huv specified in degrees (L,Cuv,huv)
  - `'CC'`: cone-opponent contrast space as specified in Eskew, McLellan, and Giulianini (1999). (LMc,Sc,Lumc)
- `ref` is the reference whitepoint used in the conversions. Valid options currently include
  - `'D65'`: CIE Illuminant D65 (white)
  - `'C'`: CIE Illuminant C
  
The second syntax allows the user to specify a custom whitepoint:
```matlab
out = colorconvert(color,colorspace,ref,refspace);
```
- `color` and `colorspace` are the same as above.
- `ref` is now a vector of length 3 indicating the coordinates of the custom whitepoint
- `refspace` is the color space in which `ref` is specified. Valid options include `'XYZ'` and `'xyY'`

### Example
The output `out` is a struct that contains the conversions of the input colors into all the color spaces specified above. For example, to convert a color specified in xyY coordinates by x=0.25, y=0.35, Y=70 into Lab coordinates using a D65 whitepoint, we would write the following code:
```matlab
c = [0.25, 0.35, 70]  % color to be converted, specified in xyY coordinates
out = colorconvert(c,'xyY','D65');
L = out.L
a = out.a
b = out.b
```
The fields contained in the `out` struct are the standard coordinates listed above: `X,Y,Z,x,y,L,a,b,u,v,Cab,Cuv,hab,huv,LMc,Sc,Lumc`. Also included are the saturation in Lab and Luv coordinates: `Sab,Suv` and the whitepoint in XYZ coordinates `Xn,Yn,Zn`.

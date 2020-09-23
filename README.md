<div align="center">

## Graphics Unit for Turbo Pascal 7\.0


</div>

### Description

I didnt know were else on the site this could go, this isnt delphi, its actually for good old Turbo Pascal. Does stuff like get into graphics mode , draw lines,rectangles,circles etc.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Patrick B\.^](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/patrick-b.md)
**Level**          |Beginner
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |Pre Delphi 4
**Category**       |[Graphics](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics__7-43.md)
**World**          |[Delphi](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/delphi.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/patrick-b-graphics-unit-for-turbo-pascal-7-0__7-344/archive/master.zip)





### Source Code

```
{ this is for Turbo Pascal.. not Delphi }
unit mgraphic;
interface
const vga = $a000; { video memory address }
procedure setpixel ( x,y: longint; color: byte);
procedure putpixel (x,y : Integer; Col : Byte);
procedure lineto (x,x2,y: longint; color: byte);
procedure rectangle(x, x2, y, y2: integer; color: byte);
procedure circle (oX,oY,rad:longint;Col:Byte);
procedure SetBkColor( Color: Byte);
procedure SetGraphicMode;
procedure SetTextMode;
implementation
{ set a specific pixel to a color (fast) }
procedure setpixel ( x,y: longint; color: byte);
begin
mem [vga:x+(y*320)]:=color;
end;
{ put a pixel the slow interupts way }
procedure putpixel (x,y : Integer; Col : Byte);
begin
  asm
    mov    ah,0Ch
    mov    al,[col]
    mov    cx,[x]
    mov    dx,[y]
    mov    bx,[1]
    int    10h
  end;
end;
{ draw line.. this algorithm draws a straight line }
procedure lineto (x,x2,y: longint; color: byte);
var count: integer;
begin
for count := x to x2 do
begin
setpixel ( count,y,color);
end;
end;
{ draw a rectangle.. this algorithm draws a rectangle }
procedure rectangle(x, x2, y, y2: integer; color: byte);
var
count: integer;
begin
for count := y to y2 do
begin
lineto(x,x2,count,color);
end;
end;
{ this procedure draws a circle }
procedure circle (oX,oY,rad:longint;Col:Byte);
   VAR deg:real;
     X,Y:integer;
begin
    deg:=0;
    repeat
     X:=round(rad*COS (deg));
     Y:=round(rad*sin (deg));
     setpixel (x+ox,y+oy,Col);
     deg:=deg+0.005;
    until (deg>6.4);
end;
{ set the screen to a color }
procedure SetBkColor( Color: Byte);
begin
fillchar(mem[$a000:0],64000,Color);
end;
{ send a interupt to DOS, to set it into Graphic Mode }
procedure SetGraphicMode;
begin
asm
mov ax,0013h
int 10h
end;
end;
{ send a interupt to DOS, to set it into Text Mode }
procedure SetTextMode;
begin
asm
mov ax,0003h
int 10h
end;
end;
end.
```


![graphpaper](https://user-images.githubusercontent.com/43251090/229385869-8c859780-dcfa-4ac6-b685-e44d62fea255.png)
```Python
'''
 grapher paper generator
 grpaper.py
'''
import vgl

p_wid, p_hgt = vgl.paper.get_paper_letter_inch()
margin_w = 0.31
margin_h = 0.31
f_wid = p_wid-margin_w*2
f_hgt = p_hgt-margin_h*2

fmm = vgl.FrameManager()
frm = fmm.create(margin_w,margin_h,f_wid,f_hgt, vgl.Data(-1,1,-1,1))

unit_grid = 0.0625 # 1./16 inch
grid_dx = unit_grid*2
grid_dy = unit_grid*2

def plot(dev):
    dev.set_plot(frm)
    lthk = 0.001*dev.frm.hgt()
    sy = margin_h
    dev.make_pen(vgl.color.BLACK, lthk)
    ex,ey = margin_w+f_wid,margin_h+f_hgt
    while sy <= ey:
        dev.lline(margin_w, sy, ex, sy)
        sy += grid_dy
        
    sx = margin_w
    while sx <= ex:
        dev.lline(sx, margin_h, sx, ey)
        sx += grid_dx
    dev.delete_pen()
    dev.close()

plot(vgl.DevicePDF("pxlgrid.pdf", fmm.get_gbbox()))
plot(vgl.DeviceWindowsMetafile("pxlgrid.wmf", fmm.get_gbbox()))
```

![graphpaper](https://user-images.githubusercontent.com/43251090/229377301-48924e18-bee6-4109-92d2-9df8982044b5.png)
```Python
'''
 grapher paper generator
 
 grpaper.py

'''
import vgl

p_wid, p_hgt = vgl.paper.get_paper_letter_inch()
margin_w = 0.31
margin_h = 0.31
f_wid = p_wid-margin_w
f_hgt = p_hgt-margin_h

fmm = vgl.FrameManager()
frm = fmm.create(0,0,1,1, vgl.Data(-1,1,-1,1))
dev = vgl.DevicePDF("pxlgrid.pdf", fmm.get_gbbox())
dev.set_plot(frm)

unit_grid = 0.0625 # 1./16 inch
grid_dx = unit_grid*2
grid_dy = unit_grid*2

lthk = 0.0001*dev.frm.hgt()
sy = margin_h
dev.make_pen(vgl.color.BLACK, lthk)
while sy <= f_hgt:
    dev.lline(margin_w, sy, f_wid, sy)
    sy += grid_dy
    
sx = margin_w
while sx <= f_wid:
    dev.lline(sx, margin_h, sx, f_hgt)
    sx += grid_dx
dev.delete_pen()
dev.close()

```

# Exercise
"""
Spyder Editor

This is a temporary script file.
"""
from PIL import Image, ImageEnhance
import matplotlib.pyplot as plt
#打开二维码图片的位置
qrcode = Image.open('C:\\Users\\HP\\Desktop\\12a.PNG').convert('RGBA')
src_size = (qrcode.size[0],qrcode.size[1])
#为方便处理二维码，先将二维码转换为99*99的尺寸
qrcode = qrcode.resize((99,99))
qrcode.size[0]
#显示出二维码
plt.imshow(qrcode)
plt.show()
#打开背景图片
bg = Image.open(r'C:\Users\HP\Desktop\11a.PNG').convert('RGBA')
#显示
bg.size[0]
bg.size[1]
plt.imshow(bg)
plt.show()
# 将新的图片转换为合适的尺寸
if bg.size[0] < bg.size[1]:
    bg = bg.resize((qrcode.size[0]-24, (qrcode.size[0]-24)*int(bg.size[1]/bg.size[0])))
else:
    bg = bg.resize(((qrcode.size[1])*int(bg.size[0]/bg.size[1]), qrcode.size[1]))
'''循环二维码图片各个像素点
    定位元素不能替换、有效数据亦不能替换'''
plt.imshow(bg)
for i in range(qrcode.size[0]):
    for j in range(qrcode.size[1]):
        #忽略左上角定位元素
        if i < 20 and j <20:
            continue
        #忽略右上角
        elif i >79 and j < 20:
            continue
        #忽略左下角
        elif i <20 and j > 79:
            continue
        elif i%3 == 1 and j%3 == 1:
            continue
        #背景中透明的不做处理
        elif bg.getpixel((i,j))[3]==0:
            continue
        else:
            qrcode.putpixel((i,j),bg.getpixel((i,j)))
qrcode = qrcode.resize(src_size)
plt.imshow(qrcode)
plt.show()

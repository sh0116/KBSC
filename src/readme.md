---
# ๐ฉโ๐ฆฏVIDA : ์๊ฐ์ฅ์ ์ธ์ ์ํ ์ด์ง๋ ์ ์ ๋๊ตฌ ์ฃผ์ ์์ค์ฝ๋๐
---


<div align="center"><img src="../asset/logo.png" width="300">
</div>


## Summary๐ซ

| ํ์ผ๋ช | ์ค๋ช | 
| ------ | ------ | 
| FloorPlan_standard.py | ์๋ ฅํ ํ๋ฉด๋ ์ด๋ฏธ์ง๋ฅผ ์๋ ์ ๊ทํํ๋ ์์ค |
| braille_transfer.py | ํ๊น๋ ๊ฑด๋ฌผ์ ๊ตฌ์กฐ์ ๊ฑด๋ฌผ๋ช์ ์ ์๋ก ๋ณํํด์ฃผ๋ ์์ค |
| split_cubeV2.py | ์ ๊ทํ๋ ํ๋ฉด๋ ์ด๋ฏธ์ง๋ฅผ 3D ๋ชจ๋ธ ์ ์์ ์ํด ์์ Cubeํํ๋ก ์ชผ๊ฐ๊ณ  ์ขํ์ ํฌ๊ธฐ๋ฅผ ๋ฐํํ๋ ์์ค|
| excute_blender.py | Blender background python ์ ์คํํ๊ณ  ์์์ ๋ง๋ค์ด์ง ๋ฐ์ดํฐ๋ฅผ ์คํฌ๋ฆฝํธ๋ก ๋๊ธฐ๋ ์์ค |
| blender_script.py | ํ๊น ๋ฐ์ดํฐ์ ํ๋ธ ๋ฐ์ดํฐ๋ฅผ ๊ธฐ๋ฐ์ผ๋ก ๋ชจ๋ธ์ ์์ฑํ๋ ์์ค |

 <br> <br> <br>
## Main Function ๐จโ๐ซ
๐ฆ์์ค ์ฝ๋์ ์ฃผ์ ํจ์ ์๊ฐ

### FloorPlan_standard.py 
์๋ ์ ๊ทํ๋ morphology transformation๋ฅผ ๊ธฐ๋ฐ์ผ๋ก ๋ง๋ค์ด์ง ์์ค์ฝ๋์ด๋ค. <br>
์๋ OpenCV ํจ์ ์ค ์นจ์(Erosion), ํฝ์ฐฝ(Dilation)์ ํ์ฉํด ๋ง๋ค์๋ค.

>    dilate = cv2.dilate(img_binary2, kernel2, anchor=(-1, -1), iterations=1) <br>
>    erode = cv2.erode(dilate, kernel2, anchor=(-1, -1), iterations=2) <br>
>    dilate2 = cv2.dilate(erode, kernel, anchor=(-1, -1), iterations=1) <br>

### braille_transfer.py
Hangul to Braille Converter ๋ผ์ด๋ธ๋ฌ๋ฆฌ hbcvt๋ฅผ ์ฌ์ฉํ์ฌ ๋ง๋  ์์ค์ฝ๋์ด๋ค.<br>

>        for i in hbcvt.h2b.text(place):
>         for j in i[1:]:
>             for k in j:
>                 braille_list.append(k[1:][0][0])


### split_cubeV2.py
Binary Image๋ก ๋ง๋  ํ๋ฉด๋๋ฅผ X๊ฐ์ ๊ธฐ์ค์ผ๋ก ์ ์ ์กฐ์ฌํ๋ค 0๊ณผ 1๋ก ๊ตฌ๋ถํ๊ณ  ์์ํ๋ ๋ถ๋ถ๊ณผ ๋๋๋ ๋ถ๋ถ์ ์ฐพ์ X๊ธธ์ด๊ฐ 1์ธ ๊ธด ๋ง๋๋ฅผ ์์ฑํ๋ค.
<br>

>     for i in range(x-5):
>        for j in range(y-5):
>            cnt = 0
>            while True:
>                for cnt_plus in range(5,0,-1):
>                    if (i,j+cnt+cnt_plus) not in visit and img[i][j+cnt+cnt_plus].tolist() == 0:
>                        cnt+=cnt_plus
>                        visit.add((i,j+cnt))
>                        break
>                else:
>                    break
>            if cnt:
>                if i not in x_dict.keys():
>                    x_dict[i] = list()
>
>                x_dict[i].append([j,j+cnt])
>                box.append([j,j+cnt,i,i])

X๊ธธ์ด๊ฐ 1์ธ ๊ธด ๋ง๋๋ฅผ ๋ชจ๋ ์ถ๋ ฅํ๋ฉด ๋ชจ๋ธ ์์ฑ์ ๊ณผ๋ถํ๊ฐ ๊ฑธ๋ฆฐ๋ค.<br>
X์ ์์น๋ฅผ ๊ธฐ์ค์ผ๋ก ๋ง๋์ ์ฒ์๊ณผ ๋์ ์ขํ๊ฐ ๊ฐ์ ๋ง๋๋ค์ ์ฐพ์ ํ๋๋ก ํฉ์น๋ค. <br>
์ฆ ๊ฐ์ ํฌ๊ธฐ, ๊ฐ์ ์์น์ ์๋ ๋ง๋๋ฅผ ํฉ์ณ X๊ฐ 2์ธ ๊ธด ๋ง๋๋ฅผ ๋ง๋๋ ๊ณผ์ ์ด๋ค
<br>
>      for i in range(len(x_dict_keys)):
>          if (x_dict_keys[i]-x_dict_keys[pre]) == (i-pre) and x_dict[x_dict_keys[pre]] == x_dict[x_dict_keys[i]]:
>              continue
>          else:
>              for temp in x_dict[x_dict_keys[i-1]]:
>                  box_sorted.append(temp+[x_dict_keys[pre],x_dict_keys[i-1]])
>              pre = i



### excute_blender.py
ํ์ฌ Blender์ Python Lib์ธ BPY์ ์ต์  ๋ฒ์ ์ด ํธํ์ฑ ๋ฌธ์ ๋ก ๋ฐฐํฌ๊ฐ ์๋๋ค.<br>
Blender๋ฅผ ๋ฐฑ๊ทธ๋ผ์ด๋๋ก ๋๋ฆฌ๋ฉด์ ๋ด๋ถ์ ์กด์ฌํ๋ Python Console๋ฅผ ์ฌ์ฉํ๋ฉด ์ต์  ๋ฒ์ ์ BPY๋ฅผ ์ฌ์ฉํ  ์ ์๋ค <br>
Blender background์์ ๋์๊ฐ๋ ํ๋ก์ธ์ค๋ก ๋ฉ์ธ ์ธํฐํ์ด์ค ํ๋ก์ธ์ค์ ๋ณ๊ฐ์ ํ๋ก์ธ์ค๋ก ๊ตฌ์ฑ๋๋ค <br>
>      os.system("C:\\VIDA\\Blender_dir\\blender.exe --background --python C:\\VIDA\\FloorPlan\\blender_script.py "+tagstring.replace(" ","")+" "+str(title).replace(" ",""))


### blender_script.py
Function 
- Cube๊ฐ์ฒด๋ฅผ ์์ฑํ๋ ํจ์
- UV๊ฐ์ฒด(๋ฐ๊ตฌ)๋ฅผ ์์ฑํ๋ ํจ์
- ์ ์๋ฅผ ์ ์ํ๋ ํจ์
- ๊ฑด๋ฌผ ๋ฒฝ์ ์ ์ํ๋ ํจ์
- ๊ฑด๋ฌผ์ ๋ฉ์ธ ๋ณด๋๋ฅผ ์ ์ํ๋ ํจ์
- ์ด์ง๋์ Summary๋ฅผ ๋ง๋๋ ํจ์ 
- ์ด์ง๋๋ฅผ ๋ชจ๋ธ ํ์ผ(stl)๋ก ๋ฐํํ๋ ํจ์
